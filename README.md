# 🎙️ Alex — Voice RAG Assistant

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python"/>
  <img src="https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi"/>
  <img src="https://img.shields.io/badge/Groq-LLM-FF6F00?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Google-Generative%20AI-4285F4?style=for-the-badge&logo=google"/>
  <img src="https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker"/>
  <img src="https://img.shields.io/badge/RAG-Enabled-blueviolet?style=for-the-badge"/>
</p>

<p align="center">
  <b>A lightweight Voice-enabled RAG assistant — ask questions, get intelligent answers, all with your voice.</b><br/>
  Built with FastAPI · Groq LLM · Google Generative AI · Speech I/O · Docker
</p>

---

## 🖥️ UI Preview

![UI Screenshot](https://github.com/user-attachments/assets/95567193-08a8-498b-ad08-c313720ec402)

> **What you see:** Alex's clean, minimal web interface where users can type or speak their questions. The assistant listens via the microphone button (Speech-to-Text), processes the query through the RAG pipeline, and speaks the answer back (Text-to-Speech) — all inside a single browser tab with no external dependencies for the end user.

---

## 📌 What is Alex?

**Alex** is a **Retrieval-Augmented Generation (RAG)** voice assistant. Instead of relying purely on an LLM's training data, Alex first **retrieves relevant context** from a local knowledge base (`sample.txt`), then feeds that context to **Groq's LLM** to generate a grounded, accurate response.

This means Alex answers from *your* documents — not hallucinated facts.

---

## ✨ Features

| Feature | Details |
|---|---|
| 🧠 RAG Pipeline | Retrieves from `sample.txt` before answering |
| ⚡ Groq LLM | Ultra-fast inference via Groq API |
| 🔢 Embeddings | Google Generative AI for semantic search |
| 🎙️ Voice Input | Speech-to-Text (speak your questions) |
| 🔊 Voice Output | Text-to-Speech (hear the answers) |
| 🌐 Web UI | Clean HTML + CSS + JS frontend |
| 🚀 FastAPI | Lightweight Python backend |
| 🐳 Docker | Fully containerized for easy deployment |
| 🔐 Env Config | API keys safely managed via `.env` |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        USER                                  │
│              (speaks or types a question)                    │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              Web UI  (index.html + JS)                       │
│     Speech-to-Text input  ←→  Text-to-Speech output         │
└───────────────────────────┬─────────────────────────────────┘
                            │  HTTP POST /chat
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              FastAPI Backend  (main.py)                      │
│              Routes, validation, response handling           │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              RAG Engine  (rag_engine.py)                     │
│   1. Embeds query → Google Generative AI                     │
│   2. Retrieves top chunks from sample.txt                    │
│   3. Builds prompt with context                              │
└──────────┬────────────────────────────────────┬─────────────┘
           │                                    │
           ▼                                    ▼
┌──────────────────────┐            ┌──────────────────────────┐
│  Google Generative   │            │     Groq LLM API         │
│  AI (Embeddings)     │            │  (Final answer generation)│
└──────────────────────┘            └──────────────────────────┘
                            │
                            ▼
                    Response → UI → 🔊 Spoken aloud
```

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | Serves the frontend web UI |
| `POST` | `/chat` | Accepts a question, returns AI response |

---

## 📁 Project Structure

```
📦 Alex-Voice-RAG-Assistant
 ┣ 📄 main.py               # FastAPI app entry point
 ┣ 📄 rag_engine.py         # Core RAG pipeline (embed + retrieve + generate)
 ┣ 📄 voice_agent.py        # Speech-to-Text & Text-to-Speech logic
 ┣ 📄 process.py            # Document processing & chunking
 ┣ 📄 cli.py                # CLI interface for terminal usage
 ┣ 📄 index.html            # Frontend web UI
 ┣ 📄 sample.txt            # Local knowledge base
 ┣ 📄 requirements.txt      # Python dependencies
 ┣ 📄 Dockerfile            # Docker build config
 ┣ 📄 docker-compose.yml    # Docker Compose setup
 ┣ 📄 .env.example          # Environment variable template
 ┣ 📄 .gitignore
 ┗ 📄 README.md
```

---

## 🚀 Installation & Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/ujjwal540/Alex-Voice-RAG-Assistant.git
cd Alex-Voice-RAG-Assistant
```

### 2️⃣ Create a Virtual Environment

```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

### 4️⃣ Configure Environment Variables

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key_here
GOOGLE_API_KEY=your_google_genai_api_key_here
```

> 💡 Get your **Groq API key** at [console.groq.com](https://console.groq.com)  
> 💡 Get your **Google API key** at [aistudio.google.com](https://aistudio.google.com)

### 5️⃣ Run the App

```bash
uvicorn main:app --reload --port 8000
```

Then open your browser at: **[http://127.0.0.1:8000](http://127.0.0.1:8000)**

---

## 🐳 Docker Deployment

### Build & Run with Docker

```bash
# Build the image
docker build -t alex-rag .

# Run the container
docker run --rm -p 8000:8000 --env-file .env alex-rag
```

### Or use Docker Compose

```bash
docker-compose up --build
```

---

## 💬 Example Interaction

```
🧑 User:   "What is Artificial Intelligence?"

🤖 Alex:   "Artificial Intelligence is the simulation of human
            intelligence processes by machines, especially
            computer systems. It includes learning, reasoning,
            and self-correction."
```

---

## 🔮 Future Improvements

- [ ] 📂 **Multi-document upload** — support PDF, DOCX, and web pages
- [ ] 🗃️ **Vector database** — integrate FAISS or Pinecone for scalability
- [ ] 🧠 **Chat memory** — maintain conversation history across turns
- [ ] ☁️ **Cloud deployment** — deploy to AWS, Render, or Vercel
- [ ] 📊 **Analytics dashboard** — track queries, latency, and usage
- [ ] 🔍 **Hybrid search** — combine keyword + semantic retrieval
- [ ] 🌍 **Multi-language support** — extend voice support beyond English

---

## 🛠️ Tech Stack

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/Groq-FF6F00?style=flat-square"/>
  <img src="https://img.shields.io/badge/Google%20AI-4285F4?style=flat-square&logo=google&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white"/>
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black"/>
</p>

---

## 👨‍💻 Author

<p align="center">
  <b>Ujjwal Kumar Karn</b><br/>
  🤖 AI & Machine Learning Enthusiast | Aspiring AI Engineer<br/><br/>
  <a href="https://github.com/ujjwal540">
    <img src="https://img.shields.io/badge/GitHub-ujjwal540-181717?style=for-the-badge&logo=github"/>
  </a>
</p>

---

<p align="center">
  <i>⭐ If you found Alex useful, drop a star — it helps a lot!</i>
</p>
