<div align="center">

# 📚 Multi-Agent Document Chatbot

**An agentic RAG application for asking questions, analyzing documents, and generating cited answers and PDF reports.**

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge)](https://www.langchain.com/)
[![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6B6B?style=for-the-badge)](https://www.trychroma.com/)

</div>

## 📌 Overview

This project implements **agentic Retrieval-Augmented Generation (RAG)** for document question answering. A coordinated set of specialized agents retrieves evidence, evaluates it, produces grounded responses with citations, and can generate a downloadable PDF report.

## ✨ Features

- Upload and index **PDF, DOCX, TXT, and supported image formats**.
- Query ingested documents using semantic retrieval and BM25 keyword search.
- Filter retrieval to a selected document.
- Analyze and compare evidence, including extracted tables and calculations.
- Re-retrieve evidence when the analyst needs additional context.
- Format answers with source references and citation checks.
- Ask questions using voice transcription through Groq Whisper.
- Generate downloadable PDF reports.
- Follow the agent pipeline through streamed progress updates.

## 🧠 Agent Architecture

```text
             Documents
                 ↓
       Ingestion & Chunking
                 ↓
       Embeddings + ChromaDB
                 ↓
             Question
                 ↓
          Retriever Agent
    (semantic search, BM25, reranking)
                 ↓
           Analyst Agent
      (reasoning, tables, tools)
          ↕ feedback loop
          Retriever Agent
                 ↓
            Answer Agent
      (formatting + citations)
                 ↓
          Cited Response
                 ↓
      Optional Report Agent
                 ↓
              PDF
```

## 📂 Repository Structure

```text
Multi-Agent-Document-Chatbot/
├── agents/
│   ├── retriever_agent.py
│   ├── analyst_agent.py
│   ├── answer_agent.py
│   └── report_agent.py
├── pipeline/
│   └── document_pipeline.py
├── static/
│   └── index.html
├── api.py
├── orchestrator.py
└── requirements.txt
```

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Paula737/Multi-Agent-Document-Chatbot.git
cd Multi-Agent-Document-Chatbot
```

### 2. Create an environment and install requirements

```bash
python -m venv .venv
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

Or on Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Then install:

```bash
pip install -r requirements.txt
```

### 3. Configure the LLM API key

Create a **`.env`** file in the project root:

```dotenv
GROQ_API_KEY=your_groq_api_key_here
# Optional: override the default Groq-hosted model
# GROQ_MODEL=openai/gpt-oss-120b
```

**Never commit your real API key.** Add `.env` to `.gitignore` if it is not already ignored.

### 4. Launch the application

```bash
uvicorn api:app --reload
```

Open **http://127.0.0.1:8000**.

> Image OCR paths may require Tesseract installed on your system in addition to Python packages.

## 🔌 API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/` | Web interface |
| `GET` | `/api/documents` | List uploaded documents |
| `POST` | `/api/ingest` | Upload and index documents |
| `DELETE` | `/api/documents/{filename}` | Delete one document |
| `DELETE` | `/api/documents` | Clear document collection |
| `POST` | `/api/ask` | Ask a question; stream pipeline status |
| `POST` | `/api/transcribe` | Transcribe voice input |
| `POST` | `/api/report` | Generate a PDF report |

## 🛠️ Tech Stack

**Backend:** Python, FastAPI, Uvicorn  
**Orchestration:** LangChain, Groq  
**Retrieval:** ChromaDB, BM25, embedding models  
**Document Processing:** PDF/DOCX extraction, OCR, chunking  
**Analysis & Reporting:** Pandas, pdfplumber, ReportLab


