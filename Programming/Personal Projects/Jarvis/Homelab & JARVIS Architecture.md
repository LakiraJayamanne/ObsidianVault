---
tags:
  - spid
  - homelab
  - self-hosting
  - architecture
created: 2026-05-15
---

# SPID — Self-hosted Personal Intelligence Daemon

**S**elf-hosted **P**ersonal **I**ntelligence **D**aemon
Named 15/05/2026. Pronounced "Spidy" — Spider-Man reference, subtle.

SPID is the entire homelab system — not just the voice assistant. Pi-hole, Jellyfin, Nextcloud, voice layer, web UI — all of it. The voice assistant is one component of SPID, not the whole thing.

Dad is potentially helping fund it. ✓

---

## Hardware

| Item | Spec | Cost |
|---|---|---|
| Raspberry Pi 5 | 4GB | ~£55 |
| PSU | Official 27W USB-C | ~£12 |
| Cooling | Active cooler / fan case | ~£8 |
| OS storage | 32GB Samsung Endurance Pro microSD | ~£8 |
| Media/file storage | 2TB WD Elements USB HDD | ~£45 |
| **Total** | | **~£128** |

- Pi Zero W (Pi-hole) plan **scrapped** — Pi-hole runs on Pi 5 instead (Docker container)
- No mini PC needed — Immich dropped from scope (too heavy for Pi 5)

---

## Services (all Docker on Pi 5)

| Service | Purpose |
|---|---|
| Pi-hole | Network-wide DNS ad blocking |
| Jellyfin | Media server — movies + TV shows |
| Nextcloud | Self-hosted cloud file storage |
| SPID voice layer | Always-on wake word + STT + TTS (see below) |
| SPID web UI | PWA — chat interface for family, installable on Mac/iPhone |

### Media decisions
- **1080p only** — 4K ruled out (3–5x larger files, Pi 5 can't transcode 4K, Samsung TV compat not guaranteed for all 4K H.265)
- 2TB = ~100–200 movies at 1080p, expandable via second USB drive later
- Samsung Smart TV → official Jellyfin app on Tizen store (2020+ models)

### Networking (inside house)
- Pi 5 gets static local IP (e.g. `192.168.1.50`)
- All services accessible from any device on home WiFi via IP:port
- No extra setup needed for in-home access

### Networking (outside house)
- **Tailscale** — install on Pi + phone, acts like same network over 4G. Free, 10 min setup.
- Alternative: Cloudflare Tunnel (no VPN app, just a URL)

---

## SPID Voice Architecture

### Role split

| Device | Role |
|---|---|
| Pi 5 | Always-on — wake word, STT, TTS, tool execution |
| Desktop (RX 6700 XT) | GPU brain — qwen3:8b via Ollama when available |
| Claude Sonnet API | Primary always-on brain (basically Claude, running in SPID) |

### Dynamic brain routing (in `brain.py`)

```
1. Is Ollama reachable on desktop? → No → Claude API
2. Yes → query free VRAM via rocm-smi over SSH
3. Free VRAM > 6GB → use Ollama (qwen3:8b needs ~5.5GB)
4. Free VRAM < 6GB → Claude API
```

- Threshold: **6GB free VRAM** — gives game enough buffer
- Pi 5 queries desktop VRAM over SSH before every request
- Both Ollama and Claude API use same message format — swapping is clean
- ~30–40 lines of routing logic on top of existing brain.py

### Why Claude API not Ollama as primary
- Claude Sonnet = same intelligence as Claude.ai subscription, pay per use
- At 20 interactions/day → ~£0.57/month. Essentially free.
- Faster than local Ollama in most cases
- Lets Lakira ditch the Claude subscription — SPID becomes the interface

### Wake word
- "Hey Spidy" — OpenWakeWord, custom wake word planned
- Matches the name, natural to say

### Mobile + Watch access

- **iPhone** → Apple Shortcuts app → records voice → sends to SPID → response read aloud
- **Apple Watch (Series 3)** → triggers Shortcut from wrist → phone mic → SPID
  - No custom app, no dev account needed
  - Series 3 works now; SE 2 from CEX (~£105) would be snappier
  - CMF Watch ruled out — Android-paired, no Shortcuts integration

### Users
- **Lakira** — main user, voice + phone + watch
- **Brother** — GCSE homework help, web UI on home network
- **Dad** — occasional, uses Claude desktop for work already, may use SPID web UI

---

## Web UI / PWA

- **Stack:** Next.js + Tailwind + Framer Motion (already know from GroundLink)
- **Design:** Dark theme, glassmorphism, animated waveform, arc reactor blue accent, "Good afternoon, Lakira" greeting
- **Real-time:** WebSockets so responses stream in
- **PWA:** Installable on Mac (dad), iPhone, any device — looks like a native app
- **Access:** Local network for family, Tailscale for outside

---

## Cost Analysis (15/05/2026)

### Claude API (Sonnet — primary SPID brain)
- Input: $3/million tokens, Output: $15/million tokens
- Typical interaction: ~500 input + 200 output tokens = **~$0.0045 per conversation**
- At 20 interactions/day → **~$2.70/month (~£2.10)**. Cheaper than any subscription.
- Haiku (faster, less capable): ~£0.57/month at same usage.

### Pi 5 electricity (24/7)
- ~8W average draw
- 8W × 24h × 365 = 70 kWh/year × £0.25 = **£17.50/year (~£1.46/month)**

### Desktop electricity (24/7 for Ollama)
- ~80W average (idle with GPU loaded)
- **~£15/month** — 10x more expensive than Pi 5 + Claude API combined

### Verdict
| Option | Monthly cost |
|---|---|
| Pi 5 24/7 electricity | ~£1.50 |
| Claude API Sonnet (20x/day) | ~£2.10 |
| Desktop 24/7 for Ollama | ~£15 |

**Total SPID running cost: ~£3.60/month.** Cheaper than Claude subscription, better experience.

---

## Future / Rabbit Holes

- **Home Assistant** — Alexa + Samsung TV both compatible. Real smart home control without new hardware.
- **Custom "Spidy" wake word** — CoreWorxLab/openwakeword-training, 20–50 samples
- **openclaw.ai** — WhatsApp/text interface complement to voice
- **Ismail's setup (Leicester GC)** — near-identical stack, ask about hardware

---

## Build Order

1. Buy hardware (~£128)
2. Flash Raspberry Pi OS Lite to microSD
3. Connect Pi to router via ethernet
4. Install Docker
5. Deploy Pi-hole, Jellyfin, Nextcloud as containers
6. Set static IP for Pi on router
7. Point router DNS to Pi-hole
8. Port SPID voice layer onto Pi 5
9. Implement dynamic brain routing in brain.py (Claude API primary, Ollama upgrade)
10. Set up Tailscale for remote access
11. Build SPID web UI / PWA (Next.js)
12. Build iPhone Shortcut for mobile access
13. Train custom "Spidy" wake word
