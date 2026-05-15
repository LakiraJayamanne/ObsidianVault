---
tags:
  - claude-memory
  - claude/status
---

# Project Primer

Current project status, what's in progress, what's next.

---

## Current Status
- **Hyprland on Fedora (laptop)** — Fully working. SDDM fixed. ✓
- **Desktop dual boot (Fedora 43)** — DONE ✓ (02/04/2026)
- **Desktop Hyprland + Caelestia rice** — FULLY WORKING ✓ (07/04/2026)
  - rgba syntax fixed, keybinds working, quickshell bar working
  - Dynamic Material You theming active
  - Vibrance shader active (1.1x saturation) at ~/.config/hypr/shaders/vibrance.frag
  - Mouse accel disabled
  - Super+Backspace + Super+middle click = killactive
  - Super+Shift+W = wallpaper shuffle
  - Sidebar character = spidey_circle.png
  - fastfetch = saturn.txt logo (image attempts abandoned due to sixel black bar issue)
- **Desktop GRUB** — Text mode (console), old kernel removed (6.17.1 gone, only 6.19.10 remains), rescue entry hidden. Theme NOT yet applied. nomodeset still in kernel args. ⚠️
- **Desktop Windows boot fix** — CONFIRMED WORKING ✓
- **Monitor @ 165Hz, scale 1.0** — Set in ~/.config/hypr/hyprland/monitors/default.conf ✓
- **Zen Browser** — Installed via Flatpak ✓
- **Spicetify** — DONE ✓
- **Wallpapers** — Synced from laptop ✓
- **Ollama** — llama3.1 8B + llama3.2:3b pulled, 100% GPU via ROCm (HSA_OVERRIDE_GFX_VERSION=10.3.0 in systemd override) ✓
- **System font** — Segoe UI (copied from Windows partition), set via gsettings + GTK3/4 ✓
- **Mouse sensitivity** — flat accel, sensitivity -0.15 ✓
- **Apple Watch (Series 3)** — Dad's old watch, set up with Omnitrix photo face. Battery degraded (~3hrs). watchOS 8.8.1, no jailbreak possible. Clockology not compatible. Decent for step tracking/notifications as-is.

---

## SPID — Self-hosted Personal Intelligence Daemon 🔥 NEW PROJECT

**Named 15/05/2026. Pronounced "Spidy" — subtle Spider-Man reference.**

SPID is the entire homelab system running on a Raspberry Pi 5. Not just a voice assistant — the whole thing.

### Hardware (to buy — ~£128 total)
- Raspberry Pi 5 4GB — ~£55
- Official 27W USB-C PSU — ~£12
- Active cooler / fan case — ~£8
- 32GB Samsung Endurance Pro microSD — ~£8
- 2TB WD Elements USB HDD — ~£45
- Dad may help fund it ✓

### Services (Docker on Pi 5)
- Pi-hole — network-wide ad blocking
- Jellyfin — movies + TV (1080p, Samsung Smart TV via Tizen app)
- Nextcloud — self-hosted cloud storage
- SPID voice layer — always-on wake word + STT + TTS
- SPID web UI — PWA, chat interface for family

### Brain routing
- Claude Sonnet API — primary always-on brain (~£2.10/month at 20x/day)
- Ollama qwen3:8b on desktop GPU — upgrade when at desk and VRAM > 6GB free
- Dynamic routing: Pi 5 checks desktop VRAM via rocm-smi over SSH before each request
- Total running cost: ~£3.60/month (Pi electricity + Claude API)

### Users
- Lakira — main (voice + phone + Apple Watch)
- Brother — GCSE homework help via web UI
- Dad — occasional, has Claude desktop for work

