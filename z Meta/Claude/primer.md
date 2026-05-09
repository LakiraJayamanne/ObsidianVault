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
- **Voice Assistant (JARVIS/Persona)** — TOOLS + CONVERSATIONAL MODE ✅ (09/05/2026)
  - config.py ✓ (brain_model = qwen3:8b, conversation_silence = 20s)
  - stt.py ✓ Moonshine tiny-en. Energy threshold (0.001 RMS) skips silence. Timestamp markers stripped.
  - tts.py ✓ Kokoro ONNX (bm_lewis) — fully local, natural voice.
  - brain.py ✓ Full tool-calling pipeline — Ollama tool schemas, ack before action, 20-msg history, memory in system prompt, /no_think for Qwen3
  - wake.py ✓ Alexa wake word, debounce
  - main.py ✓ Conversational loop — stays active after wake word, 20s silence → "Standing by, sir."
  - tools.py ✓ 12 tools: get_time, get_date, get_weather, set_timer, get_system_stats, open_app, set_volume, mute, add_note, add_task, web_search, remember
  - memory.md in vault (z Meta/JARVIS/) — persistent facts loaded into system prompt each session
  - **Next: tune ENERGY_THRESHOLD** (debug rms prints still in stt.py — remove when happy)
  - **Next: Obsidian vault RAG** — search vault notes for context (separate session)
  - **Next: Claude API as brain option** — ~0.3s to first token vs ~3-5s local. Hybrid approach.
  - **Next: custom "Persona" wake word** — CoreWorxLab/openwakeword-training, 20-50 samples
  - discord_bot.py — not started
  - input.py — not started
  - **Custom "Persona" wake word** — needs training (CoreWorxLab/openwakeword-training, 20-50 samples). Using Alexa for now.
- **Gym Tracker** — Phase 1 complete. Phase 2 not started.
- **Memory system** — Fully in Obsidian vault ✓
- **Minecraft Server (Aternos)** — DEPRIORITISED (Lakira lost interest)
- **Crimson Desert settings** — DONE ✓ (26/04/2026)
  - Settings log at C:\Users\lakir\Desktop\crimson_desert_settings.txt
  - 1080p native, FSR Native AA, Lighting Ultra, RT ON, Power Limit +15%, Fan 100%

## CO1109 Enron Assignment — SUBMITTED ✓ (27/04/2026 1:30am)

