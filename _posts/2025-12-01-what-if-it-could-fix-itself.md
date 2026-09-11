---
layout: post
title: what if it could fix itself
date: 2025-12-01
description: Building a fixer agent that reads failure context and repairs broken output — and why it ended up more capable than the original pass.
keywords: self-healing pipeline, LLM fixer agent, failure recovery, multi-agent systems, autonomous debugging, AI pipeline, Claude agent, structured error handling
tags: engineering ai systems
categories: engineering
related_posts: true
---

I had a build pipeline that produced broken output sometimes. Not always — maybe 30-40% of runs. The first version of my fix was: surface the error, ask the user to intervene, let them sort it out manually.

That worked. It also felt wrong.

The thing that felt wrong wasn't the human involvement itself — sometimes that's right. It was that the intervention was completely unstructured. The user would look at an error, make a guess, try again. The pipeline treated this as a fresh start. All the context from the previous run — what it tried, what failed, what the error actually said — was either gone or buried somewhere. The user was doing error handling without any of the state that would make error handling useful.

## treating failure as input

The shift that helped was pretty simple as a concept: failure is just another type of input. Instead of stopping when the output was broken, the pipeline could read the error, read the broken output, and try to produce a repaired version with that additional context.

Retry logic does this at a basic level. What I built does it at a higher level — the retry isn't "run the same thing again," it's "here's what went wrong last time, here's what broken output looks like, now try to fix it." The fixer doesn't have to be smarter than the original process to do this well. It just knows it's repairing something rather than building from scratch, which changes what it produces.

Getting this to actually work required a few things. Failures needed to be structured — a raw stack trace you can't really do anything with; a caught exception with type, message, and relevant state is something you can feed back into a prompt. The fixer also needed a real exit condition, because "try until it works" is an infinite loop unless you define what "works" means. I ended up with a completion gate: run tests, compare against a spec, count consecutive failures, give up after N attempts and surface to a human.

The harder part was the trust question. There's an instinct to add human review after every fix attempt. I get why — you want to catch it before it compounds. But if you review after every single attempt, the user is still the error handler, just one step downstream. At some point you have to let it run.

## the part I didn't expect

Once fix mode was working, I started leaving the pipeline overnight and checking results in the morning. More things worked than I'd expected. The first-pass failure rate didn't change — still around 30-40%. But after the fixer ran, it was much lower.

This surprised me. I'd thought of the fixer as a fallback, something that catches the easy cases the main pipeline misses. It turned out to be better at certain tasks than the original pass — not because it's more capable, but because it has richer context. It knows what didn't work. That's actually a lot of information.