### UI — IN PROGRESS ⚡
- **Design:** HUD-style + Apple glass hybrid. Black (#080808) + deep crimson red (#C0001A)
- **Inspired by:** Superior Spider-Man suit aesthetic + Iron Man HUD
- **Components:** radar circle (centre), glass panels (left/right), voice waveform + command input (bottom), status pill (top)
- **Stack:** Next.js + Tailwind + Framer Motion (same as GroundLink)
- **PWA:** installable on Mac (dad), iPhone, any device
- **Real-time:** WebSockets for streaming responses
- **Boot screen:** terminal-style loading sequence (monospace, progress bar)
- **Stats toggle:** HUD-style data cards slide in when toggled
- **WHERE TO BUILD:** inside SPIDy repo at `/home/lakira/Documents/Projects/SPIDy/ui/`
- **Reference design:** Blink JARVIS dashboard (blink.new/p/jarvis-dashboard-ui-xqnrnbw1) — no public source, build from scratch

### Full architecture doc
`Programming/Personal Projects/Jarvis/Homelab & JARVIS Architecture.md`

### NEXT SESSION — START HERE
1. Open VS Code → `~/Documents/Projects/SPIDy/ui`
2. Edit `app/globals.css` — set `--background: #080808`, add `--crimson: #C0001A`, remove dark mode media query, set `--foreground: #ededed`
3. Build the radar circle component first (`app/components/RadarCircle.tsx`)

---

## Voice Assistant (SPID) — Current Stack
| Component | Choice |
|---|---|
| Wake word | hey_jarvis_v0.1.onnx → rename to "Hey Spidy" custom wake word (planned) |
| STT | faster-whisper small.en int8 CPU (~800ms–1.5s) |
| Brain | Claude Sonnet API (primary) + Ollama qwen3:8b (desktop GPU fallback) |
| TTS | Kokoro ONNX (bm_lewis) — fully local |
| Text input | Web UI (PWA) — Discord bot deprioritised |
| Memory | Obsidian vault — z Meta/JARVIS/ |

- Project at: `/home/lakira/Documents/Projects/SPIDy/` (synced via GitHub: LakiraJayamanne/SPIDy)

---

## GroundLink Sri Lanka — DAD REVIEW IN PROGRESS 🔥 PRIORITY #1
- **What it is:** SaaS platform for guide/driver/vehicle management in Sri Lankan inbound tourism
- **Client:** TTC Sri Lanka (dad's company — laahiru@ttcsrilanka.com)
- **Project path:** C:\Users\lakir\Documents\Projects\groundlink
- **GitHub:** https://github.com/LakiraJayamanne/groundlink (private)

### Stack
- Next.js 16, TypeScript, Tailwind CSS
- Prisma 5 + SQLite (dev) → PostgreSQL (prod)
- Custom JWT auth (jose + bcryptjs)
- No AI API in app (pure logic)

### What's been built (as of 29/04/2026) — PHASE 1 COMPLETE ✅
- Full Prisma schema (11 tables), all API routes, full role-based auth
- DMC, Guide, Admin, Transport manager / Supplier, Settings pages all built
- GPS tracking, post-tour rating, admin doc review, vehicle assignment all done
- Toast notifications, Leaflet map, ngrok fix all done

### ngrok fix (08/05/2026) ✓
- To re-expose for dad: `npm run dev` in one terminal, `ngrok http 3000` in another. New URL each session.
- Dad has not yet completed review — awaiting feedback before starting Phase 2

### What's next (Phase 2)
1. Email notifications (Resend)
2. PWA manifest
3. PDF/CSV export for bookings
4. Notification bell UI
5. Programme/itinerary builder

---

## CO1109 Enron Assignment — SUBMITTED ✓ (27/04/2026 1:30am)
## OOP Test — COMPLETED (13/05/2026)

---

## Priority Order
1. **GroundLink Sri Lanka** — awaiting dad's feedback
2. **SPID UI** — build on Fedora, Next.js inside MyPersona/ui/
3. **SPID — custom "Spidy" wake word** — CoreWorxLab/openwakeword-training, 20–50 samples
4. **SPID — Discord bot** — deprioritised (web UI takes priority now)
5. **SPID — screen awareness** — pull gemma3:4b
6. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
7. **Plymouth boot animation**
8. **Gym Tracker Phase 2**

---

## Raspberry Pi Projects — UPDATED (15/05/2026)
### SPID Homelab (Pi 5 4GB) — ~£128 — NEW PRIORITY
- Replaces both the portable JARVIS Pi Zero 2 W and Pi-hole Pi Zero W plans
- Pi-hole runs on Pi 5 in Docker alongside everything else

### Portable JARVIS (Pi Zero 2 W) — ~£29 — DEPRIORITISED
- Still planned eventually but SPID homelab takes priority

---

## Caelestia Notes (desktop)
- Installed via EnceladusII/caelestia-fedora (abandoned Fedora fork, frozen Aug 2025)
- Quickshell installed via COPR (errornointernet/quickshell)
- Shell lives at ~/.config/quickshell/caelestia
- Hyprland config split across ~/.config/hypr/hyprland/*.conf
- User overrides go in ~/.config/caelestia/hypr-vars.conf and hypr-user.conf
- Keybinds at ~/.config/hypr/hyprland/keybinds.conf
- Bar is on the left (default)

---

## Gym Tracker Build Phases
1. [x] Phase 1 — models.py (ExerciseSet, Session, Log)
2. [ ] Phase 2 — storage.py (save/load JSON)
3. [ ] Phase 3 — main.py (text menu)
4. [ ] Phase 4 — algorithms.py (overload, plateau, bodyweight trend)
5. [ ] Phase 5 — Polish

## Gym Tracker — Confirmed Changes (07/04/2026)
- **RIR instead of RPE** — swap effort rating system in data model
- **Weekly Volume tracker** — total sets per muscle group per week (add to Phase 4)
- **Phone app — DECIDED AGAINST for now** — finish terminal version first
- **Draw HEAVY inspiration from tracked.gg** (by Keenan)

---

## Dad's Email Agent (23/04/2026) — BLOCKED ⚠️
- For Lakira's dad (Lahiru), on **Mac**, email: laahiru@ttcsrilanka.com
- Script lives at: `/Users/laahirujayamanne/Documents/email_agent.py`
- **BLOCKED: Anthropic API has no credits** — dad needs to add $5 minimum at console.anthropic.com → Plans & Billing
