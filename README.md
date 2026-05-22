# Backend Engineer — Live Coding Exercise

Welcome, and thanks for taking the time to do this with us. This document is everything you need to know about the session.

## Overview

You'll have **60 minutes** total with us on a screenshare call, with roughly **45 minutes of build time**. The exercise resembles the kind of work we do at Neutral Farming.

**This is an AI-assisted exercise.** Use whatever tools you normally use to do your job — Cursor, Claude Code, Copilot, Codex, ChatGPT, whatever. We expect it. We're not testing whether you can write code from memory; we're testing how you work.

## The problem

You're building part of an ingestion pipeline for sensor data from a third-party irrigation provider.

Build a small HTTP service with two endpoints:

### `POST /readings`

Accepts JSON sensor readings from the provider. Each reading looks like:

```json
{
  "sensor_id": "sensor-a12",
  "field_id": "field-007",
  "timestamp": "2026-05-22T14:32:11Z",
  "reading_type": "soil_moisture",
  "value": 38.4
}
```

The provider is flaky. In production you should expect:

- **Duplicate events** — the same `(sensor_id, timestamp)` may arrive more than once
- **Out-of-order events** — readings may arrive after newer ones from the same sensor
- **Malformed payloads** — missing fields, wrong types, occasional garbage

Persist valid readings to Postgres.

### `GET /fields/{field_id}/latest`

Returns the latest reading per sensor for a given field. Response shape is up to you — pick something a frontend team would be happy to consume.

## What we provide

- A `docker-compose.yml` with a Postgres instance ready to go
- A `go.mod` / `pyproject.toml` starter (use whichever language you prefer — both are fine for this role)
- A sample payload file: `samples/readings.json`
- This README

## What we're looking for

We care more about **how you work** than how much you finish. Specifically:

- How you scope and clarify the problem before writing code
- How you delegate to AI tools, and which parts you keep in your own head
- How you reason about concurrency, idempotency, and failure modes
- How you verify what the AI gives you
- How you'd take this to production — even if you don't get there

A working endpoint with thoughtful handling of duplicates will impress us more than a half-finished version of something more ambitious. **Scope aggressively — 45 minutes is tight.**

## Ground rules

- **Screenshare your full screen**, not just an editor window. We want to see your terminal and your AI tool.
- **Think out loud.** Tell us what you're considering, what you're worried about, what you're choosing not to do.
- **We may ask you to explain any line.** Assume we'll point at things. Use AI as much as you like, but own what's on the screen.
- **Ask questions any time.** Clarifying the problem is part of the job.
- **Use any libraries you want.** Standard library is fine, frameworks are fine, ORMs are fine — your call.

## Schedule

| Time | What's happening |
|------|------------------|
| 0:00 – 0:05 | Intro, ground rules, your questions |
| 0:05 – 0:50 | You build |
| 0:50 – 1:00 | Discussion — what you'd do next, what's missing for production |

We'll stay mostly out of your way during the build, but may ask occasional questions at decision points.

## Setup

```bash
docker compose up -d   # starts Postgres on localhost:5432
# then run your service however you like
```

Postgres connection details are in `docker-compose.yml`. Create whatever schema you need — that's part of the exercise.

## A few notes

- **You don't need to finish everything.** A small, working, well-reasoned service beats a sprawling one that doesn't run.
- **Production polish is good but optional.** If you have time at the end, things like logging, metrics, graceful shutdown, and meaningful error responses are all welcome. If you don't have time, we'll discuss them.
- **There are no trick questions.** The problem is what it looks like.

Good luck — we're looking forward to it.
