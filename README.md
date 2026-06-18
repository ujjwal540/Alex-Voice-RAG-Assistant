# Alex — Voice RAG Assistant (Nepal)

A lightweight Retrieval-Augmented Generation (RAG) voice assistant built with FastAPI, Groq LLM, and Google Generative AI.  
It answers questions from a local knowledge base (sample.txt) with optional voice input and speech output support.

---

## Features

- RAG-based question answering over local documents (sample.txt)
- FastAPI backend for API handling
- Simple web UI (HTML, CSS, JavaScript)
- Speech-to-Text voice input support
- Text-to-Speech response output
- Embeddings using Google Generative AI
- LLM responses using Groq API
- Docker support for deployment
- Environment-based API key configuration

---

## UI Preview

![<img width="917" height="852" alt="image" src="https://github.com/user-attachments/assets/95567193-08a8-498b-ad08-c313720ec402"] />

---

## System Architecture

User  
→ Web UI (HTML + JS)  
→ FastAPI Backend (main.py)  
→ RAG Engine (rag_engine.py)  
→ Embeddings (Google Generative AI)  
→ LLM (Groq API)  
→ Response returned to UI  

---

## API Endpoints

- GET / → Load frontend UI  
- POST /chat → Send question and receive response  

---

## Installation

Clone the repository

```bash
git clone <your-repo-url>
cd RAG_DAY_2

## Create virtual environment

python -m venv .venv
.venv\Scripts\activate

## Install dependencies

pip install -r requirements.txt

## Environment Setup

Create a .env file

GROQ_API_KEY=your_groq_api_key_here
GOOGLE_API_KEY=your_google_genai_api_key_here
DATABASE_URL=optiona

## Run Project
uvicorn main:app --reload --port 8000

Open in browser

http://127.0.0.1:8000

## Docker Run

Build image

docker build -t alex-rag .

Run container

docker run --rm -p 8000:8000 --env-file .env alex-rag

## Example

User Question

What is Artificial Intelligence?

AI Response

Artificial Intelligence is the simulation of human intelligence by machines.

## Future Improvements
- Multi-document upload system
- Vector database integration (FAISS or Pinecone)
- Chat memory system
- Cloud deployment (AWS, Render, Vercel)
- Analytics dashboard
- Hybrid search (keyword + semantic)

## Author

Ujjwal Kumar Karn
AI and Machine Learning Enthusiast | Aspiring AI Engineer
