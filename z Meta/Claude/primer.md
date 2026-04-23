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

## JARVIS — Architecture Decisions (07/04/2026)
- Runs as a persistent background process — never cold-starts on wake word
- Memory lives in Obsidian vault at `z Meta/JARVIS/` — separate from Claude's `z Meta/Claude/`
- Claude reads JARVIS memory, JARVIS reads Claude memory — cross-readable, separately writable
- Discord as messaging layer (proper bot API, works on phone + desktop)
- Brain upgraded to tool-calling loop — JARVIS can execute actions, not just reply
- Inspiration: claw-code agentic loop + openclaw.ai action model
- Ollama network sharing planned: desktop runs Ollama, laptop + phone point to it over LAN

## JARVIS — File Plan
| File | Status | Role |
|---|---|---|
| config.py | ✓ | All settings |
| tts.py | ✓ | Speak responses |
| brain.py | ✓ | LLM + tool-calling loop |
| stt.py | ✓ written, not tested | Whisper STT |
| wake.py | not started | OpenWakeWord trigger |
| tools.py | not started | All actions JARVIS can take |
| discord_bot.py | not started | Text channel on phone/desktop |
| input.py | not started | Routes voice + Discord into brain |
| main.py | not started | Ties everything together |

## GRUB State (desktop) — needs cleanup
- Theme: DISABLED (Valhalla caused silent black screen)
- GRUB_TERMINAL_OUTPUT=console (text mode)
- GRUB_CMDLINE_LINUX="nomodeset" — still present, should be removed
- Only one kernel: 6.19.10-200.fc43 (6.17.1 removed ✓)
- Goal: remove nomodeset, switch to gfxterm, apply Gorgeous-GRUB Matrix/Morpheus theme (Fedora + Windows version)

## CO1109 Coursework — Enron Assignment (DUE 27/04/2026 noon) ⚠️ URGENT
- Full notes in `Lecture Notes/CO1109/CO1109 Coursework — Enron Assignment.md`
- 5-min video (face on cam) + 2500 word report, one file via Blackboard
- Structure agreed: Mark-to-market → Cash flow monitoring | Shell companies → Entity verification | Andersen failure → Immutable audit trail
- Starting tomorrow (24/04)

## Priority Order (next session)
1. **Minecraft server** — boot the Aternos server and test it works clean (40 mods loaded)
2. **wake.py** — OpenWakeWord (stt.py written, not yet tested)
3. **Test stt.py** — Whisper STT on laptop
4. **input.py** — terminal text input
5. **main.py** — tie everything together
6. **Dad's Email Agent** — check if dad has Python on Mac, then build
7. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
8. **Plymouth boot animation**
9. **Gym Tracker Phase 2**
10. **Guide Tracker app** (for Lakira's dad — NOTE: dad is on Mac, not Windows)

## Caelestia Notes (desktop)
- Installed via EnceladusII/caelestia-fedora (abandoned Fedora fork, frozen Aug 2025)
- Quickshell installed via COPR (errornointernet/quickshell)
- Shell lives at ~/.config/quickshell/caelestia
- Hyprland config split across ~/.config/hypr/hyprland/*.conf
- User overrides go in ~/.config/caelestia/hypr-vars.conf and hypr-user.conf
- Keybinds at ~/.config/hypr/hyprland/keybinds.conf
- Bar is on the left (default)

## Laptop Plan (keep Waybar — iGPU can't handle full Quickshell bar)
- Tighten island layout, pill workspaces
- Add 1-2 lightweight Quickshell popups (music, calendar)
- Upgrade matugen pipeline to MatugenColors.qml live polling
- Configure Hypridle
- Keep Persona blade menu on laptop only

## Already Working on Laptop (don't redo)
- `Super+Q` → Persona Quickshell blade menu (POWER/STATS/CLAUDE)
- `Super+W` → wallpaper picker
- `Super+Shift+W` → cycle wallpaper
- `Super+Ctrl+B` → waybar style switcher
- `Super+Alt+B` → waybar layout switcher
- `Super+L` → hyprlock
- `Super+E` → Nautilus
- Power button left-click → wlogout
- `Super+D` → rofi app launcher
- `Super+Tab` → rofi window switcher
- Fish + spidey oh-my-posh prompt + fastfetch on startup
- Dynamic theming via matugen
- Dynamic papirus folder colors

## Game Setup Notes (laptop)
- Undertale: `bash /home/Lakira/Games/Undertale/launch.sh` (needs DISPLAY=:0, fuse-overlayfs)
- Wine+DXVK: `DISPLAY=:0 WINEDLLOVERRIDES="d3d11,dxgi=n" wine game.exe`
- jc141 native builds: need fuse-overlayfs, run start.n.sh from within game directory
- FitGirl repacks: `DISPLAY=:0 wine setup.exe`, install to ~/Games/
- Omori: IGG Windows build + Wine → ~/Games/OMORI
- Ender Magnolia: FitGirl + winetricks vcrun2022

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

## Gym Data Logged So Far
- Session 1: Pull Day — 17/03/2026 — BW 71kg
- Session 2: Push Day — 20/03/2026 — BW 72kg (clothes, no shoes)

## Dad's Email Agent (23/04/2026) — ALMOST DONE ⚠️
- For Lakira's dad (Lahiru), on **Mac**, email: laahiru@ttcsrilanka.com
- Script lives at: `/Users/laahirujayamanne/Documents/email_agent.py`
- User manual: `Email Agent Guide.md` (on Lakira's Desktop, needs sending over)
- Azure app registered ✓ (App: "Email Agent", single tenant)
- Permissions granted ✓ (Mail.Read, Mail.ReadWrite, Mail.Send)
- Dependencies installed on Mac ✓ (msal, requests, anthropic, Python 3.10)
- Microsoft auth flow working ✓ (device code, token cached)
- Email fetching working ✓ (fetches 30 unread emails)
- **BLOCKED: Anthropic API has no credits** — dad needs to add $5 minimum at console.anthropic.com → Plans & Billing
- Once credits added: run `python3 ~/Documents/email_agent.py` — works immediately, no setup needed

## Desktop Only
- **Guide Tracker app** — project for Lakira's dad (Mac, not Windows — correction from earlier).

## ilyamiro/nixos-configuration — Key Patterns Worth Stealing
1. Morphing master window
2. MatugenColors.qml live-polling
3. Focus time daemon (Python + SQLite)
4. DDG wallpaper search in picker
5. Calendar time-of-day color mapping
6. Workspace pills with staggered startup animation
7. Custom lock screen QML with Quickshell.Services.Pam
8. Plymouth: 80-frame animation + 80-frame progress sequence
