Date:24-08-2025
Project: #jarvis
language: #python 
Related: [[1 Voice Assistant Overview]], [[3 Design Decisions]], [[4 Technology Selection]]
Tools used: []

# The 5 Essential Components

### 1. Wake word Detection

- What it does: Listens constantly for a trigger word.
- Why it's needed: so the assistant doesn't keep listening all the time
- The challenge: Must run 24/7 without killing CPU or battery
- How it works; Always listening in the background, only "wakes up" when it hears the trigger word.

### 2. Speech To Text (STT)

- What it does: Converts sound waves from your voice into written text
- Why it's needed: Computers understand text much better than audio
- The challenge: Handling difference accents, background noise, unclear speech, speaking fast/slow

### 3. Language Model (The "Brain")

- What it does: Understands the text and figures out how to respond. 
- Why it's needed: This is what makes it "intelligent" vs just a voice recorder
- The challenge: Being smart enough to be useful, fast enough for real conversation.

### 4. Text To Speech (TTS)

- What it does: Converts the response text back into natural sounding speech. 
- Why it's needed: For natural conversation, humans expect voice responses
- The challenge: Sounding human, not robotic, get the right tone and emotion.

### 5. Tools/Functions System

- What it does: Gives the assistant actual abilities beyond just chatting
- Why it's needed: Makes it practically useful
- The challenge; Knowing WHEN to use tools vs just answering from knowledge


# How they work together

```
Wake Word  ->  STT  ->  Brain  ->  (Maybe use tools)  ->  TTS  ->  Speak
```



