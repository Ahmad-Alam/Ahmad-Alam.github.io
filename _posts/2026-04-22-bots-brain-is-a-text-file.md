---
layout: post
title: my bot's brain is a text file
date: 2026-04-22
description: How moving behavior into markdown files the LLM reads — instead of hardcoding it in Python — changed the iteration speed of a Discord bot from deploys to text edits.
keywords: LLM bot architecture, markdown as config, self-updating AI bot, autonomous bot, Claude API, behavior as data, Discord bot Python, AI configuration pattern
tags: python ai engineering architecture
categories: engineering
related_posts: true
---

I built a Discord bot. The Python wrapper is about 200 lines. It connects to Discord, formats incoming messages with some context, passes them to an LLM, posts the response back. That is genuinely all the Python does.

The behavior — what the bot does when it gets a message, when it runs on a schedule, how it decides what to prioritize, what it considers done — lives in a set of markdown files. The model reads them on each run and figures out what to do.

## what I used to do instead

The more common approach, I think, is to write behavior in code and use prompts for the LLM-shaped parts. A prompt handles classification, a conditional routes based on the result, another prompt does the work. Control flow in Python, intelligence in the model. Makes sense structurally.

The problem is that changing behavior requires changing code. If the bot should respond differently to a certain type of message, that's a code change. If the schedule needs updating, that's a scheduler change. If the definition of "done" evolves, that's a prompt buried in a function somewhere. Every behavioral iteration touched code, which meant PRs, reviews, deploys — for changes that should have taken five minutes.

## config that updates itself

The switch was moving behavior into files the model reads. Strategy, schedule, quality criteria, task priorities — all markdown. The model reads them at the start of each run and uses them as its operating instructions.

The difference from a long system prompt is that the bot can update these files. If the strategy shifts, the bot edits the strategy file and commits the change. The git history becomes a log of how the bot's behavior has evolved, including changes it made to itself. The core instructions — the things that define what it fundamentally is — live in a file it can't touch.

Anyone who can edit a markdown file can change how the bot works. The model can change how it works within the limits you set. Deploys are not involved.

## where it breaks down

Some things that look like policy are actually logic. "Send the report at 10am" is policy. "Convert that to the right timezone for each recipient" is logic and belongs in code. Drawing that line requires some practice and I've gotten it wrong a few times.

There's also a real question about trust. A bot that can edit its own config can, in principle, drift in ways you don't want. The answer I've landed on is: carefully scope which files are writable, review the git history occasionally, and keep the core instructions immutable. That's been good enough in practice.

## why I keep doing it this way

The iteration speed is just different. Something isn't working, I open a file, change some text, the bot reads it on the next run. No deploy, no restart. I've changed something in two minutes that would have taken an hour through the old cycle.

The bot has been running continuously for a few months. The strategy file has been updated dozens of times — by me, by my team, a few times by the bot itself. The Python is almost unchanged. The behavior has changed a lot. That feels like the right distribution.
