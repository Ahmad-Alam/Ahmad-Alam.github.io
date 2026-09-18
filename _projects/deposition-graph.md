---
layout: page
title: Legal Deposition Knowledge Graph Service
description: A knowledge graph service that turns a deposition transcript into typed nodes and relationships across a graph database, an encrypted document store, and a vector index, so contradictions and admissions are queryable instead of buried in a thousand-page transcript
img: assets/img/projects/deposition-graph-pipeline.svg
importance: 6
category: work
---

Lawyers prepping for trial reread depositions that run a thousand pages or more, hunting for the one contradiction that breaks a case. I built a service that reads a deposition once, pulls out everything worth remembering, and puts it in a graph that can be queried instead of read cover to cover again.

Given a transcript, it produces a set of typed nodes, entities, admissions, contradictions, timeline events, exhibits, connected by typed relationships (who said what, what supports what, what contradicts what), stored across a graph database, a document store, and a vector index.

```
deposition-graph-service/
├── main.py                       # FastAPI entrypoint, /process_deposition and /delete_deposition
├── data_extractor.py             # stage 1: deterministic parsing from structured deposition JSON
├── llm_node_extractor.py         # stage 2: LLM extraction of people, places, organizations, medications
├── llm_relationship_extractor.py # stage 2: heuristic + LLM relationship inference between nodes
├── neo4j_client.py               # bulk graph writes, retry-safe, case/deposition scoped
├── pinecone_client.py            # embeddings for semantic search, deposition-scoped deletion
└── deposition_api_client.py      # authenticated writes into MongoDB
```

{% include figure.liquid loading="eager" path="assets/img/projects/deposition-graph-pipeline.svg" title="Transcript in, two extraction stages, a UUID triad generated per node, then three databases written in sync" class="img-fluid rounded z-depth-1" zoomable=true %}

## The schema does the legal reasoning

A deposition isn't just text, it's testimony with legal weight attached. The graph has six node types built around how lawyers actually use a transcript: entities (people, places, organizations, medications), topics, admissions, contradictions, timeline events, and exhibits. Fifteen typed relationships connect them. An admission is `MADE_BY` a deponent and sits `REGARDING` a topic. A contradiction attaches back to the person who made it. A timeline event `INVOLVES` a person and `HAPPENED_BEFORE` the next one in sequence.

That specificity is the point. A generic "mentions" edge tells you two things appeared near each other. A `CONTRADICTS_SELF` edge with a page and line number tells a lawyer exactly where to point during cross-examination.

{% include figure.liquid loading="eager" path="assets/img/projects/deposition-graph-schema.svg" title="Six node types, fifteen typed relationships, scoped to case and deposition" class="img-fluid rounded z-depth-1" zoomable=true %}

## Two passes over the same transcript

Extraction runs in two stages. The first is deterministic. A deposition arrives from the backend with a lot of structure already: admissions, contradictions, and timeline events as JSON arrays, topics buried inside a Mermaid flowchart. Parsing that costs nothing and gets it exactly right. It produces the bulk of the graph, somewhere around 200 to 300 nodes per deposition, before a single model call happens.

The second stage is where an LLM earns its cost. It reads the narrative summary and pulls out entities the structured data doesn't name explicitly, a medication referenced once, an organization that shows up in a single sentence, and matches each one to the topic it's most relevant to. It also infers relationships the structured data can't hand over directly, like who works where or which exhibit supports which admission. That second pass adds another 70 to 150 nodes and relationships, capped at five concurrent model calls so a long transcript doesn't spike cost or fall over on rate limits.

Splitting it this way keeps the expensive step small and the cheap step doing most of the work.

## Keeping three databases honest

The graph lives in Neo4j. The underlying document content lives encrypted in MongoDB. The semantic search index lives in Pinecone. Three systems, one deposition, and every node needs to exist correctly in all three or the whole thing stops being trustworthy.

The fix is to generate three IDs for every node before writing anywhere:

```json
{
  "kgNodeId": "c1a1e2b4-9f3a-4d21-8b6e-2a7c5f9d1e02",
  "neo4jNodeId": "7e2f9a11-4c88-4a3d-9f21-6b5e0d8c3a19",
  "pineconeId": "a93b7c40-1d5e-4f2a-8c9b-3e7f1a2d4c60",
  "nodeType": "ADMISSION",
  "question": "Did you review the pricing report before it was sent to corporate?",
  "answer": "Yes, I reviewed it the morning it went out.",
  "reason": "Establishes the deponent had direct knowledge before distribution.",
  "page": 142,
  "line": 8,
  "caseId": "case-a",
  "depoId": "depo-d"
}
```

All three IDs get written to all three stores. A Neo4j node already carries the ID needed to look up its document in MongoDB or find its vector in Pinecone. There's no mapping table to maintain and no drift to reconcile later, because the sync happens once, at creation, instead of after the fact.

Writes to Neo4j go through APOC's merge functions in batches of a hundred, labeled dynamically by case and deposition so a delete or a scoped query never touches another case's data, with three retries on anything transient. Writes to MongoDB are atomic per batch too: a hundred nodes succeed together or fail together, authenticated with a time-based one-time code instead of a static credential.

## The tradeoff I'd flag first

That last part is also the weakest link. The MongoDB write depends on a live, time-synced handshake with an external API. If that service is down or the clock drifts, an entire batch of nodes fails to persist there, even though the same nodes already landed fine in Neo4j and Pinecone. The graph and the vector index would say a node exists and MongoDB wouldn't have it yet. Nothing catches that gap automatically right now. It would need a reconciliation pass or a retry queue, and I didn't build one. Across five test depositions it never came up. At real volume it would.

## Where this actually stands

Across five real depositions, this produces roughly 300 to 400 graph nodes and 200 to 300 relationships per transcript, matched by a similar number of vectors for semantic search, in under two minutes end to end. That's enough to ask the graph what a witness admitted about a given topic and get back a sourced, page-referenced answer instead of a search result I'd still have to go verify myself.

This has only run against a handful of test transcripts so far. But the shape of it, typed legal reasoning built into the schema, cheap extraction doing most of the work and expensive extraction doing the rest, a consistency scheme that skips the need for a reconciliation job in the common case, is the right foundation to build a real one on.
