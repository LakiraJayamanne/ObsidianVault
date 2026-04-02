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
- **Voice Assistant** — Stack decided. Not started. Waiting on desktop setup.

## In Progress
- **Desktop dual boot** — MID INSTALL. Stopped at partition step. See below.

## Desktop Dual Boot — Current State (02/04/2026)
- Drive: Kingston 1TB NVMe, one C: partition (~930GB), 441GB free
- Motherboard: ASRock B660M Pro RS — boot menu key: **F11**
- Fedora 43 ISO flashed to USB with Rufus (GPT, UEFI)
- Fast Startup disabled (`powercfg /h off` done)
- Windows Disk Management couldn't shrink (only 7.7GB available — unmovable files blocked it)
- **Next step: boot from USB (F11), choose "Try Fedora", open GParted, shrink C: by 100GB, then run installer**

## Priority Order
1. **Desktop dual boot** — IN PROGRESS (see above)
2. **claw-code** — get it set up
3. **Desktop rice** — full Quickshell setup on desktop
4. **Voice assistant** — build starts after above three

## Voice Assistant — Stack Locked (01/04/2026)
| Component | Choice |
|---|---|
| Wake word | Porcupine (Picovoice) — wake word: "Persona" |
| STT | Whisper (local) |
| Brain | claw-code |
| TTS | edge-tts |

- Cross-platform: Windows + Linux
- Wake word name TBD (will be the assistant's name)
- Don't build/test on laptop — iGPU can't handle Whisper well. Use desktop (RX 6700XT).
- Old JARVIS project notes archived in vault at `Programming/Personal Projects/Jarvis/Old Notes (Aug 2025).md`

## Memory System — How It Works Now
- All memory lives in the vault at `z Meta/Claude/`
- Claude reads `lessons.md`, `primer.md`, `session-log.md` at session start
- Claude writes/commits/pushes the ObsidianVault repo at session end
- Obsidian Git plugin removed — Claude handles git
- Old `claude-memory` repo to be archived once both machines confirmed working

## Still To Do
- **Archive claude-memory repo** — once laptop confirmed working off vault
- **Hypridle** — screen dim/lock/suspend timers not configured
- **Gaps & borders** — window spacing, border thickness
- **Plymouth boot animation** — custom frame-sequence animation (desktop only)

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
