---
tags:
  - tools
  - ide
  - ai
---

# Google Antigravity IDE

**Released:** 18 November 2025
**Website:** antigravity.google
**Type:** Agent-first AI IDE (VS Code fork)

---

## What it is

An IDE where AI agents are the primary actors, not assistants. You define a task, multiple agents run in parallel — one plans, one codes, one writes tests, one browses — and you review their work via an "Artifacts" dashboard (task lists, screenshots, browser recordings). Asynchronous by design: kick off a task and walk away.

This is fundamentally different from Claude Code or Cursor, which are chat-based and sequential.

---

## Key Features

- **Multi-agent parallelisation** — spawn multiple agents simultaneously
- **Artifacts system** — audit agent reasoning, decisions, screenshots
- **Multi-model** — Gemini 3 Pro (default), Claude Sonnet 4.6, OpenAI models
- **Browser integration** — Chrome only
- **Terminal access** — agents can run commands

---

## Pricing

| Tier | Price | Notes |
|---|---|---|
| Free preview | £0 | Currently available |
| Pro | $25/month | Gemini 3.1 Pro, unlimited completions |
| Enterprise | $45/user/month | — |

---

## vs. Claude Code / Cursor

| Tool | Approach | Best for |
|---|---|---|
| **Claude Code** | Chat-based, integrated, sequential | Daily maintenance, ongoing work |
| **Cursor** | Chat-based, incremental edits | Line-by-line refinement |
| **Antigravity** | Agent-first, async, parallel | Scaffolding new projects fast |

---

## Linux Support

- Fedora 36+ via `.rpm` ✓
- Ubuntu 20.04+, Debian 11+, RHEL 8+ via `.deb`
- Requires glibc 2.28+, graphical session, Chrome

---

## Honest Assessment (as of May 2026)

**Good:** Scaffolding new projects is fast. Multi-agent parallelism is genuinely novel. Free tier is usable.

**Bad:** Chrome-only browser integration. Reports of throttling/quota exhaustion post-launch. AI quality degrades on long-running projects as context gets messier. Windows stability issues. Slow agent planning phase.

**Verdict:** Worth experimenting with for initial project scaffolding (e.g. GroundLink Phase 2, future SPIDy features). Not a daily driver replacement for Claude Code yet.

---

## Noted

First seen: 16/05/2026. Looked up during SPIDy session.
