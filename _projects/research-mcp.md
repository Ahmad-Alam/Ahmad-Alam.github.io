---
layout: page
title: Building a Research MCP Server for Claude Code
description: A stdio MCP server that gives Claude Code nine research tools and an offline, pre-built podcast transcript corpus, built around one rule, check the free local cache before paying for an API call
img: assets/img/projects/research-mcp.svg
importance: 5
category: work
---

Some research questions don't have good answers in a model's weights or on the first page of Google. "Is anyone actually paying for this?" "What do people hate about this tool?" Those live in Hacker News threads, subreddit comments, X replies, podcast episodes, app store reviews. Pulling that by hand is slow, and doing it through an LLM's own web tools re-pays the same API cost every time you ask something close to a question you already asked. So I built an MCP server that gives Claude Code a set of research tools, one per source, plus a local store the tools are told to check before spending anything.

The repo isn't public, so here's the layout of the files this case study refers to:

```
research-mcp/
├── src/
│   ├── index.ts              # 17 tool registrations, zod schemas, formats every adapter's output
│   ├── hn.ts                 # Algolia HN search + full thread read
│   ├── reddit.ts              # OAuth2 client-credentials, search + thread read
│   ├── x.ts                   # bearer-token search, last 7 days only
│   ├── youtube.ts             # unofficial transcript scrape, no API key
│   ├── youtube-search.ts      # Data API v3 search
│   ├── youtube-comments.ts    # Data API v3 comment threads
│   ├── web-search.ts          # Google search via Serper
│   ├── producthunt.ts         # GraphQL v2, topic-slug discovery
│   ├── app-reviews.ts         # iTunes RSS + Play scraper
│   ├── alternativeto.ts       # HTML scrape, no official API
│   └── storage.ts             # save_results, search_local, search_transcripts
├── ingest_channels.py         # offline pipeline: channels → transcripts → chunked corpus
├── build_search_index.py      # rebuilds the SQLite FTS5 index from the chunk files
├── channels.json              # the source channel list
└── data/
    ├── transcripts.db         # SQLite FTS5, 8,432 chunks, 45MB, committed to git
    └── transcript_chunk_*.md  # one file per ~400-word transcript chunk
```

### Check local first, always

`search_local` and `search_transcripts` are the two tools whose descriptions tell the model, in plain language, to try them before calling anything external. Two different things sit behind that one rule.

The small one: every tool that saves something writes both the raw JSON and a markdown synthesis to a flat `data/` directory, so a question answered once doesn't cost anything the second time someone asks something close to it.

The real investment is the offline transcript corpus. A separate Python pipeline pulls the upload history from 20 startup and solopreneurship-adjacent YouTube channels, chunks each transcript into roughly 400-word pieces, and compiles the result into a SQLite FTS5 index with BM25 ranking and Porter stemming, so "startup" matches "startups" for free. `search_transcripts` queries that index directly. No network call, no API key, no cost, whether it's the first question run against it or the thousandth.

### It didn't start this wide

The commit history is honest about how this grew. It started as "Phase 1: HN scraper with local caching," then added Reddit, then X, then YouTube transcripts, one phase at a time. Partway through, once it had stopped being just an HN tool, I renamed the whole repo to match what it had actually become. Web search started on Brave and got swapped to Serper once Google results tested better for the kinds of queries I was running. The last batch of source adapters, four of them in one push, came after I kept hitting the same gap in the same session: comments, Product Hunt, app reviews, an alternatives lookup.

Nine sources by the end, all following the same shape: one file, a handful of plain async functions, no shared HTTP client, no shared retry logic, each one reading its own credentials at call time. Adding a tenth source means writing one new file and one new tool registration. It doesn't mean touching the other nine.

The timeline is real too. The first four phases, the rename, and the initial web search tool all landed in two days in early March. The transcript ingestion pipeline and its 8,432-chunk corpus came a week later. Then the repo sat untouched for three months before the last four adapters went in during a single day in June. It grew in bursts when I actually needed a new source, not on any planned schedule.

<div class="table-responsive">
<table class="table table-sm table-bordered">
<thead>
<tr><th>Source</th><th>Auth</th><th>Notes</th></tr>
</thead>
<tbody>
<tr><td>Hacker News</td><td>none</td><td>Algolia's public search API</td></tr>
<tr><td>Reddit</td><td>client ID + secret</td><td>OAuth2, app-only, no private subreddits</td></tr>
<tr><td>X / Twitter</td><td>bearer token</td><td>last 7 days only, and the one adapter that can actually cost money</td></tr>
<tr><td>YouTube search + comments</td><td>API key</td><td>Data API v3, quota-limited</td></tr>
<tr><td>YouTube transcripts</td><td>none</td><td>unofficial scrape, the most fragile piece in the repo</td></tr>
<tr><td>Web search</td><td>Serper key</td><td>replaced Brave partway through</td></tr>
<tr><td>Product Hunt</td><td>token</td><td>topic-slug discovery only, no free-text search</td></tr>
<tr><td>App Store / Play</td><td>none</td><td>first search hit wins, no disambiguation</td></tr>
<tr><td>AlternativeTo</td><td>none</td><td>pure HTML scrape, fails soft with a note field instead of throwing</td></tr>
</tbody>
</table>
</div>

{% include figure.liquid loading="eager" path="assets/img/projects/research-mcp.svg" title="The model checks the local store and offline corpus first. Only a miss there reaches the nine external adapters." class="img-fluid rounded z-depth-1" zoomable=true %}

### Building the corpus

The ingest pipeline resolves each channel's upload playlist through the YouTube Data API, then fetches transcripts through an unofficial endpoint that scrapes the watch page for an internal API key and impersonates an Android client to pull captions. That path is rate-limited hard: an early run logged 21 consecutive `429` errors back to back before I added randomized 12 to 22 second delays between videos and a 60 second cooldown between channels, plus an immediate hard stop on any further `429` rather than pushing through it. The whole thing is resumable, checkpointed after every single video, so a Ctrl-C costs nothing.

Across the 20 channels, the pipeline discovered 1,000 candidate videos. 457 made it into the corpus as full transcript chunks. 538 got discarded under a 500-word floor meant to filter out YouTube Shorts, and 5 had no captions at all. Over half the discovered videos getting dropped is more than I'd expect from a Shorts filter alone, and I don't have a confirmed reason for it. I'd rather say that plainly than guess at a cause for a public case study.

### Where it stands

2,115 lines of TypeScript, 17 tools across 9 sources, in 15 commits. The offline half of it is 8,432 transcript chunks from 457 episodes across 20 channels, compiled into a 45MB SQLite index that answers a query with zero network calls, on the first run or the thousandth. Ask it something today, ask something close to it a year from now, and that half of the answer is still sitting there, free and instant, no API key required.
