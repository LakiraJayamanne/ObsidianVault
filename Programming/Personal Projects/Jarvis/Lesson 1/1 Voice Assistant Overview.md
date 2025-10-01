Date:24-08-2025
Project: #jarvis 
language: #python
Related: [[2 Component Breakdown]], [[3 Design Decisions]]
Tools used: []

# The Core Loop

- Every voice assistant follows the same pattern:

```
1. Listen for wake word ("Jarvis")
2. Record Speech
3. Speech To Text (STT)
4. Process with AI 
5. TTS 
6. Play Audio
7. Loop back to step 1
```

- Examples: Siri, Alex, etc.

# The Key Insight

- The loop is simple. The complexity is in HOW you implement each step:
	- Step 1: How to detect wake word efficiently?
	- Step 2: How accurate is the STT?
	- Step 3: How smart is the AI? How fast is the response time?
	- Step 4: How natural does the voice sound?

# Why the loop matters

- Understanding the loop helps:
	- Debug problems (which step is failing)
	- Optimise performance (which step is slow)
	- Add new features (modify specific steps)
	- Learn other voice assistants


# The Goal

- Build this loop *locally*. No internet required.