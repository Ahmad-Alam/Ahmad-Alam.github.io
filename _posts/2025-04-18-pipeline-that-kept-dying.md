---
layout: post
title: the pipeline that kept dying at 3am
date: 2025-04-18
description: How checkpointing and semaphore-controlled concurrency turned a brittle LLM batch pipeline into something that actually finishes overnight.
keywords: python asyncio, async pipeline, checkpointing, semaphore rate limiting, LLM batch processing, asyncio.gather, exponential backoff, pipeline engineering
tags: python async pipelines engineering
categories: engineering
related_posts: true
---

I had a pipeline that needed to process a large corpus of documents — LLM calls per document, some database writes, a few API lookups. The kind of job you kick off and leave running.

It kept dying.

Not crashing. Dying quietly. Somewhere around the 60-70% mark it would just stop. Sometimes a timeout, sometimes a rate limit that wasn't being caught. Once, for reasons I still don't fully understand, it hung. I'd come back in the morning to a frozen terminal and nothing useful in the logs.

Retry logic helped. The real problem was that every time it died, I started from zero. Three hours of compute and API credits, gone.

## checkpointing

The first fix was checkpointing. After each successfully processed document, write its ID to a manifest file. On restart, skip anything already in the manifest. About ten lines of code, and it immediately changed the failure mode from "start over" to "pick up where you left off."

I hadn't thought to do this earlier because I was thinking about the job as a transaction — either it all works or you redo it. That model makes sense when runs are cheap and fast. When a single run costs hours, you need to treat each successful step as something worth keeping.

## concurrency depth

Checkpointing fixed the restarts. The pipeline still felt slow and I was hitting rate limits in a weird pattern — bursts of errors, then silence, then more errors.

I'd implemented concurrency by throwing everything at `asyncio.gather` at once. All N documents in parallel, all making API calls simultaneously. The rate limiter saw a spike, throttled hard, and half the tasks failed.

The fix was a semaphore to cap concurrent operations:

```python
semaphore = asyncio.Semaphore(10)

async def process_with_limit(doc):
    async with semaphore:
        return await process_document(doc)
```

Combined with exponential backoff on rate limit errors, the pipeline went from constantly fighting the API to just running. The gains from async aren't about parallelizing everything — they're about parallelizing the right things at the right depth. Running 10 things at once and letting the rest queue turned out to be much faster than 200 things at once and half of them failing.

The pipeline runs overnight now. I mostly don't think about it, which took a while to get to.