## GroundLink Sri Lanka — DAD REVIEW IN PROGRESS 🔥 PRIORITY #1
- **What it is:** SaaS platform for guide/driver/vehicle management in Sri Lankan inbound tourism
- **Client:** TTC Sri Lanka (dad's company — laahiru@ttcsrilanka.com)
- **Project path:** C:\Users\lakir\Documents\Projects\groundlink
- **Old Python prototype:** C:\Users\lakir\Documents\Projects\GuideTracker (SCRAPPED + REPO DELETED 08/05/2026)
- **GitHub:** https://github.com/LakiraJayamanne/groundlink (private)
- **Docs:** C:\Users\lakir\Documents\Projects\GuideTracker\DOCS\ (groundlink-techspec.docx + groundlink-flows.html)

### Stack
- Next.js 16, TypeScript, Tailwind CSS
- Prisma 5 + SQLite (dev) → PostgreSQL (prod)
- Custom JWT auth (jose + bcryptjs)
- No AI API in app (pure logic)

### What's been built (as of 29/04/2026) — PHASE 1 COMPLETE ✅
- Full Prisma schema (11 tables), all API routes, full role-based auth
- **DMC:** overview stats, bookings list + filter, new booking form, booking detail (status flow, guide + vehicle assignment panels, live map when active, rate guide on completion)
- **Guide:** 3-step onboarding wizard, diary view (upcoming/past), accept/decline pending bookings, share live location button on active bookings, document upload card
- **Admin:** verification queue with expandable doc preview, approve/reject
- **Transport manager / Supplier:** fleet management page (add vehicle modal, class filter)
- **All roles:** settings page (name, phone, password change)
- Guide profile detail pages (ratings, bio, zones, specialisms, reviews)
- Guide directory cards clickable through to profile
- Toast notifications system (slide-up, 3.5s, success/error/info)
- GPS tracking: POST /api/gps (guide pushes position), GET polls latest for booking, Leaflet map on booking detail (polls every 15s)
- Post-tour rating modal (star picker + notes, updates guide aggregate)
- Admin doc review: expandable panel per user, view uploaded files inline
- Vehicle assignment panel (mirrors guide panel UX)
- PATCH /api/me: name/phone/password with current password verification

### ngrok fix (08/05/2026) ✓
- Added `allowedDevOrigins` to next.config.ts for all ngrok domains (*.ngrok-free.app, *.ngrok-free.dev, *.ngrok.io, *.ngrok.app)
- Added `suppressHydrationWarning` to body in layout.tsx (AdBlock Plus injects vc-init class → hydration mismatch)
- Both fixes pushed to GitHub
- To re-expose for dad: `npm run dev` in one terminal, `ngrok http 3000` in another. New URL each session.
- Dad has not yet completed review — awaiting feedback before starting Phase 2

### What's next (Phase 2 / nice-to-have)
1. Email notifications (Resend) — guide assigned, guide accepts
2. PWA manifest — guides add to phone home screen
3. PDF/CSV export for bookings
4. Notification bell (model exists, just needs UI)
5. Programme/itinerary builder (route planner in booking)

## Voice Assistant — Current Stack
| Component | Choice |
|---|---|
| Wake word | OpenWakeWord (fully local, no account needed) |
| STT | Whisper tiny (local, CPU — SLOW, needs replacing) |
| Brain | Ollama — llama3.2:3b on GPU (~0.5s) |
| TTS | edge-tts — en-GB-RyanNeural (cloud, needs replacing) |
| Text input | Discord bot (not started) |
| Actions | tools.py (not started) |
| Memory | Obsidian vault — z Meta/JARVIS/ |

- Wake word: "Persona"
- Assistant name: **JARVIS / Persona** (Persona game character, TBD)
- Project at: `/home/Lakira/Documents/PROGRAMMING/PERSONAL/MyPersona/` (laptop + desktop, synced via GitHub)
- Full build notes + optimization plan: `Programming/Personal Projects/Jarvis/Persona Build Notes.md`

### STT Optimization Plan (researched 08/05/2026)
**Step 1 (quick win):** Switch to `faster_whisper` with `compute_type="int8"`, pre-load model once at startup + add Silero VAD. The 24s is likely a code issue, not a GPU issue.
**Step 2:** Try Moonshine STT (`pip install moonshine-voice`) — ~270ms on CPU, beats Whisper Large V3 accuracy.
**Step 3:** Swap edge-tts → Piper TTS (`en_GB-alan-medium` voice) with streaming synthesis.
**Step 4:** Stream LLM tokens → TTS (sentence buffer pattern) — biggest single architecture win.
**Step 5 (optional):** whisper.cpp with Vulkan (`-DGGML_VULKAN=1`) for GPU STT on RX 6700.

**Acknowledgement pattern:** For long tasks, JARVIS speaks an immediate ack ("On it sir, researching xyz") then does the work in background and reports when done.

## Priority Order
1. **GroundLink Sri Lanka** — awaiting dad's feedback
2. **JARVIS STT optimization** — clear plan ready, do on Fedora
3. **JARVIS tools.py** — give Persona real-time data (time, weather, etc.)
4. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
5. **Plymouth boot animation**
6. **Gym Tracker Phase 2**

## Raspberry Pi Projects — PLANNED (02/05/2026)
### Portable JARVIS (Pi Zero 2 W) — ~£29
- Pi Zero 2 W (£15) + 16GB micro SD (£7) + INMP441 I2S mic (£5) + micro USB OTG adapter (£2)
- Already have: power bank, Alexa as Bluetooth speaker, micro USB cable
- Architecture: same as desktop JARVIS — wake word → Whisper STT → Claude API → edge-tts → Alexa speaker
- Needs soldering: header pins on Pi Zero 2 W + INMP441 wiring to GPIO

### Pi-hole (Pi Zero W) — ~£14
- Pi Zero W (£9) + 8GB micro SD (£5)
- Network-wide ad blocker — plug in near router, set as DNS in router settings, done
- Runs completely headlessly, totally separate from JARVIS Pi

### Combined total: ~£43 for both

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
