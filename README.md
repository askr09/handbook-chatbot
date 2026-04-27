# 🦊 GitLab Handbook Assistant

An AI-powered chatbot that helps employees and aspiring candidates easily access insights from GitLab's **Handbook** and **Direction pages** using an advanced **Hybrid RAG + HyDE pipeline**.

---

## 🌐 Live Demo

🔗https://handbook-chatbot-gl.streamlit.app/

---

## 👤 Author

**Donipati Anu Kumari**
GitHub: https://github.com/askr09

---

## 🧠 How It Works

This project implements an **Advanced Retrieval-Augmented Generation (RAG)** system designed for high accuracy and minimal hallucination.

### 🔍 Core Pipeline

* **Query Expansion** — Enhances user queries with GitLab-specific terminology
* **HyDE (Hypothetical Document Embeddings)** — Generates a hypothetical ideal answer using Gemini to improve retrieval relevance
* **Hybrid Search** — Combines Semantic Search (ChromaDB) + Keyword Matching
* **Dual Collection Retrieval** — Retrieves from GitLab Handbook (operational) + Direction pages (strategic)
* **Grounded Generation** — Final response generated using **Gemini 2.0 Flash**, strictly based on retrieved context

---

## ✨ Features

* 💬 **Conversational AI** — Multi-turn conversations with memory
* 📚 **Massive Knowledge Base** — 75,000+ indexed document chunks
* 🔍 **Hybrid RAG + HyDE** — Reduces hallucinations significantly
* 📖 **Source Citations** — Every response grounded with references
* 🎨 **Custom UI Themes** — Light, Dark, Blue
* 🛡️ **Smart Guardrails** — Handles irrelevant queries gracefully
* ⚡ **Model Fallback System** — Auto-switches Gemini models on quota limits

---

## 🛠️ Tech Stack

| Component      | Technology                               |
| -------------- | ---------------------------------------- |
| Frontend       | Streamlit                                |
| LLM            | Gemini 2.0 Flash                         |
| Embeddings     | sentence-transformers (all-MiniLM-L6-v2) |
| Vector Store   | ChromaDB                                 |
| Data Source    | GitLab Handbook (git clone)              |

---

## 🗂️ Project Structure

```
gitlab-handbook-chatbot/
├── app.py                    # Streamlit UI
├── src/
│   ├── rag_engine.py         # Core RAG pipeline
│   ├── ingest_handbook.py    # Handbook ingestion
│   ├── ingest_direction.py   # Direction pages ingestion
│   ├── build_vectorstore.py  # Build ChromaDB vector store
│   ├── clear_db.py           # Reset database
│   └── debug_search.py       # Debug retrieval
├── requirements.txt
└── .env                      # Your API keys (not committed)
```

> `data/` and `chroma_db/` are excluded from git — you build them locally (see below).

---

## 🚀 Setup & Run Locally

### Prerequisites

* Python 3.10+
* Git
* [Gemini API key](https://aistudio.google.com) (free)

---

### 1. Clone the repo

```bash
git clone https://github.com/askr09/handbook-chatbot
cd gitlab-handbook-chatbot
```

---

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

> ⚠️ **Python 3.13 users:** `numpy<2.0` won't build from source. Install numpy 2.x first:
> ```bash
> pip install "numpy>=2.0" --only-binary=:all:
> pip install -r requirements.txt --only-binary=:all:
> ```

---

### 3. Create your `.env` file

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

---

### 4. Build the vector database

```bash
python src/build_vectorstore.py
```

This will:
1. **Clone** the GitLab Handbook repo (~100MB, one time)
2. **Chunk** ~4,000 markdown files into 75,000+ pieces
3. **Embed** everything using `all-MiniLM-L6-v2` (runs locally, no API needed)
4. **Store** in ChromaDB

⏱️ Takes **~45 minutes** on first run (CPU). Only needs to be done once.

---

### 5. Run the app

```bash
streamlit run app.py
```

Open **http://localhost:8501** in your browser.

---

## 🎯 Example Queries

* "What are GitLab's CREDIT values?"
* "How does GitLab handle unlimited PTO?"
* "How should I prepare for a GitLab technical interview?"
* "What is GitLab's three-year strategy?"
* "How does GitLab approach remote work?"

---

## 📊 Key Highlights

* Handles **large-scale documentation (75K+ chunks)** efficiently
* Uses **HyDE + Hybrid Retrieval** for better semantic matching
* Reduces hallucinations via **strict grounded generation**
* Designed for **real-world enterprise knowledge systems**

---

## 🚀 Future Improvements

* Add user authentication & personalization
* Implement feedback-based learning loop
* Integrate LangGraph / Agents for complex workflows
* Improve ranking using rerankers (cross-encoders)

---

## 📜 License

This project is for educational and research purposes.

---

⭐ If you find this useful, give it a star on GitHub!
