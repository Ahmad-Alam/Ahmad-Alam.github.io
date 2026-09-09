---
layout: page
title: Building a Real-Time Voice Agent
description: A production-style voice pipeline with a swappable local/cloud stack and a live per-stage latency inspector, extended to drive a real phone call and, separately, a webpage by voice
img: assets/img/projects/voice-pipeline-inspector.png
importance: 3
category: work
---

Most voice agent demos hide the parts that actually matter: how much latency you're really carrying between the user going silent and the bot answering, and how often the model quietly fails to call a tool correctly. I wanted to see both numbers for myself, not read about them in a framework's marketing page. So I built two versions of the same voice agent on two different frameworks, picked the one that fit, built a real one on top of it with a live inspector so I could watch every stage's latency in real time, then pushed it in two directions: onto a real phone call, and onto a version that can read and drive a webpage by voice using a second LLM.

The repo isn't public, so here's the layout of the files this case study refers to:

```
voice-agent/
├── framework-comparison/
│   ├── pipecat-bot.py            # bare Pipecat pipeline, laptop mic/speaker
│   ├── livekit-agent.py          # same pipeline, LiveKit framework
│   └── comparison.ipynb          # side-by-side architecture notes
├── e2e-agent/
│   ├── server.py                 # FastAPI: WebRTC signaling, events + logs sockets
│   ├── session.py                # pipeline build, local/cloud backend swap, InspectorObserver
│   ├── kokoro_tts.py             # local Kokoro TTS, streamed, shared across sessions
│   ├── weather.py                # the get_weather tool (Open-Meteo)
│   └── static/                   # the live inspector UI
├── ui-worker-agent/
│   ├── ui_session.py             # voice worker + a second, screen-reading worker
│   └── static/                   # the controllable page + inspector
└── telephony-agent/
    ├── bot.py                    # same pipeline, Twilio transport
    ├── server.py                 # TwiML endpoint, media socket, softphone routes
    └── softphone.html            # browser softphone, bypasses trial-account PSTN limits
```

### Picking a framework by building both

Pipecat and LiveKit both promise the same thing: wire together VAD, STT, an LLM, and TTS into a live voice pipeline. Reading the docs doesn't tell you which one to trust with a real system, so I built the identical bot twice, same providers (Groq for STT and the LLM, a local Kokoro model for TTS) on both, and put them side by side in a browser app with a shared event inspector and a feature matrix.

The real difference sat below the feature list, in how each framework wants you to think about a call. Pipecat models a call as a pipeline of frame processors you assemble yourself, full control, more code. LiveKit hands you an Agent/AgentSession abstraction and a managed SFU, less code, less control. I wrote it up plainly in a comparison notebook: Pipecat optimizes for the pipeline, LiveKit optimizes for the deployment. I picked Pipecat, because I wanted to see the actual frame-by-frame mechanics of a voice turn, not have them abstracted away.

### The pipeline, and the latency budget

The core agent runs a straightforward chain: mic audio through a WebRTC transport, into Silero VAD for turn-taking, speech-to-text, an LLM with two tools, a live weather lookup and a way to end the call, text-to-speech, and back out over the same WebRTC connection. What's not straightforward is that every stage in that chain has a free, local option and a faster, paid one, and the whole thing swaps between them off two environment variables, no pipeline code changes. Set a Deepgram key and STT goes from Groq's batch Whisper to Deepgram's streaming STT. Set a Cartesia key and TTS goes from a local Kokoro model to Cartesia's streaming Sonic voice. Leave both unset and it falls back to the free stack automatically.

I built an observer that taps every frame moving through the pipeline, deduplicates by frame ID since some frames pass through multiple stages, and throttles high-volume audio frames to a few updates a second so the UI doesn't drown in events. It measures the number that actually matters for a voice agent: voice-to-voice latency, the gap between the user going silent and the bot's audio starting, not total round-trip time, not time-to-first-token. On the cloud stack that lands around 0.7 to 1.0 seconds warm. On the all-local stack it's closer to 2.4 seconds. The industry bar for this is p50 under 500ms, p95 under 800ms. Neither of my stacks clears that on a cold or even a fully warm local run, and I'd rather say that plainly than round it up. The cloud stack gets close. The free stack is free for a reason.

<div class="table-responsive">
<table class="table table-sm table-bordered">
<thead>
<tr><th>Stage</th><th>Free / local</th><th>Fast / cloud</th></tr>
</thead>
<tbody>
<tr><td>STT</td><td>Groq Whisper (batch, ~1.2s)</td><td>Deepgram streaming (~0.2s)</td></tr>
<tr><td>LLM</td><td colspan="2">Groq Llama 4 Scout, same on both stacks</td></tr>
<tr><td>TTS</td><td>Kokoro-82M, local, streamed (~0.9s)</td><td>Cartesia Sonic, streaming (~0.2s TTFB)</td></tr>
<tr><td>Voice-to-voice, warm</td><td>~2.4s</td><td>~0.7-1.0s</td></tr>
</tbody>
</table>
</div>

