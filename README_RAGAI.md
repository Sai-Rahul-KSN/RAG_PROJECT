# Open AI Integrated RAG System

This repository contains two separate Retrieval-Augmented Generation (RAG) projects demonstrating end-to-end pipelines for academic literature question answering using different LLM backends and corpora:

1. **RAG_OpenAI_FullArxiv**: Uses OpenAI embeddings and LLM (GPT-4) over the full arXiv corpus.  
2. **Corpus_RAG_OpenAI**: A lightweight demo on a tiny, hand-picked 6-document corpus using OpenAI.  
3. **GenAI_RAG**: Gemini-powered RAG system using Google Generative AI embeddings and LLM via LangChain.

---

## Project 1: RAG_OpenAI_FullArxiv

### Introduction
A scalable RAG system indexing tens of thousands of arXiv abstracts with OpenAI embeddings and GPT-4, returning citation-backed answers to research questions.

---

### Requirements
- Python 3.8+  
- OpenAI API key  
- Dependencies: see `RAG_OpenAI_FullArxiv/requirements.txt`

---

### Installation & Setup
```bash
git clone https://github.com/Sai-Rahul-KSN/RAG_PROJECT.git
cd RAG_PROJECT.git
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
export OPENAI_API_KEY="..."  # your OpenAI key 
```

### Building the Index

```bash
python scripts/load_arxiv.py      # fetch ~10k abstracts
python scripts/build_index.py     # embed & index with FAISS
```

### Running the System
```bash
CLI:
python scripts/run_rag.py --query "CRISPR-Cas9 mechanism" --k 3
```
### Web UI:
``` bash
cd ui
python app.py
```
- Then visit http://localhost:7860




