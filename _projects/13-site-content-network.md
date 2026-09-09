---
layout: page
title: Building a 13-Site Content Network
description: How a 13-site AI content network went from zero to 364 published articles, through a hardcoded pipeline, a handoff to an autonomous system, a coordinated tools-and-SEO rollout, and one AI feature that got built, deployed, and paused
img: assets/img/projects/seo-pipeline.svg
importance: 2
category: work
---
Thirteen sites, one industry each, healthcare to freelancing to fashion, aimed at organic search traffic and an email list. I built the pipeline that got the first of them live, then kept building on top of it as the network grew. As of early August 2026 it's produced 364 published articles, every site has its own themed calculator tool, and one of those calculators briefly had a live AI feature bolted onto it before I paused it. None of this happened in one clean phase. It happened in three, and the middle one involved handing the whole operation to a different system entirely.

The repos are private, so here's the layout of the files this case study refers to.

```
content-pipeline/
├── run.py                     # orchestrator, runs phases 1-6 per industry
├── config/
│   └── industries.json        # the 16 configured industries and seed keywords
├── prompts/
│   ├── phase1_keyword_research.txt
│   ├── phase2_cluster_mapping.txt
│   ├── phase3_brief_generation.txt
│   ├── phase4_article_generation.txt
│   └── phase5_optimization.txt
├── data/
│   ├── clusters/               # per-industry cluster map, one file per industry
│   └── inventory/              # what's already published, checked before every new run
├── blog_scheduler.py           # APScheduler cron, generate then publish
├── google_indexing.py          # pings Google's Indexing API on publish
├── image_gen.py                # fal.ai thumbnail generation on publish
└── publish_approved.py         # writes frontmatter, commits to the site repo, verifies it's live
```

```
insights-api/
├── main.py                     # FastAPI app, single POST route
├── deploy/
│   ├── insights-api.service    # systemd unit, hardened
│   └── Caddyfile                # reverse proxy + TLS
└── TODO_SECURITY.md             # deferred hardening items, dated and reasoned
```

### Six phases, one shell command

Each industry moves through the same six phases every time the pipeline runs. Phase one pulls seed keywords for that industry and expands them through autocomplete, People Also Ask, and related searches, then filters by volume, difficulty, and intent, checking the existing inventory first so it never targets a keyword already covered. Phase two maps the survivors onto a pillar-and-cluster structure and plans the internal links. Phase three builds a content brief from what's actually ranking. Phase four writes the article against that brief. Phase five runs an on-page pass, meta title, description, schema markup, and a quality checklist that has to pass before anything moves on.

`run.py` shells out to the Claude Code CLI in headless mode for all six phases, no API key required, auth comes from the same session already logged into the box. Instead of parsing a short answer out of the response text, it gives Claude a file path in the prompt and has it write structured JSON straight to disk, then reads that file back once the subprocess exits. A full brief with a nested outline doesn't fit cleanly in a response body, so it goes to a file instead.

Publishing isn't just a git push. Once an article clears the checklist, `publish_approved.py` writes the frontmatter, commits it to the site's repo, and only marks it done after confirming the URL actually returns 200. Two more things happen on the way out the door: `google_indexing.py` pings Google's Indexing API directly instead of waiting on a crawl, and `image_gen.py` asks fal.ai for a hero thumbnail matched to the article's topic, so nothing ships without an image already attached.

{% include figure.liquid loading="eager" path="assets/img/projects/seo-pipeline-thumbnail-example.png" title="An auto-generated thumbnail for a published article" class="img-fluid rounded z-depth-1" zoomable=true %}

### Approval, inverted

The pipeline didn't start with an opt-out review model. The first version had an Approve column in the tracking sheet, an article stayed unpublished until someone actively marked it good. About six weeks in I flipped that to a Rejected column instead: articles publish automatically after a six-hour review window unless someone flags one first. I also cut the schedule from daily to every other day at the same time. The actual bottleneck was never how fast the pipeline could produce a draft, it was how much of my own attention a review gate ahead of every single article demanded. Betting that most drafts clear the bar by default, and treating review as the exception instead of the gate, was a real changed direction, not a tuning knob.

The bet behind the whole pipeline, not just that one change, was that a content network chasing organic search traffic and an email list doesn't need every article to be exceptional. It needs enough of them, published on schedule, cheap enough per article that being wrong about a handful of keywords doesn't matter.

### The handoff

This pipeline generated new content for about two months, then went quiet for a few weeks. On April 6, 2026 the whole operation moved to a different system: an autonomous Discord bot I've written about separately, which reads its own operating rules from markdown instead of hardcoded Python and gates every publish behind an explicit human approval. I won't retell that system's architecture here, it has its own case study. But its output belongs to this network's story just as much as the pipeline's does, and it kept the network growing for four more months after this pipeline stopped, past the point where this case study would otherwise end.

### What shipped after the handoff

The successor system didn't just keep the content cadence going. Mid-May 2026 brought a coordinated rollout: every one of the thirteen sites got its own themed calculator tool, matched to its industry.

