---
tags:
  - jarvis
  - programming
  - python
---

# stt.py — How It Works

Reference guide for `stt.py`. Read this alongside the code.

---

## What this file does

Records audio from the microphone for a fixed duration, then passes it through Whisper to convert it to text. Returns the transcribed string.

---

## Imports

```python
import whisper
import sounddevice as sd
import numpy as np
import config
```

- `whisper` — OpenAI's open source speech recognition model, runs fully locally
- `sounddevice` — captures audio from the microphone
- `numpy` — handles raw audio data as arrays
- `config` — project settings (model name, timeout, input device)

---

## Loading the model

```python
model = whisper.load_model(config.stt_model)
```

Done at module level — outside any function. Loading a model means reading the weights from disk into memory. It takes a few seconds and would be wasteful to repeat every time we transcribe. By doing it here, it happens once at startup and stays in RAM.

`config.stt_model` is `"base"` — a balance of speed and accuracy for local use.

---

## Sample rate

```python
sample_rate = 16000
```

Whisper was trained on audio at 16,000 samples per second (16kHz). If you feed it audio at a different sample rate it will misinterpret the timing of sounds and produce bad output. This value is set inside `listen()` and used throughout.

---

## Recording with sd.rec()

```python
audio = sd.rec(
    int(config.timeout * sample_rate),
    samplerate=sample_rate,
    channels=1,
    dtype="float32",
    device=config.input_device
)
```

- `int(config.timeout * sample_rate)` — total number of samples to capture. e.g. timeout=5, sample_rate=16000 → 80,000 samples (5 seconds of audio)
- `samplerate=sample_rate` — capture at 16kHz to match Whisper's expectation
- `channels=1` — mono audio. Whisper doesn't use stereo, so two channels would just waste memory
- `dtype="float32"` — audio values stored as 32-bit floats in range [-1.0, 1.0]. Whisper expects float32, so we capture in this format directly
- `device=config.input_device` — which microphone to use. `None` = system default

---

## sd.wait()

```python
sd.wait()
```

`sd.rec()` starts recording in a background thread and returns immediately. `sd.wait()` blocks here until that recording thread finishes. Without this, the next line would run before recording is done.

---

## Flattening the audio

```python
audio = audio.flatten()
```

`sd.rec()` returns a 2D numpy array with shape `(num_samples, num_channels)` — e.g. `(80000, 1)` for 5 seconds of mono audio. Whisper expects a 1D array with shape `(num_samples,)`. `.flatten()` collapses the channel dimension: `(80000, 1)` → `(80000,)`.

---

## Transcribing

```python
result = model.transcribe(audio, fp16=False)
```

- Passes the raw audio array directly to Whisper
- Whisper handles everything internally: FFT, mel spectrogram, transformer inference
- `fp16=False` — disables half-precision floating point. FP16 runs faster on GPUs that support it, but causes errors on CPU and most iGPUs

---

## Return value

```python
return result["text"].strip()
```

`result` is a dict. `result["text"]` is the full transcription as a string. `.strip()` removes any leading/trailing whitespace or newlines Whisper sometimes adds.

---

## Test block

```python
if __name__ == "__main__":
    print("Listening...")
    text = listen()
    print(f"You said: {text}")
```

Only runs when you execute `stt.py` directly. Won't run when imported by another file. Used to test in isolation.
