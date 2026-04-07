---
tags:
  - jarvis
  - programming
  - python
---

# wake.py — How It Works

Reference guide for building `wake.py`. Read this alongside the code.

---

## What this file does

Sits in the background permanently, listening to a continuous audio stream. Every small chunk of audio gets scored by OpenWakeWord. When the score crosses a threshold, it calls a callback function — telling the rest of JARVIS to wake up and start listening properly.

---

## Imports

```python
import openwakeword
from openwakeword.model import Model
import sounddevice as sd
import numpy as np
```

- `openwakeword` — the wake word detection library
- `Model` — the class that loads and runs the wake word model
- `sounddevice` — same as stt.py, used to capture mic audio
- `numpy` — used to handle the raw audio data as arrays

---

## Loading the model

```python
model = Model(wakeword_models=["hey_jarvis"], inference_framework="onnx")
```

- `wakeword_models` — list of wake words to listen for. `"hey_jarvis"` is a pre-trained model that ships with OpenWakeWord.
- `inference_framework="onnx"` — the format the model runs in. ONNX is cross-platform and runs on CPU without needing GPU drivers or CUDA.

This is done at module level (outside any function) so it loads once at startup and stays in memory — same reason as `whisper.load_model()` in stt.py.

---

## The listen() function

This is the main function. It takes one argument: `on_wake` — a **callback function**.

### What is a callback?
A callback is a function you pass into another function, to be called later when something happens. Here, `on_wake` is a function that gets called the moment the wake word is detected. `wake.py` doesn't need to know what `on_wake` does — that's decided by whoever calls `listen()`.

Example: `listen(on_wake=start_recording)`

---

## The audio stream

```python
def audio_callback(indata, frames, time, status):
    ...
```

`sd.InputStream` works differently from `sd.rec()` in stt.py.

- `sd.rec()` — records for a fixed duration then stops
- `sd.InputStream` — runs forever, calling `audio_callback` every time a new chunk of audio is ready

`audio_callback` receives:
- `indata` — numpy array of the latest audio chunk
- `frames` — number of samples in this chunk
- `time` / `status` — metadata, mostly ignored

---

## Chunk size and sample rate

```python
chunk_size = 1280
sample_rate = 16000
```

- `sample_rate = 16000` — same as stt.py. OpenWakeWord also expects 16kHz audio.
- `chunk_size = 1280` — number of samples per chunk fed to the model. This is the value OpenWakeWord recommends. At 16kHz, 1280 samples = 80ms of audio per chunk.

---

## Scoring and threshold

Inside `audio_callback`, after feeding the chunk to the model:

```python
scores = model.predict(indata.flatten())
score = scores["hey_jarvis"]
```

- `model.predict()` takes the audio chunk and returns a dict of scores, one per wake word
- The score is a float between 0.0 and 1.0 — confidence that the wake word was just said

```python
threshold = 0.5
if score > threshold:
    on_wake()
```

- If confidence is above 0.5, fire the callback
- 0.5 is a reasonable starting point — tune it up if you're getting false triggers, down if it's missing you

---

## Opening the stream

```python
with sd.InputStream(samplerate=sample_rate, channels=1, dtype="float32",
                    blocksize=chunk_size, callback=audio_callback,
                    device=config.input_device):
    while True:
        pass
```

- `sd.InputStream` opens the mic and starts calling `audio_callback` on every chunk
- `while True: pass` keeps the function alive indefinitely — without this, the stream would open and immediately close
- The `with` block ensures the stream is properly closed if the program exits or crashes

---

## Test block

```python
if __name__ == "__main__":
    print("Listening for wake word...")
    def on_wake():
        print("Wake word detected!")
    listen(on_wake)
```

- Defines a simple `on_wake` that just prints a message
- Passes it into `listen()` to test detection
- Say "hey jarvis" and it should print "Wake word detected!"

---

## Summary — what you're writing

1. Imports
2. Load the model at module level
3. Define `listen(on_wake)` function
4. Inside it, define `audio_callback(indata, frames, time, status)` that scores each chunk and calls `on_wake()` if above threshold
5. Open `sd.InputStream` with that callback and loop forever
6. Test block at the bottom
