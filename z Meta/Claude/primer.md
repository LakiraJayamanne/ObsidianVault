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
  - config.py ✓ (brain_model = qwen3:8b → SWITCHING TO qwen3:1.7b — see research below)
  - stt.py ✓ Moonshine tiny-en. Energy threshold (0.001 RMS) skips silence. Timestamp markers stripped.
  - tts.py ✓ Kokoro ONNX (bm_lewis) — fully local, natural voice.
  - brain.py ✓ Full tool-calling pipeline — Ollama tool schemas, ack before action, 20-msg history, memory in system prompt, /no_think for Qwen3
  - wake.py ✓ Alexa wake word, debounce
  - main.py ✓ Conversational loop — stays active after wake word, 20s silence → "Standing by, sir."
  - tools.py ✓ 12 tools: get_time, get_date, get_weather, set_timer, get_system_stats, open_app, set_volume, mute, add_note, add_task, web_search, remember
  - memory.md in vault (z Meta/JARVIS/) — persistent facts loaded into system prompt each session

  ### LLM Model Research (13/05/2026) — CONCLUSION: Switch to qwen3:1.7b
  - Deep research done on 21-model tool-calling benchmark (Mike Veerman, Feb 2026)
  - qwen3:1.7b scored 0.960 agent score — HIGHEST of all 21 models tested
  - qwen3:8b: ~25–35 tok/s, ~6s TTFT. qwen3:1.7b: ~100–140 tok/s, sub-1s TTFT expected on RX 6700
  - qwen3:4b: same agent score as qwen3:0.6b (0.880) — worse than 1.7b, not worth it
  - phi4-mini: confirmed broken tool_calls on Ollama (GitHub issue #9437), skip
  - llama3.2:3b: calls tools on EVERY prompt — unusable
  - Action: `ollama pull qwen3:1.7b`, create Modelfile with `num_ctx 2048` + `num_predict 256`
  - Also add `OLLAMA_KEEP_ALIVE=-1` to systemd ROCm override
  - Try `OLLAMA_FLASH_ATTENTION=1` + `OLLAMA_KV_CACHE_TYPE=q8_0` (may or may not activate on RDNA2)

  ### STT Research (13/05/2026) — CONCLUSION: Switch to whisper.cpp small.en + Vulkan
  - Deep research on 7 STT options for RX 6700 (gfx1031), British/Sri Lankan accent, low latency
  - Moonshine tiny-en root cause: trained only on American English (LibriSpeech), 12.66% WER — accent-blind
  - Moonshine base: 10.07% WER but still American-only training — won't fix accent issue
  - **VERDICT: whisper.cpp + Vulkan backend + small.en model**
    - Vulkan works on all AMD GPUs including gfx1031 — NO HSA_OVERRIDE needed (not ROCm)
    - Build: `cmake -B build -DGGML_VULKAN=1 && cmake --build build -j --config Release`
    - Python via pywhispercpp: `GGML_VULKAN=1 pip install git+https://github.com/absadiki/pywhispercpp`
    - Whisper small.en: 244M params, 466MB, multilingual-trained → accent-robust
    - Expected latency: ~300–600ms for 3–5s utterance on RX 6700 via Vulkan (similar to RX 6600 HIP at ~1s/min)
    - Whisper small on Indian accent: 17.36% WER fine-tuned, untuned but much better than Moonshine tiny on accents
    - Larger whisper consistently beats smaller on accent diversity (large >> medium >> small >> tiny)
    - Alternative (CPU fallback): faster-whisper base.en int8 — ~800ms–1.5s on i5-12400F — acceptable
    - Why NOT distil-whisper: distilled models specifically underperform on accent-diverse benchmarks (EdAcc, AfriSpeech)
    - Why NOT Parakeet: CUDA-only, no AMD GPU path, CPU latency unknown but designed for NVIDIA
    - Why NOT Vosk: Kaldi-based, good for low-power but noticeably lower accuracy than Whisper
    - Why NOT wav2vec2: 37% WER on clean audio in 2025 benchmarks — worse than Whisper on everything
    - Model file: `models/ggml-small.en.bin` (~466MB), download with `bash models/download-ggml-model.sh small.en`
  ### Session 77 changes (13/05/2026)
  - Brain: qwen3:1.7b → jarvis-brain (qwen3:8b, num_ctx 8192, num_predict 1024, think=True for tool decisions)
  - Memory: about-lakira.md loaded into system prompt every session ✓
  - Memory: async proactive extraction after each LLM turn (background thread, strict prompt)
  - Intent: apostrophe normalisation fix, threshold lowered to 4 words, many new intent words
  - Intent: set_personality removed from LLM tools — keyword-routed only (no more hallucination)
  - Intent: routes for now_playing, notes, tasks, clipboard, screen, personality
  - Brain: _strip_think on all responses, think=True on tool-decision call
  - Tools added: read_notes, read_tasks, get_now_playing, remind_at, read_clipboard, log_gym, describe_screen
  - Tools: web_research upgraded — DDG HTML search + fetches 3 sources, combines results
  - main.py: last_speech reset after _respond (standby timer fix)
  - wake.py: debug score print removed
  - Zen Browser set as system default browser
  - psutil installed (CPU/RAM now show in system stats)
  - **Next: custom "Persona" wake word** — CoreWorxLab/openwakeword-training, 20-50 samples
  - **Next: always-on media/mute hotwords** — parallel listener, no wake word needed
  - **Next: STT fine-tuning** — train faster-whisper small on Lakira's voice (~1-2hr recording)
  - **Next: dictation mode** — hotkey → speak → paste into any app
  - **Next: Discord bot** — discord_bot.py, text input to JARVIS via Discord channel
  - **Next: screen awareness** — pull gemma3:4b (`ollama pull gemma3:4b`), then describe_screen works
  - **Next: presence detection** — DroidCam on Samsung M21 (deprioritised, last on list)
  - discord_bot.py — not started
- **Apple Watch (Series 3)** — Dad's old watch, set up with Omnitrix photo face. Battery degraded (~3hrs). watchOS 8.8.1, no jailbreak possible. Clockology not compatible. Decent for step tracking/notifications as-is. Considering SE 2nd gen refurb from CEX (~£105) eventually.
- **Gym Tracker** — Phase 1 complete. Phase 2 not started.
- **Memory system** — Fully in Obsidian vault ✓
- **Minecraft Server (Aternos)** — DEPRIORITISED (Lakira lost interest)
- **Crimson Desert settings** — DONE ✓ (26/04/2026)
  - Settings log at C:\Users\lakir\Desktop\crimson_desert_settings.txt
  - 1080p native, FSR Native AA, Lighting Ultra, RT ON, Power Limit +15%, Fan 100%

## CO1109 Enron Assignment — SUBMITTED ✓ (27/04/2026 1:30am)

## OOP Test — COMPLETED (13/05/2026)
- Q1: polymorphism/method overriding output trace (B)
- Q2: UML diagram false statements (B, D, E)
- Q3: fill-in-the-blanks on abstract classes, super, overriding, polymorphism
- Q4: keyword matching (final, static, implements, super)
- Q5: Java error finding — 4 errors (extend→extends, this.name→super(name,price), discount missing (), main missing static)

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
| Wake word | OpenWakeWord (Alexa) — custom "Persona" wake word planned |
| STT | Moonshine tiny-en (local, ~270ms CPU) |
| Brain | Ollama — qwen3:8b on GPU |
| TTS | Kokoro ONNX (bm_lewis) — fully local |
| Text input | Discord bot (not started) |
| Memory | Obsidian vault — z Meta/JARVIS/ |

- Project at: `/home/Lakira/Documents/PROGRAMMING/PERSONAL/MyPersona/` (synced via GitHub)
- Full build notes + feature roadmap: `Programming/Personal Projects/Jarvis/Persona Build Notes.md`

## Priority Order
1. **GroundLink Sri Lanka** — awaiting dad's feedback
2. **JARVIS — STT energy threshold tuning** — do on Fedora, remove debug prints when done
3. **JARVIS — barge-in/interrupt** — Vocalis pattern
4. **JARVIS — proactive mode** — background trigger daemon
5. **JARVIS — presence detection** — DroidCam on Samsung M21
6. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
7. **Plymouth boot animation**
8. **Gym Tracker Phase 2**

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
