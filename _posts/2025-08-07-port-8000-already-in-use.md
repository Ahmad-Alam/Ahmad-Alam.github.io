---
layout: post
title: "port 8000 is already in use"
date: 2025-08-07
description: What happens when you stack multiple processes that each assume they own port 8000 — and how to think about shared resources when orchestrating agents.
keywords: multi-process orchestration, port binding conflict, subprocess management, python process coordination, shared resource management, LLM agent orchestration
tags: python engineering systems
categories: engineering
related_posts: true
---

I was building something that involved spawning multiple processes, each of which needed to start a server. The first one would start fine. The second would fail with `address already in use`. The third would either fail or land on some random port the OS assigned it.

Stupid problem. Five-minute fix once I understood it. I spent a while not understanding it, which is the part worth writing about.

## what I thought was happening

My first instinct was zombie processes — the previous one hadn't shut down cleanly, port still bound. So I added cleanup logic: kill anything holding the target port before starting. That helped but didn't fix it.

The actual problem was more embarrassing. I'd written each process independently without thinking about the fact that they share an environment. Each one would read its own config, see port 8000, and try to bind to it. There was no coordination. Why would there be? Each component was written in isolation, where "port 8000" was just a config value, not a claim on a shared resource.

## the part that generalizes

When you're orchestrating multiple processes, some things that feel like per-process config are actually global state. Port bindings are the obvious one, but also file paths, temp directories, lock files, log locations. Every component author makes assumptions about what they own exclusively. Stack enough components together and those assumptions start colliding.

I ended up with a simple port allocation scheme — base port, increment per process, kill any existing holder before binding. Fine. But the thing I actually took from this was the habit of sitting down before wiring up a new system and asking: what are these components going to fight over that nobody has thought about yet?

## the fix

```python
def kill_port(port: int):
    result = subprocess.run(
        ["lsof", "-ti", f":{port}"],
        capture_output=True, text=True
    )
    if result.stdout.strip():
        for pid in result.stdout.strip().split("\n"):
            subprocess.run(["kill", "-9", pid])
```

Called before every server start. Annoying that it's necessary. Works fine.
