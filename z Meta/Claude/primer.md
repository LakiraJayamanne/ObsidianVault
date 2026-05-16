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

### Brain routing (REVISED 15/05/2026 — locked in)
1. Desktop on + Ollama reachable + VRAM > 6GB → qwen3:8b on RX 6700 (free, private, primary)
2. Desktop off / unavailable → NVIDIA NIM (free, 40 RPM, 100+ models, OpenAI-compatible)
3. NIM rate-limited or complex task → Claude API (last resort only)
- **Why:** Claude Sonnet at real usage = £25-35/month. Desktop GPU is free. NIM is free.
- Total running cost: ~£1.50-3/month (Pi electricity + occasional Claude API)

### Users
- Lakira — main (voice + phone + Apple Watch)
- Brother — GCSE homework help via web UI
- Dad — occasional, has Claude desktop for work

### UI — IN PROGRESS ⚡
- **Design:** HUD-style + Apple glass hybrid. Black (#080808) + deep crimson red (#C0001A)
- **Stack:** Next.js + Tailwind + Framer Motion
- **WHERE:** `/home/lakira/Documents/Projects/SPIDy/ui/` — GitHub: LakiraJayamanne/SPIDy

#### BUILT (15/05/2026 — session 81)
- Full MemoryGraph with 4 modes: idle (sphere, word-count glow, recency boost), listening (implode), speaking (explode + real RMS), thinking (Bohr atom, smoothstep entry, central node pulse)
- Bloom: threshold 0.1, intensity 1.4. Thinking nodes flat (emissive 0.8, no bloom). Central node pulses 2–8.
- `ws_server.py` — WebSocket on localhost:8765, broadcasts mode/rms/speech, receives text queries
- `main.py` — full state machine: wake→listening→thinking→speaking→listening. Stop phrases. Text input worker thread. interruptible=False for text queries
- `tts.py` — streams real RMS every 50ms to frontend while speaking
- `tools.py` — get_health (contextual comments, step goal awareness), get_health_trends (90-day history)
- `intent.py` — health routes added (BROKEN — too greedy, catches "heart" in any sentence). Needs tighter regex next session
- `brain.py` — get_health/_trends in _RESPONSES (skip 2nd LLM call). Health queries now ~1-2s
- `VoiceBar.tsx` — bigger input (480px), no equaliser, DPI fix, dev toggle button (⌥)
- `page.tsx` — lastSpeech display above input bar, sendQuery wired, rms passed to MemoryGraph
- `vault/route.ts` — wordCount + mtime per node, content read once (no double-read)
- `health/route.ts` — force-dynamic, appends to health-history.json on POST
- venv activate script fixed (was pointing to old MyPersona path)
- wake.py model path fixed (same issue)

#### DONE SESSION 83 (16/05/2026)
- Spotify now-playing: switched from Spotify Web API to playerctl/MPRIS (`/api/nowplaying` route)
- intent.py: health regex tightened, now_playing regex fixed (was catching "what's on my screen")
- main.py: text query → idle after responding. finally block guarantees reset.
- wake.py: 3-bug fix. Silero VAD gate added.
- stt.py: VAD tuned for voice commands
- Modelfile: num_ctx 8192→2048, num_predict 1024→256
- **Sentence streaming** — tts.py split into synthesize() + play_audio(). main.py _respond() pipelines synth N+1 while playing N. stop_event fixes thread-leak on interrupt. Double idle broadcast bug fixed.
- **Screen awareness** — get_screen(question) in tools.py. grim (Wayland) → resize to 1280px via magick → base64 → gemma3:4b via Ollama REST. Prompt tuned for 1-2 spoken sentences, no markdown. Ack fires in intent routing path (was missing). gemma3:4b pulled and working.
- **Sleep tracking fixed** — iOS Shortcuts rebuilt: Find Health Samples (Sleep, Asleep, today), loop End-Start per segment, sum minutes ÷ 60. Source filter added to stop iPhone+Watch double-counting. 7h 6m displaying correctly.
- **Steps fixed** — removed Limit 1, added source filter. 13,539 steps correct.
- **Gym calendar fixed** — anchor moved to 16/05/2026 (today = Upper). Tomorrow = Lower.
- **Vault node CRUD** — 4 new tools: search_nodes, read_node, create_node, append_node. Intent patterns + brain.py wiring. JARVIS can now search, read, create, append vault nodes via voice.
- **MemoryGraph search filter** — type any letter on the graph to enter search mode. Non-matching nodes fade to near-invisible, matching nodes stay bright with labels. Overlay shows query + match count. Escape/Backspace to clear.
- Google Antigravity IDE logged to vault: `Programming/Tools/Google Antigravity IDE.md`
- Local checkpoint: git commit cd56453 (NOT pushed to GitHub)

#### DONE SESSION 84 (17/05/2026)
- **qwen3:1.7b** — pulled and switched. Modelfile: `FROM qwen3:1.7b`, `num_predict 128`, `num_ctx 2048`. SystemPanel label updated. Faster TTFT confirmed.
- **MemoryGraph: single-click focus, double-click open** — single click (220ms debounce) = focus node. Double click = open content panel. Drag detection (>5px threshold) prevents orbit from clearing focus.
- **Controlled component: focusedNodeId as prop** — MemoryGraph no longer holds internal focus state. Parent (page.tsx) owns focus via `focusedNodeId` prop + `onFocusChange` callback. Fixed desync bug where white node showed but FOCUS label didn't.
- **Color swap** — default node: red (#C0001A). Focused node: white (#ffffff) with higher glow intensity.
- **Focus WS pipeline** — frontend sends `{type: "focus", node: id}` via sendFocus(). ws_server.py stores `_current_focused_node`. Voice path passes it to _respond(). Text query path passes it in dict through _query_queue.
- **Focused node read shorthand** — brain.py: if focused_node set and user says "read this / read the highlighted file / show me this / etc." → read_node(focused_node) → strip markdown → LLM summarise → speak.
- **Focus context injection** — for general LLM queries, focused node content is prepended to user message.
- **Intent routing fixes** — read_node pattern moved BEFORE read_notes. Negative lookahead on read_notes. "read this" removed from clipboard pattern (was stealing focused-node reads).
- **wake.py audio gate** — `if audio_state.speaking.is_set(): return` in audio_callback. Prevents TTS speaker audio from triggering wake word.
- **soul.md brevity** — strengthened: hard cap 30 words, 2 sentences max, no volunteering extra info.
- **FOCUS label in UI** — `FOCUS: {nodeName} ✕` shown above VoiceBar when node focused. ✕ clears focus.

#### DONE — Session 84 final state (17/05/2026 late)
**All changes pushed to GitHub. Last commit: 31f8cc2**

### Architecture change (MAJOR — done by overnight agent)
Switched from keyword-routing + LLM-fallback to **pure LLM-first tool-use**:
- `intent.route()` removed from `think_with_tools()` — LLM always decides
- `_select_tools()` now returns ALL tools every time (LLM picks freely)
- Removed `_TOOL_KEYWORDS`, `_ALWAYS_INCLUDE`, `_MAX_TOOLS` (~50 lines of dead code)
- Focused-node shorthand removed — node content is now markdown-stripped and injected into LLM context directly
- Net: every query goes to Ollama → LLM picks tool or answers directly → tool result formatted by `_RESPONSES`

### Other fixes this session
- `_is_stop()` ignores questions ending with `?` — "Should I go to sleep?" no longer triggers standby
- `_current_focused_node` persisted to `.focus_state.json` — survives backend restarts
- stdout/stderr tee'd to `spidy.log` for persistent debug trace
- `think=False` + `num_predict 512` on main LLM call

### What to test when you wake up
1. Restart backend (`python main.py` from SPIDy dir in .venv)
2. Say "what time is it?" — LLM should call `get_time` tool
3. Focus a node, say "read this" — LLM gets injected content, should summarize
4. Say a general question — should answer without tool
5. Check `spidy.log` for `[brain] all tools passed to LLM for:` traces
6. If any tool call fails, check `spidy.log` for the tool name and args the LLM chose

### Known tradeoff
Pure LLM routing adds ~150-200ms vs scripted routing. Acceptable given 800ms STT overhead.

#### NEXT (after fixing above)
- Test other voice features: personality dials, echo detection, heartbeat
- **`OLLAMA_FLASH_ATTENTION=1`** — confirmed ROCm regression with Qwen3 (GitHub #12432). Test carefully.
- **Swap STT to Moonshine Small** — when Pi arrives (527ms vs 10,400ms)
- **Train "Hey SPIDy" wake word** — CoreWorxLab/openwakeword-training, Kokoro synthetic data
- Tauri packaging (when UI is feature-complete)

### Full architecture doc
`Programming/Personal Projects/Jarvis/Homelab & JARVIS Architecture.md`

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
2. **SPIDy — test qwen3:1.7b** — benchmark vs qwen3:8b for tool calls, sub-1s TTFT
3. **SPIDy — sentence streaming in tts.py** — synthesise N+1 while N plays, 40-60% latency drop
4. **SPIDy — screen awareness** — gemma3:4b (multimodal), not yet specced
5. **SPIDy — custom "Hey SPIDy" wake word** — CoreWorxLab/openwakeword-training, Kokoro synthetic data
6. **SPIDy — Moonshine Small STT** — when Pi arrives (527ms vs 10,400ms)
7. **SPIDy — Tauri packaging** — when UI is feature-complete
8. **Gym Tracker** — rebuild later, SPIDy-integrated (trends + progressive overload via SPIDy brain/tools)

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

## Gym Tracker — SCRAPPED (16/05/2026)
Standalone CLI version scrapped. Will be rebuilt as a SPIDy-integrated feature — log workouts via voice/text, trend analysis and progressive overload suggestions routed through SPIDy's brain/tools layer. Reference: tracked.gg (by Keenan). RIR rating, weekly volume tracking still planned for the rebuild.

---

## Dad's Email Agent (23/04/2026) — BLOCKED ⚠️
- For Lakira's dad (Lahiru), on **Mac**, email: laahiru@ttcsrilanka.com
- Script lives at: `/Users/laahirujayamanne/Documents/email_agent.py`
- **BLOCKED: Anthropic API has no credits** — dad needs to add $5 minimum at console.anthropic.com → Plans & Billing
