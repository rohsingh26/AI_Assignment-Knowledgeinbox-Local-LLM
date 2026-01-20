# Local Embedding Server – MiniLM (Sentence Transformers)

This service provides **local text embeddings** using the **MiniLM sentence-transformers model**.  
It runs as a lightweight **Flask API** and is used by the backend to generate embeddings for both:

- Ingested content chunks
- User questions at query time

This design avoids using paid or token-limited LLM APIs for embeddings.

---

## 🚀 Why This Server Exists

### ❌ Why NOT use Gemini / OpenAI for embeddings?
- Embedding large documents consumes **a lot of tokens**
- Free-tier LLM APIs have **strict token limits**
- Embeddings are **not generative** tasks — they don’t need large LLMs

### ✅ Why MiniLM?
- Open-source
- Lightweight and fast
- Produces high-quality semantic embeddings
- Runs fully **locally**
- No token cost
- Perfect for RAG pipelines

---

## 🧠 Model Used

**Sentence Transformers**
- Model: `all-MiniLM-L6-v2`
- Embedding size: 384
- Optimized for semantic similarity search

---

## 🛠 Tech Stack

- Python
- Flask
- sentence-transformers
- PyTorch

---

# 📦 Setup Instructions

## 📥 Clone the Repository First

Before setting up the environment, clone the repository:

```bash
git clone https://github.com/rohsingh26/AI_Assignment-Knowledgeinbox-Local-LLM.git
cd AI_Assignment-Knowledgeinbox-Local-LLM
```
---

## 1️⃣ Create Virtual Environment

```bash
python -m venv venv
```

## Activate it:

### Windows
```bash
venv\Scripts\activate
```


### Mac / Linux
```bash
source venv/bin/activate
```

## 2️⃣ Install Dependencies
```bash
pip install sentence-transformers flask
```

### 3️⃣ Start the Embedding Server
```bash
python embedding_server.py
```


## Server will start at:
```bash
http://localhost:8000
```

### 🔌 API Endpoint
POST 
```bash
http://localhost:8000/embed
```

Request
```Code snippet
{
  "text": "Text content"
}
```

Response
```Code snippet
{
  "embedding": [0.0123, 0.9845, ...]
}
```

- Returns a numerical vector representation of the input text

- Used for both document chunks and user queries

## 🔄 How This Fits Into the Project
During Content Ingestion

Backend chunks content into smaller parts

Each chunk is sent to this server

MiniLM generates embeddings

Embeddings are stored with chunk IDs in vector storage

During Question Answering

User question is embedded using the same MiniLM model

Cosine similarity is computed against stored vectors

Top-K relevant chunks are selected

Only those chunks are sent to Gemini for answer generation

### 🎯 Benefits of This Approach

### 🚀 Faster ingestion

### 💸 Zero token cost for embeddings

### 🔒 Fully local & private

### 🧠 Same embedding space for data + queries

### 🧩 Clean separation of responsibilities

---

### ➡️ Next step: Start the Backend
Go to the:
```bash
https://github.com/rohsingh26/AI_Assignment-Knowledgeinbox-backend
```
