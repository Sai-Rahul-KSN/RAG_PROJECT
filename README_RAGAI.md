# Open AI Integrated RAG System

This repository contains two separate Retrieval-Augmented Generation (RAG) projects demonstrating end-to-end pipelines for academic literature question answering using different LLM backends and corpora:

1. **RAG_OpenAI_FullArxiv**: Uses OpenAI embeddings and LLM (GPT-4) over the full arXiv corpus.  
2. **Corpus_RAG_OpenAI**: A lightweight demo on a tiny, hand-picked 6-document corpus using OpenAI.  


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

### Key Features
- **Semantic Search** via OpenAI `text-embedding-ada-002` + FAISS  
- **Citation‑Aware Prompting**: answers cite retrieved abstracts as `[1]`, `[2]`, …  
- **Evaluation**: Precision@K (retrieval) and ROUGE‑1 F1 (answer quality)  
- **Interactive UI**: Gradio chat interface with day/night theme toggle  
- **Incremental Updates**: add new abstracts to the vector store without retraining

---

### Dependencies
- Python ≥ 3.8  
- `datasets` (HuggingFace)  
- `sentence-transformers`  
- `faiss-cpu`  
- `openai>=1.0.0`  
- `gradio`  
- `rouge_score`

---
### Code Structure & Cell-by-Cell Walkthrough

- **Cell 1:** Install dependencies (pip install ...)
- **Cell 2:** Restart kernel to apply upgrades
- **Cell 3:** Prompt for OPENAI_API_KEY (secure input)
- **Cell 4:** Verify & instantiate OpenAI client, list models
- **Cell 5:** Load 20 k arXiv + 20 k PubMed abstracts, keep only abstract
- **Cell 6:** Embed all abstracts via SentenceTransformer → FAISS index
- **Cell 7:** retrieve(query, k): embed query + FAISS .search()
- **Cell 8:** generate_answer(): build citation-aware prompt + ChatCompletion
- **Cell 9:** answer_query(): combine retrieval & generation
- **Cell 10:** Sample end-to-end test
- **Cell 11–12:** Evaluation: Precision@K + ROUGE-1 on held-out queries
- **Cell 13–17:** Gradio UI setup, custom CSS + day/night toggle

##  Challenges & Solutions

### API Rate Limits & Costs

- **Mitigation:** Batched embeddings, cache common queries, fall back to GPT-3.5-turbo.

### Context Window

- **Mitigation:** Chunk abstracts into 500 chars with 50 char overlap; tune top-k.

### Retrieval Relevance

- **Mitigation:** Use high-quality embeddings, optional BM25 reranking.

### Data Privacy

- **Mitigation:** Anonymize sensitive text; only send embeddings to API.

###  Future Work

- **Integrate OpenAI function calling for dynamic data access**
- **Fine-tune a smaller local model on domain data to reduce API calls**
- **Add confidence scoring & refusal logic for low-certainty queries**
- **Extend to multimodal RAG (e.g., images, tables)**

# Architecture Flow

[User Query]  
↓  
[1] Embed Query (OpenAI Embedding API)  
↓  
[2] FAISS vector search → top-k abstracts  
↓  
[3] Assemble Prompt with citations [1],[2],…  
↓  
[4] Generate Answer (OpenAI Chat API)  
↓  
[5] Format & Display (Gradio UI)
