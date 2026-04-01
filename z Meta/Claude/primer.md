---
tags:
  - claude-memory
  - claude/status
---

# Project Primer

Current project status, what's in progress, what's next.

---

## Current Status
- **Hyprland on Fedora** — Fully working. SDDM fixed. ✓
- **Gym Tracker** — Phase 1 complete. Ready to start Phase 2 (storage.py).
- **Memory system** — Fully migrated to Obsidian vault (z Meta/Claude/). ✓
- **Obsidian vault** — Now the main base for Claude memory. Synced to GitHub. ✓
- **Laptop vault** — Moved to Documents/Obsidian/MyVault. Same path as Windows. ✓

## In Progress
- **Desktop rice plan** — Saving all GPU-heavy Quickshell stuff for desktop dual boot
- **Voice for Claude** — Discussed, not started. Leaning towards edge-tts or ElevenLabs. Against OpenAI TTS.

## Memory System — How It Works Now
- All memory lives in the vault at `z Meta/Claude/`
- Claude reads `lessons.md`, `primer.md`, `session-log.md` at session start
- Claude writes/commits/pushes the ObsidianVault repo at session end
- Obsidian Git plugin removed — Claude handles git
- Old `claude-memory` repo to be archived once both machines confirmed working
- Memory grows organically: core files stay flat, individual topics get their own notes as they grow

## After Vacation (from ~31 Mar 2026)
- Full month off uni — good time for big projects
- **Priority: Desktop dual boot** — Fedora + Hyprland, full Persona Quickshell rice on RX 6700XT
- Gym Tracker Phase 2 + 3
- Voice for Claude

## Still To Do
- **Archive claude-memory repo** — once laptop confirmed working off vault
- **Hypridle** — screen dim/lock/suspend timers not configured
- **Gaps & borders** — window spacing, border thickness
- **Plymouth boot animation** — custom frame-sequence animation (desktop only)
- **Desktop dual boot (Fedora)** — RX 6700XT, need to partition around 215GB games library

## Already Working (don't redo)
- Super+Q → Persona Quickshell blade menu (POWER/STATS/CLAUDE)
- Super+W → wallpaper picker
- Super+Shift+W → cycle wallpaper
- Super+Ctrl+B → waybar style switcher
- Super+Alt+B → waybar layout switcher
- Super+L → hyprlock
- Super+E → Nautilus
- Power button left-click → wlogout
- Super+D → rofi app launcher
- Super+Tab → rofi window switcher
- Fish + spidey oh-my-posh prompt + fastfetch on startup
- Dynamic theming via matugen
- Dynamic papirus folder colors
- Bibata-Modern-Ice cursor active

## Gym Tracker Build Phases
1. [x] Phase 1 — models.py (ExerciseSet, Session, Log)
2. [ ] Phase 2 — storage.py (save/load JSON)
3. [ ] Phase 3 — main.py (text menu)
4. [ ] Phase 4 — algorithms.py (overload, plateau, bodyweight trend)
5. [ ] Phase 5 — Polish

## Gym Data Logged So Far
- Session 1: Pull Day — 17/03/2026 — BW 71kg
- Session 2: Push Day — 20/03/2026 — BW 72kg (clothes, no shoes)
