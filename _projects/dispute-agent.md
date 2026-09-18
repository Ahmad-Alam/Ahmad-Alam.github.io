---
layout: page
title: Automated PayPal Dispute Resolution Agent
description: A PayPal dispute automation system that routes each dispute to one of ten narrowly scoped agents, negotiates through a fixed escalating offer ladder, and hands off to a human the moment it runs out of good offers
img: assets/img/projects/dispute-agent-pipeline.svg
importance: 7
category: work
---

A PayPal dispute arrives as a webhook and somebody has to respond fast, on PayPal's clock, not the merchant's. I built the system that handles that response: it reads the dispute, decides what it's actually about, negotiates a resolution through a fixed set of escalating offers, and hands off to a human the moment it runs out of good ones.

```
dispute-agent-service/
├── main.py                 # webhook entrypoint, /paypal-disputes-webhook
├── dispute_processor.py    # orchestrator: stage detection, agent routing, offer tracking
├── evidence_collector.py   # gathers tracking, refund, and order evidence by dispute reason
├── dispute_tools.py        # the tool surface exposed to the agents
├── agent_instructions.py   # ten specialist agent prompts and the offer ladder
├── agents_service.py       # OpenAI Agents SDK runner, model selection
└── paypal_service.py       # OAuth2-backed PayPal Disputes API wrapper
```

{% include figure.liquid loading="eager" path="assets/img/projects/dispute-agent-pipeline.svg" title="Webhook in, evidence gathered, one specialist agent runs the ladder, PayPal gets the response" class="img-fluid rounded z-depth-1" zoomable=true %}

## The offer ladder

Every dispute gets a running offer history and a level counter, starting at zero. The first touch asks for details or evidence. If that doesn't resolve it, the agent makes an offer: a partial coupon plus reshipment, or a return address. If the customer declines, the next offer is bigger, a larger coupon or a coupon-plus-refund split. Decline again and it goes bigger still. After the final tier, the only move left is a full refund and a handoff to a human team.

{% include figure.liquid loading="eager" path="assets/img/projects/dispute-agent-ladder.svg" title="The level counter only moves one direction. Nothing resets it and nothing repeats a tier" class="img-fluid rounded z-depth-1" zoomable=true %}

The counter only moves one direction. An agent can't reset it, repeat an earlier offer, or negotiate outside the ladder. That's the actual design problem dispute automation has to solve. Writing a plausible reply is easy, any model manages that. Knowing when a negotiation is over, and stopping before it loops or gives away more than it should, is the hard part.

## Ten agents, each with one job

Rather than one agent handling every dispute reason, there are ten, each scoped to one situation so its instructions and its offer ladder don't have to cover every case at once.

<div class="table-responsive">
  <table class="table table-sm table-bordered">
    <thead>
      <tr><th>Agent</th><th>Handles</th></tr>
    </thead>
    <tbody>
      <tr><td>Damaged item</td><td>Item arrived broken or defective. Offers repair, reshipment, or refund in escalating tiers.</td></tr>
      <tr><td>Not as described, confirmed</td><td>Item genuinely differs from the listing. Runs the same offer ladder as damaged item.</td></tr>
      <tr><td>Not as described, preference</td><td>Item matches the listing but the customer doesn't like it. Opens with a softer offer.</td></tr>
      <tr><td>Unfulfilled order</td><td>Order never shipped. Cancels it and offers reshipment or a refund.</td></tr>
      <tr><td>Fulfilled order</td><td>Order shipped. Supplies tracking and handles non-receipt claims.</td></tr>
      <tr><td>Return-related</td><td>Customer already started a return. Full refund once it's back, offers otherwise.</td></tr>
      <tr><td>Out of stock</td><td>Item can't be fulfilled. Full refund if the order never shipped, offers otherwise.</td></tr>
      <tr><td>Cancellation</td><td>Order was cancelled. Handled the same way as out of stock.</td></tr>
      <tr><td>Inquiry orchestrator</td><td>Reads the dispute and order state, then routes to the specialist above that fits.</td></tr>
      <tr><td>Claim handler</td><td>Takes over once a dispute escalates past inquiry into a formal claim.</td></tr>
    </tbody>
  </table>
