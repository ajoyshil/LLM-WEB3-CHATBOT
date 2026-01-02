# 🧠 Demo: Full-Stack AI Chatbot RAG System  
**Multi-Embedding · Multi-LLM · Plug-and-Play · Docker-Ready**

![Docker](https://img.shields.io/badge/Docker-Ready-blue?logo=docker)
![LangChain](https://img.shields.io/badge/LangChain-Framework-green)
![OpenAI](https://img.shields.io/badge/OpenAI-LLM-black?logo=openai)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Models-yellow?logo=huggingface)
![Groq](https://img.shields.io/badge/Groq-UltraFast-red)

---

## 🚀 Overview

This project is a **demo full-stack AI chatbot system** built using **Retrieval-Augmented Generation (RAG)**.  
It showcases how to design a **modern, modular, and extensible AI application** that supports **multiple LLM providers** and **multiple embedding models** using a clean **plug-and-play architecture**.

The system combines:
- A **FastAPI backend**
- **LangChain-powered LLM orchestration**
- **Vector search for RAG**
- **JWT-based authentication**
- A **Next.js (React) frontend**
- **Docker-first deployment**

> 🎯 Built as a **demo project**, but structured like a real-world system — ideal for portfolios, demos, learning, and open-source use.

<img width="1512" height="868" alt="Screenshot 2026-01-03 at 12 28 31 AM" src="https://github.com/user-attachments/assets/0eefa13e-42cf-4ba2-9615-4f3fe24ea931" />


---

## ✨ Key Features

- ✅ Retrieval-Augmented Generation (RAG)
- ✅ Multi-LLM support (plug-and-play)
- ✅ Multi-embedding support
- ✅ LLM-agnostic & embedding-agnostic design
- ✅ JWT-based authentication
- ✅ Conversation history & memory
- ✅ Clean modular backend architecture
- ✅ Component-based frontend
- ✅ Docker-ready setup
- ✅ Easy extensibility for new models

---

## 🧠 Supported LLM Providers

This project uses **LangChain** to enable seamless switching between LLM providers without changing business logic.

### 🔹 OpenAI
- `gpt-4`
- `gpt-4o`
- `gpt-3.5-turbo`

### 🔹 Hugging Face
- Chat & text-generation models via Inference API
- Open-source transformer models

### 🔹 Groq
- Ultra-fast inference
- Open-weight models (provider dependent)

### 🔹 Ollama (Local LLMs)
- LLaMA
- Mistral
- Gemma
- Any Ollama-supported model

> Switching LLMs requires only a configuration or factory update.

---

## 🧬 Supported Embedding Models

The RAG pipeline supports **multiple embedding backends**:

### 🔹 OpenAI Embeddings
- `text-embedding-3-small`
- `text-embedding-3-large`

### 🔹 Hugging Face Embeddings
- SentenceTransformers
- Open-source embedding models

### 🔹 Local / Custom Embeddings
- Ollama-compatible embeddings
- Custom embeddings via LangChain interfaces

Vector storage is designed to be **backend-agnostic**, enabling easy switching between FAISS, Chroma, PGVector, etc.

---

## 🛠️ Tech Stack

### 🔙 Backend
- FastAPI
- LangChain
- JWT Authentication
- PostgreSQL
- Vector Store (RAG)
- Docker

### 🎨 Frontend
- Next.js (React)
- Axios with interceptors
- JWT-based auth flow
- Chat UI with history
- Component-driven architecture

---



## 🧱 Project Structure

```
web3-rag-ai/
├── client/          # Next.js frontend
├── server/          # FastAPI backend
├── docker-compose.yml
└── README.md
```

### 📁 Server (Backend)


```
server/
├── api/                # FastAPI route handlers
│   ├── auth.py
│   └── chat.py
│
├── services/           # Business logic
│   ├── llm_service.py
│   ├── retrieval_service.py
│   └── llm_factory.py
│
├── repository/         # Database access layer
│   ├── chat_repository.py
│   └── user_repository.py
│
├── core/               # Core configs & security
│   ├── config.py
│   └── security.py
│
├── models/             # SQLAlchemy models
├── main.py             # FastAPI entry point
└── requirements.txt
```

---

## 🔄 API Flow (Chat Request)

1. User sends message from frontend
2. Backend retrieves relevant context using embeddings
3. Prompt is dynamically constructed
4. LLM generates grounded response
5. Conversation history is stored
6. Response + conversation ID returned

---

## 🚦 Getting Started

### 1️⃣ Clone Repository

```bash
git clone https://github.com/ajoyshil/LLM-WEB3-CHATBOT.git
cd LLM-WEB3-CHATBOT
```

### 2️⃣ Environment Variables

Create a `.env` file:

```env
HF_TOKEN=your_huggingface_token
JWT_SECRET_KEY=your_secret_key
DATABASE_URL=sqlite:///./app.db
```

### 3️⃣ Run with Docker

```bash
docker-compose up --build
docker-compose exec server python -m app.embeddings.ingest
```

### 4️⃣ Access API Docs

```
http://localhost:8000/docs
```

---

## 🧪 Example Chat Request

```http
POST /chat
Authorization: Bearer <token>

{
  "question": "What is Web3?",
  "conversation_id": null
}
```


---

## 🌱 Future Improvements

* Streaming responses (SSE / WebSockets)
* File upload & document ingestion
* Role-based access control (RBAC)
* Redis caching
* Rate limiting

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repo
2. Create a feature branch
3. Commit changes
4. Open a Pull Request

---

flowchart TD
    %% Client Layer
    subgraph Client["Client (React + MUI)"]
        UI[Chat UI]
        AuthUI[Auth Pages]
        HistoryUI[Chat History]
    end

    %% API Layer
    subgraph Server["Backend (FastAPI)"]
        AuthAPI[Auth API]
        ChatAPI[Chat API]
        HistoryAPI[History API]
    end

    %% Core Services
    subgraph Core["Core Services"]
        LLMService[LLM Service<br/>LangChain]
        RetrievalService[Retrieval Service<br/>RAG]
        VectorService[Vector Store]
    end

    %% LLM Providers
    subgraph LLMs["LLM Providers"]
        OpenAI[OpenAI]
        HF[Hugging Face]
        Groq[Groq]
        Ollama[Ollama]
    end

    %% Embeddings
    subgraph Embeddings["Embedding Models"]
        OpenAIEmb[OpenAI Embeddings]
        HFEmb[HF Sentence Transformers]
        OllamaEmb[Ollama Embeddings]
    end

    %% Storage
    subgraph Storage["Storage"]
        DB[(PostgreSQL)]
        VectorDB[(FAISS / Chroma)]
    end

    %% Client to Server
    UI --> ChatAPI
    HistoryUI --> HistoryAPI
    AuthUI --> AuthAPI

    %% Server Internals
    ChatAPI --> LLMService
    ChatAPI --> RetrievalService
    HistoryAPI --> DB
    AuthAPI --> DB

    %% RAG Flow
    RetrievalService --> VectorService
    VectorService --> VectorDB
    RetrievalService --> Embeddings

    %% LLM Routing
    LLMService --> OpenAI
    LLMService --> HF
    LLMService --> Groq
    LLMService --> Ollama

    %% Persistence
    ChatAPI --> DB


---

## 📄 License

MIT License © 2026

---

## 🙌 Acknowledgements

* LangChain
* Hugging Face
* FastAPI Community

---

**Built for scalable AI chat systems using open-source LLMs.** 🚀
