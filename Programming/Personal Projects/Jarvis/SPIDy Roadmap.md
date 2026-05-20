---
tags:
  - spidy
  - roadmap
  - ai
created: 2026-05-20
---

# SPIDy Roadmap — What's Missing to Feel Like JARVIS

## 🔴 Breaks Immersion Right Now

- **Response latency (7–30s)** — #1 priority. Tool calls trigger 3 LLM round-trips = 30s. Need faster casual-response path or smaller fast model for simple replies.
- **Two-sentence limit too rigid** — cuts off mid-thought or pads unnecessarily. Needs context-aware length, not a hard cap.

## 🟡 Missing "Individual Entity" Feeling

- **Proactive commentary** — SPIDy only speaks when spoken to. Should surface things unprompted: "I was reading about Deadlock's new patch" or "You've been at your desk 4 hours, sir."
- **Memory surfacing naturally** — 107 nodes in the brain but rarely woven into conversation unprompted. Should connect mentions to known facts without being asked.
- **Screen awareness** — `get_screen` tool exists but never used proactively. JARVIS always knew what Tony was working on.
- **Faster memory writes** — corrections like "it's GroundLink not GuideTracker" hit 3 LLM calls and take 26s. Needs a direct write path.

## 🟡 Personality Depth

- **Genuine pushback** — soul says he has opinions, but model almost never disagrees. JARVIS pushed back on Tony. SPIDy currently validates everything.
- **Running themes / inside references** — JARVIS had running jokes and referenced past events. SPIDy doesn't yet say "last week you mentioned X." Memory exists but isn't used for rapport.
- **Custom voice** — Thomas.wav is decent but generic. A voice trained on a specific character would make it feel like *his* AI.

## 🟢 Functional Gaps

- **Screenshot/link analysis + memory** — SPIDy currently refuses ("I can't retain data from images"). Should read a screenshot, extract facts, save to brain.
- **Music commentary** — media watcher tracks what's playing but SPIDy never comments on it or connects it to his knowledge of Lakira's taste.
- **Calendar as context** — MS Graph wired for reminders but schedule isn't used to proactively frame the day.
- **Self-code analysis** — SPIDy should be able to read its own source, analyse it, research improvements, and propose changes autonomously.

## Priority Order

1. Response speed
2. Proactive commentary
3. Memory surfacing in conversation
4. Screen/context awareness
5. Screenshot + link intelligence
6. Pushback / genuine opinions
7. Voice refinement
8. Calendar context
9. Self-directed improvement loop
