---
tags:
  - spidy
  - research
  - voice-assistant
  - jarvis
date: 2026-05-16
---

# SPIDy Stack Improvements — Research Report

> Researched overnight 15–16 May 2026. Current stack benchmarked against 2025–2026 alternatives.
> Related: [[Homelab & JARVIS Architecture]]

---

## Executive Summary

- **Swap STT to Moonshine Small** — 527ms on Pi 5 vs ~10,400ms for Whisper Small. Biggest single win.
- **Swap TTS to Piper on Pi 5** — Kokoro is sub-real-time on Pi 5 CPU. Piper runs 15× real-time on the same hardware.
- **Fix sentence streaming** — synthesise sentence N+1 while N plays. 40–60% latency reduction with zero model changes. Low effort, high impact.
- **Train custom "Hey SPIDy" wake word** — `CoreWorxLab/openwakeword-training` uses Kokoro (which we already have) for synthetic data.
- **Set `OLLAMA_FLASH_ATTENTION=1`** — cuts qwen3:8b inference time up to 75%, frees ~5GB VRAM. One env var.

---

## STT

**Current:** faster-whisper small.en int8, CPU, ~800ms–1.5s latency on desktop. ~10,400ms on Pi 5.

**Winner: Moonshine Small (Useful Sensors)**
- Pi 5 CPU benchmarks: Tiny=237ms/12% WER, Small=527ms/7.84% WER, Base=802ms/6.65% WER
- Whisper Small takes ~10,400ms on same hardware — 20× slower
- Streaming-capable, Apache 2.0
- `pip install moonshine-voice`
- Repo: https://github.com/usefulsensors/moonshine

**Desktop GPU option: Parakeet TDT 0.6B v3 (NVIDIA)**
- 6.34% WER, RTFx ~3386 on GPU — SOTA accuracy
- Worth running server-side on the RX 6700 if STT ever moves off Pi
- https://huggingface.co/nvidia/parakeet-tdt-0.6b-v2

**Recommendation:** Switch to Moonshine Small on Pi 5. Keep faster-whisper on desktop for now.

---

## TTS

**Current:** Kokoro ONNX (bm_lewis), fully local. Great on desktop GPU (96× real-time on RX 6700). Sub-real-time on Pi 5 CPU.

**Pi 5: Switch to Piper TTS**
- 15× real-time on Pi 5 Cortex-A76
- `en_US-ryan-high` is the closest British-adjacent high-quality voice
- `pip install piper-tts`
- https://github.com/rhasspy/piper

**Desktop: Keep Kokoro (bm_lewis)** — it's excellent here.

**Future: Orpheus TTS**
- 3B model, Apache 2.0, emotional tags (`[laugh]`, `[chuckle]`, `[sigh]`)
- Zero-shot voice cloning
- Needs 6–8GB VRAM → desktop-only
- https://github.com/canopyai/Orpheus-TTS

**Immediate high-impact fix (no model swap needed):**
The current code generates the entire audio clip before playback starts. Fixing the sentence-streaming loop so Kokoro/Piper synthesises sentence N+1 while sentence N plays cuts perceived latency 40–60% with zero model changes. This should be done before any model swap.

---

## Wake Word

**Current:** openwakeword with `hey_jarvis_v0.1.onnx`

**Best option: Train custom "Hey SPIDy" model**
- `CoreWorxLab/openwakeword-training` uses Kokoro for synthetic data generation — which we already have
- ~13,000 synthetic utterances + 20–50 real recordings
- One-time 4–8 hour GPU training job on the RX 6700
- End result: proper "Hey SPIDy" wake word, no more JARVIS branding
- https://github.com/CoreWorxLab/openwakeword-training

**Porcupine (Picovoice):**
- Cannot do custom wake words on Pi without enterprise licence. Not worth it.

**Recommendation:** Train the custom model. Already planned, just needs to be prioritised.

---

## LLM Routing

**Current:** qwen3:8b via Ollama on RX 6700 (ROCm), NVIDIA NIM fallback, Claude API last resort.

**qwen3:8b is well chosen.** Immediate improvements:

1. **`OLLAMA_FLASH_ATTENTION=1`** — cuts inference time up to 75%, frees ~5GB VRAM. Set in the Ollama systemd override. Do this first.
2. **Add qwen3:1.7b as Tier 2** — simple conversational turns (time, weather, chit-chat) don't need 8B. Route short/simple queries to 1.7b, use 8b for anything complex.
3. **Semantic response cache** — 60-second TTL cache for repeated queries (time, weather, health status). Skip Ollama entirely for hits.
4. **Speculative decoding** — 1.7B draft + 8B verifier gives 2–3× throughput but requires llama.cpp server instead of Ollama. Leave for later.

---

## Latency Budget

**Current estimated total to first audio: 2–5 seconds**
**Target after improvements: 800ms–1.5s**

| Stage | Current | After fix | Saving |
|---|---|---|---|
| Wake word detection | ~50ms | ~50ms | — |
| STT (Pi 5) | ~1,500ms | ~527ms | ~1,000ms |
| LLM first token | ~500–1,500ms | ~300–800ms | ~500ms |
| TTS synthesis | ~300–800ms | streaming | ~400ms perceived |
| Audio device start | ~50ms | ~20ms | ~30ms |

**Biggest individual wins:**
- STT swap: saves ~1,000ms on Pi 5
- Sentence streaming: saves 40–60% perceived response time
- VAD fix: saves ~300ms silence padding
- Replace `subprocess.Popen(["mpv", ...])` with `sounddevice.play()` directly: saves 30–50ms per utterance

---

## VAD & Other Improvements

**Silero VAD**
- Already in faster-whisper via `vad_filter=True`
- Should replace energy-threshold silence counting in `stt.py` for standalone end-of-speech detection
- Saves ~300ms per turn
- https://github.com/snakers4/silero-vad

**RealtimeSTT (KoljaB)**
- Pre-built drop-in wrapping Silero VAD + Moonshine/Whisper + realtime partials
- Worth evaluating as a full stt.py replacement
- https://github.com/KoljaB/RealtimeSTT

**Memory improvements**
- Add FAISS or sqlite-vec embedding index for semantic deduplication of facts in memory.md
- Add conversation summary compression every 10 turns (summarise older context, keep recent verbatim)

---

## Suggested but Not Applied

These were found but left for Lakira to decide:

- **Speculative decoding (1.7B + 8B)** — requires moving from Ollama to llama.cpp server. Big architectural change.
- **Orpheus TTS** — great expressiveness but 3B model, needs proper integration and voice selection.
- **RealtimeSTT as full stt.py replacement** — opinionated library, replaces the current clean custom code. Worth evaluating but not a drop-in.
- **FAISS memory index** — meaningful but requires schema design decisions.

---

## Prioritised Action List

Given Pi 5 + RX 6700 setup, in order of impact vs effort:

1. **`OLLAMA_FLASH_ATTENTION=1`** — one env var, massive win. Do this now.
2. **Fix sentence streaming in tts.py** — 40–60% latency drop, no model change.
3. **Swap STT to Moonshine Small** — 20× faster on Pi 5.
4. **Swap TTS to Piper on Pi 5** — Kokoro is unusable at real-time on Pi CPU.
5. **Add Silero VAD to stt.py** — cleaner end-of-speech, saves 300ms.
6. **Add qwen3:1.7b as Tier 2** — faster simple replies.
7. **Train "Hey SPIDy" wake word** — custom model via CoreWorxLab/openwakeword-training.
8. **Semantic response cache** — skip LLM for repeated queries.
