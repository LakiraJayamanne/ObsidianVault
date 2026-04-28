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
- **Ollama** — Installed, llama3.1 8B pulled and working ✓
- **Voice Assistant (JARVIS)** — IN PROGRESS ⚠️
  - config.py ✓ (added stt_model = "base")
  - tts.py ✓ (tested, working)
  - brain.py ✓ (ollama.chat() working, tested, ~4s response time)
  - stt.py ✓ (Whisper base, sounddevice, written + pushed — NOT YET TESTED)
  - wake.py — not started
  - discord_bot.py — not started
  - tools.py — not started
  - input.py — not started
  - main.py — not started
- **Gym Tracker** — Phase 1 complete. Phase 2 not started.
- **Memory system** — Fully in Obsidian vault ✓
- **Minecraft Server (Aternos)** — DEPRIORITISED (Lakira lost interest)
- **Crimson Desert settings** — DONE ✓ (26/04/2026)
  - Settings log at C:\Users\lakir\Desktop\crimson_desert_settings.txt
  - 1080p native, FSR Native AA, Lighting Ultra, RT ON, Power Limit +15%, Fan 100%

## CO1109 Enron Assignment — SUBMITTED ✓ (27/04/2026 1:30am)

## GroundLink Sri Lanka — IN PROGRESS 🔥 PRIORITY #1
- **What it is:** SaaS platform for guide/driver/vehicle management in Sri Lankan inbound tourism
- **Client:** TTC Sri Lanka (dad's company — laahiru@ttcsrilanka.com)
- **Project path:** C:\Users\lakir\Documents\Projects\groundlink
- **Old Python prototype:** C:\Users\lakir\Documents\Projects\GuideTracker (scrapped)
- **GitHub:** https://github.com/LakiraJayamanne/groundlink (private)
- **Docs:** C:\Users\lakir\Documents\Projects\GuideTracker\DOCS\ (groundlink-techspec.docx + groundlink-flows.html)

### Stack
- Next.js 16, TypeScript, Tailwind CSS
- Prisma 5 + SQLite (dev) → PostgreSQL (prod)
- Custom JWT auth (jose + bcryptjs)
- No AI API in app (pure logic)

### What's been built (as of 28/04/2026)
- Full Prisma schema: organisations, users, guide_profiles, vehicles, availability, bookings, gps_events, sleep_logs, documents, ratings, notifications
- API routes: register, login, /api/guides, /api/guides/:id, /api/bookings, /api/bookings/:id, /api/vehicles, /api/admin/verify/:userId, /api/admin/pending
- DMC dashboard: overview stats + bookings table, bookings list with status filter tabs, new booking form, booking detail page with status transitions + guide assignment slide-in panel + vehicle slot
- Guide directory: card grid with language/type/date filters, star ratings, language badges
- Admin queue: pending user cards with approve/reject
- JWT auth with role guard (dmc_ops, transport_mgr, guide, driver, supplier, admin)
- Organisation auto-created at registration for dmc_ops/transport_mgr/supplier
- Dark mode CSS bug fixed (globals.css — removed dark media query, forced light colour-scheme)
- `withErrorHandling<C>` made generic for typed route contexts
- Guide onboarding wizard written (`src/app/onboarding/page.tsx`) — 3-step: guide type + SLTDA licence + day rate → languages + zones → specialisms + bio

### What's IN PROGRESS / NOT YET COMMITTED
- `src/app/onboarding/page.tsx` — written, not committed, not type-checked
- `src/app/login/page.tsx` — needs redirect to `/onboarding` after guide/driver registration (currently always goes to `/dashboard`)
- Several modified files unstaged: register/route.ts, guides/page.tsx, globals.css, login/page.tsx

### What's next (Phase 1 completion)
1. **Commit checkpoint 1** — onboarding wizard + login redirect for guides/drivers
2. **Checkpoint 2** — Role-aware dashboard: guides see their own booking diary with accept/decline, not DMC table
3. **Checkpoint 3** — Toast notifications (guide assigned, status changed)
4. **Checkpoint 4** — Document upload flow (S3 or local for dev)
5. **Checkpoint 5** — GPS position endpoint + live map placeholder (Phase 2)

## Voice Assistant — Current Stack
| Component | Choice |
|---|---|
| Wake word | OpenWakeWord (fully local, no account needed) |
| STT | Whisper base (local) |
| Brain | Ollama — llama3.1 8B + tool-calling loop |
| TTS | edge-tts — en-GB-RyanNeural |
| Text input | Discord bot |
| Actions | tools.py (system control, file I/O, web search etc.) |
| Memory | Obsidian vault — z Meta/JARVIS/ |

- Wake word: "Persona"
- Assistant name: **JARVIS / Persona** (Persona game character, TBD)
- Project at: `/home/Lakira/Documents/PROGRAMMING/PERSONAL/MyPersona/` (laptop + desktop, synced via GitHub)
- Full build notes: `Programming/Personal Projects/Jarvis/Persona Build Notes.md`

## Priority Order
1. **GroundLink Sri Lanka** — booking detail + guide assignment, then admin queue
2. **JARVIS — wake.py** — OpenWakeWord
3. **Test stt.py** — Whisper STT on laptop
4. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
5. **Plymouth boot animation**
6. **Gym Tracker Phase 2**

## Caelestia Notes (desktop)
- Installed via EnceladusII/caelestia-fedora (abandoned Fedora fork, frozen Aug 2025)
- Quickshell installed via COPR (errornointernet/quickshell)
- Shell lives at ~/.config/quickshell/caelestia
- Hyprland config split across ~/.config/hypr/hyprland/*.conf
- User overrides go in ~/.config/caelestia/hypr-vars.conf and hypr-user.conf
- Keybinds at ~/.config/hypr/hyprland/keybinds.conf
- Bar is on the left (default)

## Gym Tracker Build Phases
1. [x] Phase 1 — models.py (ExerciseSet, Session, Log)
2. [ ] Phase 2 — storage.py (save/load JSON)
3. [ ] Phase 3 — main.py (text menu)
4. [ ] Phase 4 — algorithms.py (overload, plateau, bodyweight trend)
5. [ ] Phase 5 — Polish

## Gym Tracker — Confirmed Changes (07/04/2026)
- **RIR instead of RPE** — swap effort rating system in data model
- **Weekly Volume tracker** — total sets per muscle group per week (add to Phase 4)
- **Phone app — DECIDED AGAINST for now** — finish terminal version first, use it, port to PWA later if needed
- **Draw HEAVY inspiration from tracked.gg** (by Keenan) — reference it for UX, features, and flow decisions

## Dad's Email Agent (23/04/2026) — BLOCKED ⚠️
- For Lakira's dad (Lahiru), on **Mac**, email: laahiru@ttcsrilanka.com
- Script lives at: `/Users/laahirujayamanne/Documents/email_agent.py`
- **BLOCKED: Anthropic API has no credits** — dad needs to add $5 minimum at console.anthropic.com → Plans & Billing
- Once credits added: run `python3 ~/Documents/email_agent.py` — works immediately
