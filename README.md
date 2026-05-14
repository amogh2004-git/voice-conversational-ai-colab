# Voice Conversational AI (Google Colab )

I'm a final-year undergraduate student, and this project is my implementation of a **voice-based conversational AI pipeline**.  
The original company assignment asked for Whisper + Kokoro + Pipecat on RunPod.  
Due to budget limits, I built and tested the same **core architecture** on **Google Colab**:

- Speech-to-Text (STT) with **Whisper** (`faster-whisper`)
- Text generation with **Groq Llama 3.1**
- Text-to-Speech (TTS) with **Google TTS (gTTS)**

The goal is to show that I understand how to connect STT → LLM → TTS into a working conversational loop.

---

## What this project does

This repo contains one main notebook:

- `colab_voice_pipeline.ipynb`  
  A Colab notebook that runs the full pipeline:

  1. Load a Whisper model on GPU (Colab).
  2. Send text (simulating speech transcription) to a Groq LLM.
  3. Convert the LLM's reply to audio using Google TTS.
  4. Play the audio inside the notebook.

In a real deployment (e.g. RunPod), the same logic can be used with:

- Real microphone input → Whisper STT  
- A hosted LLM (Ollama/Groq/OpenAI/etc.)  
- Kokoro or another TTS engine  
- An HTTP or WebSocket API instead of a notebook

---

## How to run this on Google Colab

### Open the notebook

1. Open `whisper_kokoro_pipecat.ipynb` from this repo.
2. Click "Open in Colab" or upload it manually to Colab.

### Enable GPU

In Colab:

- Go to **Runtime → Change runtime type**  
- Set **Hardware accelerator = T4 GPU**  
- Click **Save**

---

## Notebook structure (step by step)

### Install dependencies

The first cell installs the libraries:

```python
!pip install --quiet ctranslate2
!pip install --quiet faster-whisper
!pip install --quiet gtts
!pip install --quiet groq
```

### Load Whisper

```python
from faster_whisper import WhisperModel

whisper_model = WhisperModel("small", device="cuda", compute_type="float16")
print("Whisper model loaded.")
```

### Configure Groq LLM

```python
from groq import Groq

client = Groq(api_key="YOUR_GROQ_API_KEY_HERE")
```

To get an API key:

1. Go to **https://console.groq.com**  
2. Sign up → API keys → Create key  
3. Paste the key in the notebook

### Full pipeline: text → LLM → audio

The final cell links everything:

```python
user_input = "Demonstrate a short voice AI response for my company project."

response = client.chat.completions.create(
    model="llama-3.1-8b-instant",
    messages=[
        {"role": "system", "content": "You are a concise voice assistant. Answer in under 20 words."},
        {"role": "user", "content": user_input},
    ],
    max_tokens=80,
    temperature=0.7,
)

llm_text = response.choices.message.content
print("LLM response:", llm_text)

audio_bytes = google_tts(llm_text)
display(Audio(audio_bytes, rate=24000))
```

---

## Relation to the original RunPod + Pipecat assignment

The company assignment asked for:

1. **Low-latency voice bot** (Whisper + Kokoro + Pipecat)  
2. **Research LLM with Ollama**  
3. **Browser agent using an 8B model**

This notebook focuses on **part 1** (voice pipeline) in a Colab-friendly way.

What I learned:

- How to load and run **Whisper** on GPU in Colab.  
- How to integrate a **remote LLM (Groq)** as the reasoning engine.  
- How to convert LLM text responses into **audio TTS** and play them.  
- How to keep responses short using system prompts and `max_tokens` to help with latency.

The same architecture can be moved to RunPod by:

- Installing these dependencies on a GPU pod  
- Replacing Google TTS with Kokoro TTS  
- Wrapping STT/LLM/TTS in a Pipecat-based streaming server

---

## Next steps / ideas

If I had more time or a proper GPU server, I would:

- Plug real audio input → Whisper → LLM → TTS for full voice-to-voice demo.  
- Replace gTTS with Kokoro or another local TTS.  
- Build a small FastAPI server around this logic to serve a frontend.

For now, this Colab prototype shows the main skills the assignment is testing:
- Using GPU for model inference  
- Calling LLM APIs  
- Connecting multiple AI components into one working pipeline