<div class="table-responsive">
  <table class="table table-sm table-bordered">
    <thead>
      <tr><th>Site</th><th>Tool</th></tr>
    </thead>
    <tbody>
      <tr><td>academicaitrends.com</td><td>GPA calculator</td></tr>
      <tr><td>creatoraidaily.com</td><td>Creator earnings estimator</td></tr>
      <tr><td>ecomaidaily.com</td><td>Reseller fee calculator</td></tr>
      <tr><td>fashionaidaily.com</td><td>Clothing size converter</td></tr>
      <tr><td>financeaidaily.com</td><td>Compound interest calculator</td></tr>
      <tr><td>fitnessaitrends.com</td><td>TDEE and macro calculator</td></tr>
      <tr><td>focusaiguide.com</td><td>Pomodoro timer</td></tr>
      <tr><td>foodaidaily.com</td><td>Recipe calculator</td></tr>
      <tr><td>freelanceaidaily.com</td><td>Hourly rate calculator</td></tr>
      <tr><td>healthaidaily.com</td><td>Body composition calculator</td></tr>
      <tr><td>hiringaiguide.com</td><td>Job offer calculator</td></tr>
      <tr><td>housingaitrends.com</td><td>Rent vs. buy calculator</td></tr>
      <tr><td>travelaidaily.com</td><td>Trip budget calculator</td></tr>
    </tbody>
  </table>
</div>

Right behind the tools came a coordinated SEO pass across all thirteen sites in the same two-week window: tool schema, FAQ blocks, AI-overview answers, related-article links, sitemap and canonical URL fixes. In June, publishing picked up a "citability" rule: every article needs at least four distinct types of source, and Reddit citations follow their own stricter rules, a direct response to how these articles were actually getting cited (or not) once they were live. Two real bugs shipped and got caught in the same window: the reseller fee calculator's ROI figure had a denominator that excluded platform fees, understating the real cost, and the clothing size converter was off by one on IT band sizes and Japanese shoe sizes. Both got fixed within days. In July, a mismatch in where the article-generation prompt put its thumbnail suggestion caused four articles, across education, e-commerce, content creation, and healthcare, to publish with no image at all before the extraction logic got patched. Analytics and an email capture form went out network-wide on July 28, the point where the network started actually measuring the audience it had spent five months building.

### The insights API

One of the tools, financeaidaily's compound interest calculator, got something none of the others did: a live AI-generated insight underneath the results, a separate FastAPI service that reads the visitor's current numbers and writes two plain-English sentences about them, "$130,000 invested yields $300,851 after 20 years, compound interest accounts for $170,851 of that, 131% return on contributions," that kind of thing. Numbers only reach the model. No free text from the visitor is ever interpolated into anything, so there's no prompt-injection surface to close in the first place.

The interesting parts are the defense-in-depth details that don't show up in a one-line description. CORS blocks a browser from calling the API cross-origin, but it does nothing to stop a direct POST from curl or a bot with a spoofed Origin header, so there's a second server-side check on every write that rejects anything not from the site's own origin, on top of per-IP rate limiting. A pydantic validator rejects any input where the math doesn't actually imply compound growth, principal and contribution both zero, or a final balance lower than what was put in, before the request ever reaches the subprocess call, which matters because every subprocess call is a real, billed API request. On the frontend, recalculating on every slider drag would fire a request per pixel, so it's debounced 800ms, and any in-flight request gets aborted the instant a newer one starts so a stale answer can't land after a fresher one already has.

{% include figure.liquid loading="eager" path="assets/img/projects/seo-pipeline-calculator.png" title="The compound interest calculator the insights API plugs into" class="img-fluid rounded z-depth-1" zoomable=true %}

It went live, then I paused it a few hours later, not because anything broke. The API shares its host with another service, and at the time both ran under the same OAuth session, meaning a compromise of either one exposes the credential the other depends on, and Anthropic spend from the two workloads shows up mixed together in one place instead of two budgets I could cap separately. Neither of those is urgent for a single-tenant setup, but neither is something I wanted running publicly while it sat unresolved. Extending the same live-insight approach to the other twelve calculators got discussed and dropped, the latency and cost of a real subprocess call per visitor wasn't worth it for tools this small. The rent-vs-buy calculator ended up with something in the same spirit anyway, a plain-language verdict, buying wins by this much, or renting does, computed from a few if/else branches with no model call at all. That wasn't a network-wide substitute, it's specific to that one tool's shape. The other eleven calculators are plain, no narrative layer of any kind.

### Where this actually stands

The network has produced 364 published articles across the thirteen sites as of early August 2026. Three of the sixteen industries originally configured for the pipeline, legal, media and entertainment, and small business, never produced a single article and never got a site. In the most recent tracked week, the network logged 6,307 search impressions and 58 clicks, up 24% and 45% week over week. That traffic isn't even: healthaidaily.com and fitnessaitrends.com carried most of it, 1,682 and 1,282 impressions with 17 clicks each, while hiringaiguide.com logged 420 impressions and zero clicks in the same week. I'd rather show that spread plainly than average it into one flattering number.

### Where this is honest, not clean

The article count at the April handoff doesn't reconcile cleanly between the two systems, the original pipeline's own records show 183, the successor's initial tracking showed 157. Neither number is wrong exactly, they're just counted differently, and nobody wrote down a reconciliation at the time. Running content generation through a CLI subprocess instead of a direct API call costs real latency too, eight to eighteen seconds per call, most of it CLI startup rather than the model thinking. That's a fine tradeoff for an article generated overnight. It's a worse one for a calculator someone's actively watching, and if I rebuilt the insights API today I'd swap the subprocess for a direct API call and take the corresponding hit of provisioning a dedicated key. None of that is something I noticed after the fact. It's the honest state of a system that's been growing for seven months, not a system I dressed up to look finished.
