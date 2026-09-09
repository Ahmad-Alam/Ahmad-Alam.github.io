---
layout: page
title: Autonomous Content Operation Bot
description: A self-scheduling content system that researches, drafts, and quality-scores blog posts and videos across 13 niches on its own, and never publishes anything without an explicit human approval
importance: 1
category: work
---

I built this to run without me. Not "make a bot that writes posts," which is easy, but "make something I can walk away from for months, that generates real content on a schedule and only ever asks me for one thing: permission to actually publish it."

It runs 24/7, controlled through Discord. On a fixed weekly schedule it researches, drafts, and quality-scores blog articles and short explainer videos across a set of niche content sites and channels, entirely on its own. Each site targets one industry's corner of the AI-tools conversation, aimed at organic search traffic and an email list, not a one-off content dump. It never posts anything without me replying "approve" first. Those two facts together, autonomous generation and a hard human gate on publishing, are the actual shape of the project, and most of the interesting engineering sits in the gap between them.

The repo isn't public, so here's the layout of the files this case study actually refers to:

```
content-ops-bot/
├── bot.py                          # thin Discord shell, no logic
├── CLAUDE.md                       # core instructions, bot cannot edit this one
├── strategy.md                     # products, industries, priorities (bot can self-update)
├── schedule.md                     # what runs when, catch-up protocol (bot can self-update)
├── quality_criteria.md             # the ship/revise/scrap checklist (bot can self-update)
├── cron_times.md                   # the ~30 daily trigger times
├── config/
│   ├── channels.md                 # per-industry YouTube channel POV and voice
│   ├── publishing.md               # blog frontmatter, repo mapping, deploy verification
│   ├── video_publishing.md         # video upload and rendering workflow
│   └── explainer_spec.md           # the 5 hard rules for video format
├── prompts/
│   ├── blog/                       # phased blog generation prompts
│   ├── video/                      # phased video generation prompts
│   └── reddit/                     # Reddit comment drafting prompt
├── video-kit/explainer/scripts/
│   └── gen-audio.mts               # TTS chunking, site of the decimal bug
└── state/                          # daily metrics snapshots, session persistence
```

### How it thinks

There's zero intelligence in the Python. `bot.py` is a thin Discord shell that passes the full context, time, state, history, incoming message, to Claude and does whatever Claude decides. Every actual decision, what to generate, whether a draft is good enough to ship, when to skip a day, lives in a set of markdown files the model reads fresh each time it runs. Three of those files, the strategy, the schedule, and the quality criteria, are ones the bot can rewrite on its own, git-committed each time. One file, the core instructions, it can't touch. That split, self-editable operating rules on top of a fixed core, is the actual permission model here. There's no code enforcing it. It's a rule the model has followed so far, not a lock that would stop it if it didn't.

This wasn't the first version of this architecture, and it's worth saying so. The content pipeline used to be two separate coded Python systems, one for research and drafting, one for video rendering, each with its own hardcoded control flow. I replaced both with this bot because every new requirement meant a code change, and the actual bottleneck was never the model's writing ability, it was how much of the decision-making I'd locked into Python instead of leaving it somewhere I could edit in two minutes.

Every generation phase, research, drafting, analytics, Reddit scanning, runs in its own spawned subagent rather than in the main conversation. That's a deliberate rule, not an accident: heavy work happens in a disposable subagent, and only the result comes back to the main session, which is what lets a persistent Discord bot stay coherent over months instead of drowning in its own context. The main session itself survives a machine restart by resuming a stored session ID, and falls back to starting fresh if that session's expired, so a server reboot costs nothing but a bit of conversational memory, not the system itself.

### What it produces, and how much

Content splits by weekday. Monday and Thursday, it generates blog articles across 13 niche AI-trend sites, one per industry, from healthcare to freelancing to fashion. Tuesday, Wednesday, and Friday, it generates short vertical videos for five of those same industries, each with its own YouTube channel and a distinct editorial voice defined per industry, the healthcare channel measured and cautious, the productivity channel openly contrarian about productivity culture itself. It also scans Reddit for threads relevant to each industry and drafts a reply in that industry's voice, capped at five drafts a day, for a human to review and post manually. It never posts to Reddit on its own either. Weekends, nothing runs. A cron job checks in roughly thirty times a day, but most of those checks do nothing. They exist so a run that gets cut off, more on that below, gets picked back up automatically instead of just disappearing.

### The quality gate

Every piece of content gets scored against a written checklist before it's allowed to ship. Blog posts need a real keyword target, an opinion section, no fabricated statistics. Videos need a hook in the first three seconds, a clear take, a cost cap on how many freshly generated clips they're allowed to use. Both have an explicit list of banned phrases, "game-changer," "in today's fast-paced world," "seamless," "cutting-edge," and a second list specifically banning phrases that perform honesty instead of being honest, "no BS," "let's be real," "here's what nobody tells you." A 7-or-above score ships, 4 to 6 gets revised and retried, anything lower gets scrapped and restarted from research. I wrote that checklist before I ever thought about how I wanted my own writing to sound, and it's funny how much overlap there ended up being.

### The part that requires a human

Generation and scoring are fully autonomous. Going live isn't. Nothing posts to a blog, YouTube, or Instagram without me replying to a review message in Discord that lists everything ready to go. For blog posts specifically, even after I approve, the bot still has to verify the article is actually live, checking the URL for an HTTP 200, before it's allowed to mark anything as published. A build that silently fails doesn't get to call itself done just because the code ran.

### Keeping it running

The operating rule I wrote for this system is blunt: never stop the pipeline. If something breaks mid-run, a bad API response, a malformed file, retry it three times before giving up, and if a draft is borderline, ship it anyway, since something posted beats nothing posted. The only thing allowed to actually halt a run is a real infrastructure failure, an invalid key, a dead service. Everything else gets logged and pushed through. That rule exists because the generation window runs against a rolling usage cap that can trip mid-run for reasons that have nothing to do with content quality, and a system that gives up the first time that happens would spend more time stalled than working. The catch-up checks I mentioned earlier are what actually resume a run once the cap resets, picking up whichever industry didn't finish instead of leaving a silent gap in the schedule.

### The bug I'm most annoyed I didn't catch sooner

The text-to-speech step for videos chunks a script into sentences before sending it to the voice model. The original chunker used a regex that matched sentences ending in a period, and it was quietly dropping whatever text came right before a decimal number, so a stat like "44.6%" would eat the sentence around it. Nothing crashed. Nothing errored. Videos just occasionally lost a piece of a sentence, and I only found it because I happened to read a transcript closely enough to notice something was missing. The fix was small, switch from matching sentence patterns to actually splitting on sentence boundaries, but finding a bug that never throws an error is its own kind of slow.

### Where this actually stands

Five months in, this is a working system, not a proof of concept. It's produced 364 published blog articles across the 13 sites so far. Search traffic is still early and I'd rather say that plainly than round it up: 6,307 impressions and 58 clicks in a recent 7-day window, up 24% and 45% week over week, respectively. YouTube sits around 14,000 total views across the five active channels, with just over 100 new views in the most recent week tracked. None of that is a growth story yet. It's a real, running, sustained pipeline with real if early numbers, and I'd rather show the actual state of it than dress it up.

### Where this is honest, not clean

The trust model here is real, not decorative. The rule that nothing auto-posts is written in plain language in a markdown file, not enforced by withheld credentials or a separate approval service. It has held, every time, so far. That's not the same as a guarantee, and I'd rather say that plainly than dress up a bet as a safeguard.