</div>

A damaged-item agent only ever needs to know about damaged-item offers.

## Evidence before the model ever runs

Before any agent sees a dispute, evidence gets collected automatically based on the dispute reason: tracking information for a non-receipt claim, return policy and product details for a not-as-described claim, refund status for a credit dispute, an amount comparison for an incorrect-charge claim. Finding the order behind a dispute isn't always direct, so it falls back through three lookups: a custom field on the transaction first, then an invoice ID, then a search of the storefront by transaction ID if neither of those resolves it.

By the time an agent runs, it already has the order, the delivery status, and whatever evidence its dispute reason calls for sitting in context, roughly this shape:

```json
{
  "dispute_id": "PP-DISPUTE-8841",
  "reason": "NOT_AS_DESCRIBED",
  "stage": "inquiry",
  "order_number": "ORD-10432",
  "order_status": "fulfilled",
  "delivery_status": "delivered",
  "offer_history": ["initial_touch"],
  "current_offer_level": 0,
  "evidence": {
    "tracking_number": "1Z999AA10123456784",
    "return_policy": "30-day return window"
  }
}
```

It isn't guessing at facts it could have just looked up.

## Where the actual work was

Most of the effort here wasn't prompt engineering. It was making the plumbing survive PayPal's actual behavior.

Webhooks aren't as reliable as the diagram makes them look. PayPal retries a failed delivery up to 25 times over 3 days until it gets back a success response, so the same dispute event can and does arrive more than once. The queue consumer has to check whether a dispute_id has already been processed before doing anything with it, or a customer ends up getting the same offer twice.

Signature verification added its own tax. PayPal verifies a webhook by checking its signature against the exact raw request body, so that body has to stay untouched, byte for byte, between arriving and getting verified. Any framework middleware that reformats it first breaks that silently. No error. Just a signature that never matches.

Testing had its own gap. Sandbox makes it easy, fabricate a dispute and test against it directly. Production doesn't work that way. A merchant only ever reacts to a dispute a buyer opens, there's no equivalent button for "create a dispute and see what happens" once it's live. That gap meant the path most likely to cause a surprise in production was the one I could never fully rehearse.

And the Resolution Center dashboard itself, the thing a human opens once a dispute escalates past what the agents can handle, doesn't say outright what stage a dispute is in or which actions are actually available at that stage. I only found out by which buttons were missing. Building the automation meant reverse engineering the same state machine the dashboard already knows and never says out loud.

## The tradeoff I'd flag first

The ladder itself lives in natural language, in each agent's instructions, not in code that validates an offer before it goes out. Nothing checks that an agent is actually on the tier it claims to be on, or refuses an offer that's out of order. The `current_offer_level` counter is trusted state, updated because the instructions say to update it, not enforced by a rule the agent can't get around.

For the ladder it's built around, gpt-4.1 and gpt-5 both follow it reliably in practice. But the ceiling is a convention the model honors, not a limit the system enforces, and that's worth being honest about.

## Where this actually stands

Ten specialist agents, a four-tier offer ladder, evidence auto-collection with a three-way fallback, and a dual-stage handoff: inquiry-stage disputes get a direct message back to the customer, claim-stage disputes get evidence submitted instead, since PayPal closes off its own messaging channel the moment a dispute leaves inquiry stage. Any reply that still needs to reach the customer at that point goes out through Gorgias instead, not through PayPal at all. The model backing it is switchable between gpt-4.1 and gpt-5 through a single environment variable, so cost and behavior can be tuned without touching the pipeline.

The part I'd point to first isn't that it can answer a dispute. Any model can write a reasonable-sounding reply to a customer complaint. The part that matters is that it knows to stop, tier by tier, and put a person back in the loop before it runs out of good options. That's the part most automated dispute handling skips, and it's the part that keeps this one from making a bad situation worse.
