---
tags:
  - research
  - voice-assistant
  - ai-tools
---

# claw-code & openclaw.ai — Research Notes

*Researched: 02/04/2026*

---

## openclaw.ai

- **What:** Local, always-on personal AI assistant by Peter Steinberger
- **URL:** https://openclaw.ai/
- **How it works:** Runs persistently on your machine, you talk to it via WhatsApp / Telegram / Discord / Slack / Signal / iMessage
- **Features:** Persistent memory, browser control, file read/write, command execution, 50+ integrations, custom skills
- **Models:** Claude, GPT, local models
- **Cost:** Free and open-source
- **Verdict:** Not what I want for the voice assistant — it's a full product, not a harness to build on. Could be interesting as a standalone thing later though.

---

## claw-code

- **Main repo:** https://github.com/instructkr/claw-code *(locked mid-ownership transfer as of 02/04/2026)*
- **Parity/mirror repo:** https://github.com/ultraworkers/claw-code-parity *(active Rust work)*
- **Stars:** 142K — "fastest repo to hit 100K stars in history" (hit 50K in 2 hours)
- **Language:** Python first, Rust port in progress (binary: `claw`)

### Backstory

On 31/03/2026 at 4 AM, **Claude Code's TypeScript source was leaked**. Sigrid Jin (@instructkr, Korea) did a clean-room Python rewrite from scratch before sunrise using oh-my-codex (OmX). Rust port followed. This is essentially an open-source reimplementation of Claude Code — the tool I use right now.

### What the Rust port can do (as of 02/04/2026)

| Feature | Status |
|---|---|
| Anthropic API + streaming | ✅ |
| OAuth login | ✅ |
| Interactive REPL | ✅ |
| Tools: bash, read, write, edit, grep, glob | ✅ |
| Web search / fetch | ✅ |
| Sub-agent orchestration | ✅ |
| CLAUDE.md / project memory | ✅ |
| MCP server lifecycle | ✅ |
| Session persistence + resume | ✅ |
| Extended thinking | ✅ |
| Cost tracking, git integration | ✅ |
| Slash commands | ✅ |
| Hooks (PreToolUse/PostToolUse) | 🔧 Config only, not executed |
| Plugin system | 📋 Planned |
| Skills registry | 📋 Planned |

### Big gaps vs real Claude Code

1. Hook execution pipeline doesn't actually run
2. Plugin system absent
3. Skills registry not implemented
4. Missing tools: AskUserQuestion, plan/worktree, task tools, cron/schedule
5. No remote transports (SSE, WebSocket)
6. No advanced streaming orchestration

### Relevance to voice assistant

This is the planned **"brain"** in my voice assistant stack:

> Porcupine (wake word) → Whisper (STT) → **claw-code** (brain) → edge-tts (TTS)

It works as a local, self-hosted agent — receives text from Whisper, executes tools, returns a result. Basic usage would be:

```bash
claw --permission-mode danger-full-access prompt "turn the lights off"
```

Or pipe Whisper output directly into the binary from Python.

The core agentic loop is solid enough for a v1 voice assistant. The missing stuff (hooks, plugins, skills) doesn't matter for the first build.

### Current status / when to build

Too new and unstable right now (2 days old as of research date). Watch for a few weeks. By the time desktop Hyprland + claw-code setup is done, it should have stabilised.

---

## See also

- [[Jarvis/Old Notes (Aug 2025)]] — old voice assistant project notes
- [[z Meta/Claude/primer]] — current project priority order