{% include figure.liquid loading="eager" path="assets/img/projects/voice-pipeline-inspector.png" title="The live inspector: pipeline stages lighting up as frames flow through them, with per-stage latency tiles" class="img-fluid rounded z-depth-1" zoomable=true %}

Kokoro was the one piece with no managed alternative worth using, so it got the most engineering attention: a shared pipeline cached at the class level so every session on the box reuses one loaded model instead of reloading it per call, pre-warmed in a background thread at server startup so the first real user isn't the one who eats the cold-start cost, and streamed chunk by chunk so the latency number reflects time to the first audio chunk, not time to the whole synthesized sentence.

The other real bug lived in tool calling. The first LLM I tried, a smaller fast model, intermittently emitted malformed function calls, the kind that fail silently from the user's side and just look like the bot ignoring them. I traced it to the model, not the code, swapped to a larger one and dropped the sampling temperature to make tool-call formatting more consistent. Small fix, but it's the kind of bug that's invisible until you're specifically watching for it, which is most of the reason I built the inspector in the first place.

### Extending it: onto a real phone call

To find out whether the transport-swap design actually meant anything, I pointed the same pipeline at a phone line. The only change from the browser version is the transport: swap the WebRTC transport for a WebSocket one wired to Twilio's media stream format, and answer Twilio's connection with the right TwiML. Everything upstream of the transport, VAD, STT, the LLM, tools, TTS, didn't change at all, which is the whole point of building on frame processors instead of a monolithic call loop.

Getting a real call working hit a real constraint: a Twilio trial account can't place outbound calls to every country, mine included. Rather than treat that as a dead end, I added a browser softphone as a second way in, same bot, reached over WebRTC instead of the PSTN, no phone number, no trial restriction, no cost. I also ended up self-hosting Twilio's JS SDK, because their CDN is geo-blocked in some regions and I wasn't going to let a CDN outage decide whether the demo worked.

### Extending it again: a voice agent that drives a webpage

The other direction I pushed it was a version that can read a webpage out loud, answer questions about it, and act on it, scroll to a section, highlight a paragraph, fill in a form, all by voice. That needs two separate reasoning contexts: the voice LLM, which owns the conversation and never sees the page's structure, and a second LLM that owns the page and never sees the chat history. They talk to each other over a small internal job queue, the voice worker dispatches a request, the screen worker answers it and can emit UI commands back to the browser.

{% include figure.liquid loading="eager" path="assets/img/projects/voice-pipeline-uiworker.png" title="The webpage-driving demo: the voice agent reads the page, and a second LLM owns everything it can scroll, highlight, or fill in" class="img-fluid rounded z-depth-1" zoomable=true %}

The browser sends the second LLM a snapshot of the page as an accessibility tree, every element tagged with a short reference ID, and the model sends back commands, scroll to this ref, highlight that one, fill this input, resolved against the last snapshot the browser has.

The first version of that tree was flat, headings, paragraphs, and form fields all as siblings with no structure between them. The model kept confusing them, filling text into a paragraph instead of the input field next to it, because nothing in the data told it which refs belonged to a form versus body text. The model was doing exactly what a flat, ambiguous input told it to do. I fixed it by actually nesting form fields under a dedicated form node in the tree instead of leaving them flat, tightened the prompt to say explicitly which roles are fillable, and swapped in a larger model for that worker specifically, since the smaller one kept making the same mistake even with the better data. Shipped the demo one evening, had it reliably filling the wrong element by the next morning, had the real fix in less than a day.

It's demo-grade, and I'd rather say so than let the screenshot imply otherwise. Reference IDs get reassigned every time the page snapshot rebuilds, so a command issued right as the page changes can target the wrong element. The browser resends a fresh snapshot every two seconds to keep that window small, which helps but doesn't close it. A production version of this needs stable element identity instead of a rebuilt list of IDs each time.

### Where this stands

This was a dense two-week build, June 19 through July 3, not a long-running system like some of my other projects, and I'd rather be upfront about that than imply otherwise. What's there is real. A working dual-stack pipeline with measured, honest latency numbers. A phone-reachable version that handles a real carrier's real trial restrictions. A webpage-driving demo with two independent LLM contexts and a documented, fixed failure mode. A from-scratch comparison of two frameworks that actually justifies the one I picked instead of just asserting it. I also wrote up a separate piece of research grounded in this same codebase, on whether a voice agent can interrupt the user mid-sentence the way a human would, and the honest finding there was that Pipecat doesn't currently have a verified working example of that. Worth knowing before you assume it's a solved problem.

I also built a five-module interactive walkthrough of how the core agent works, frame by frame, mostly because writing the explanation forced me to understand it more precisely than skimming my own code did.
