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
- **Minecraft Server (Aternos)** — IN PROGRESS ⚠️
  - Client profile: mostly done, still debugging connection issues
  - Server: boots successfully (174 mods), but client can't connect yet
  - Current error: "Invalid entity data item type for field 17 on PlayerEntity" — mod mismatch
  - Removed from client so far: Krypton (Netty pipeline crash), Farmer's Delight (entity data mismatch)
  - Next fix to try: remove Citadel from client (leftover Alex's Mobs dependency, not on server)
  - Hosting: Aternos (free, hibernates when empty — chosen over Oracle due to signup friction)
  - Full mod list in Gaming/Minecraft Server.md
- **Crimson Desert settings** — DONE ✓ (26/04/2026)
  - Settings log at C:\Users\lakir\Desktop\crimson_desert_settings.txt
  - 1080p native, FSR Native AA, Lighting Ultra, RT ON, Power Limit +15%, Fan 100%

## CO1109 Enron Assignment — SUBMITTED ✓ (27/04/2026 1:30am)
- Report: WRITTEN, needs final touches before submission
  - File: C:\Users\lakir\Desktop\Enron_Report.docx
  - Word count: ~2250+ words ✓
  - **TODO: Reword Executive Summary + Methodology sections (AI risk)**
  - **TODO: Fix typos — "hundres", "Everon's"**
  - **TODO: Fill in word count on title page**
- Video: NOT YET RECORDED ⚠️
  - Script saved: Lecture Notes/CO1109/CO1109 Enron Video Script.md
  - Slides: C:\Users\lakir\Downloads\The-Enron-Scandal.pptx
  - Method: PowerPoint Record Slide Show with webcam overlay
  - 5 minutes, face on camera required
- Submission: ONE file only via Blackboard (video + report combined)

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

## Priority Order (next session — AFTER submission)
1. **CO1109 submission** — finish video, submit by noon Monday
2. **Minecraft server** — boot Aternos and test (40 mods loaded)
3. **wake.py** — OpenWakeWord
4. **Test stt.py** — Whisper STT on laptop
5. **input.py** — terminal text input
6. **main.py** — tie everything together
7. **Dad's Email Agent** — blocked on Anthropic API credits ($5 needed at console.anthropic.com)
8. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
9. **Plymouth boot animation**
10. **Gym Tracker Phase 2**

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
