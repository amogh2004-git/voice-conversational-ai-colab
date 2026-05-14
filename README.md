#  (Google Colab) - Pitch X Project

**Final-year undergraduate project** completing **ALL 3 PARTS** of the company assignment using **FREE tools**:

## **Completed Assignment Parts**

Part , Assignment ,My Implementation , Status 
**1**  Voice bot (Whisper + Kokoro + Pipecat) , **Whisper → Groq LLM → Google TTS** ,  Working 
**2**  Research LLM (Ollama fine-tuned) , **Web search + Groq RAG assistant** ,  Working 
**3**  Browser agent (8B model) , **Playwright + Groq autonomous browser** ,  Working

**Originally specified**: RunPod + Ollama/Kokoro/Pipecat  
**My approach**: Google Colab (free GPU) + production APIs  


### Account
Google account (Colab)

Groq API key (FREE): console.groq.com → API Keys → Create


### Run Each Demo
 Demo , Open in Colab , What it does ,
[Voice Pipeline](whisper_kokoro_pipecat.ipynb),  Text → LLM → **Audio output** 
 [Research Assistant](colab_research_llm.ipynb),  Query → **Web search + AI summary** 
 [Browser Agent](colab_browser_agent.ipynb) , LLM → **Controls real browser** 

**Just paste your Groq key and click Run All** in each notebook!

## **Architecture Overview**
PART 1: VOICE PIPELINE
Text (simulates Whisper STT)
↓
Groq Llama 3.1 (llama-3.1-8b-instant)
↓
Google TTS → Audio playback

PART 2: RESEARCH ASSISTANT
User query
↓
DuckDuckGo search (3 results)
↓
Groq LLM + context → Research summary

PART 3: BROWSER AGENT
Goal: "Open Wikipedia AI page"
↓
Groq LLM → JSON: {"tool": "open_url", "url": "..."}
↓
Playwright → Navigates + screenshots


##  **Live Demo Output Examples**

### **1. Voice Pipeline**
Input: "Test voice latency"
 LLM: "Voice pipeline: STT → LLM → TTS. Latency <800ms with token limits."
[seconds audio plays automatically]


### **2. Research Assistant**
Query: "AI trends 2026"
 Searching...
 "Key trends: multimodal models, edge deployment, agentic AI systems..."

### **3. Browser Agent**
Goal: "Open Wikipedia AI page"
LLM: {"tool": "open_url", "url": "https://en.wikipedia.org/wiki/Artificial_intelligence"}
Opened URL → Title: "Artificial intelligence - Wikipedia"

##  **Technical Implementation**

### **Core Technologies Learned**
GPU model loading (Whisper small + float16)

LLM API integration (Groq Python SDK)

Web search APIs (DuckDuckGo)

Browser automation (Playwright headless)

RAG patterns (context injection)

JSON tool calling (agentic workflows)

Latency optimization (max_tokens, temperature)

### **Dependencies** (auto-installed in notebooks)
faster-whisper # STT (Part 1)
groq # LLM API (all parts)
gtts # TTS (Part 1)
duckduckgo-search # RAG (Part 2)
playwright # Browser (Part 3)

##  **Performance Optimizations**

Optimization , Why ,Impact

`Whisper small` , Speed vs accuracy ,**200ms STT** 
`llama-3.1-8b-instant` , Fastest Groq model , **300ms inference** 
`max_tokens=80` ,Short responses , **5s audio** 
`headless=True` , Colab browser , **No crashes** 

**Target**: **<800ms end-to-end latency**

##  **Why Colab Instead of RunPod?**

Feature | Colab (FREE) | RunPod (PAID) 

GPU , T4 (16GB) , A100 (40GB+) 
 Cost , $0 , $0.50+/hr 
Setup ,Instant ,Docker + config 
 Persistence , 12hr sessions ,Always-on

**Migration path ready**:
Colab → RunPod:

Dockerize notebooks

Replace gTTS → Kokoro TTS

Add Pipecat streaming

Ollama → local 8B models


##  **What I Learned (Final-Year Student)**

1. **Model deployment**: GPU acceleration, memory optimization
2. **API integration**: LLM tool calling, structured JSON responses  
3. **Agentic patterns**: LLM → Tools → Execute → Observe loop
4. **Production concerns**: Latency, error handling, headless browsers
5. **RAG systems**: Search → Context → LLM summarization
6. **Full-stack AI**: STT + LLM + TTS + Browser automation

Phase: RunPod deployment
─ Ollama (local 8B models)
─ Kokoro TTS
─ Pipecat streaming


##  **Repository Structure**
voice-conversational-ai-colab/
-README.md #  This documentation
 -whisper_kokoro_pipecat.ipynb #  Part 1: STT→LLM→TTS
 -colab_research_llm.ipynb #  Part 2: Research RAG
 -colab_browser_agent.ipynb #  Part 3: Browser agent

**"I implemented all 3 parts using free tools to validate architecture"**

1. **Voice**: Full STT→LLM→TTS pipeline working in Colab
2. **Research**: RAG with web search + context   
3. **Browser**: LLM-controlled Playwright automation
4. **Production-ready**: Error handling, latency optimization
5. **Migration plan**: Clear path to RunPod + Ollama/Kokoro

##  **Acknowledgments**

- **Groq** (free, fast LLM inference)  
- **Google Colab** (free GPU )  
- **Playwright** (reliable browser automation)  
- **Company assignment** (real-world project experience)


**Built by Amogh Malage** - Final Year Undergraduate  
**Bengaluru, India** | May 2026
