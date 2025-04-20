# Open AI Integrated RAG System 

## Project 2: Corpus_RAG_OpenAI

### Introduction

RAG_CORPUS is a minimal Retrieval‑Augmented Generation prototype built on a hand‑picked 6 document corpus. It demonstrates the entire RAG pipeline embedding, retrieval, citation aware prompting, evaluation, and a simple Gradio UI in under 2 minutes.

---

### Requirements

- Python 3.8+  
- OpenAI API key  
- Dependencies: see `Corpus_RAG_OpenAI/requirements.txt`

---
### Key Features
- Local embeddings via sentence-transformers (all-MiniLM-L6-v2)
- FAISS for exact semantic search on 6 docs
- Citation prompts: enforces [1] style references
- Evaluation: Precision@1 and ROUGE‑1 for three test queries
- Lightweight UI: Gradio Interface for single‑turn Q&A
---
### Dependencies
- Python ≥ 3.8
- sentence-transformers
- faiss-cpu
- openai
- gradio
- rouge_score

### Installation & Setup
``` bash
git clone https://github.com/Sai-Rahul-KSN/RAG_PROJECT.git
cd RAG_PROJECT.git
pip install -r requirements.txt
export OPENAI_API_KEY="..."[Youre API key]
```
# Code Structure

- **Cell 1:** Install deps (pip install ...)
- **Cell 2:** Prompt for OPENAI_API_KEY
- **Cell 3:** Define 6-document corpus (docs list)
- **Cell 4:** Embed & FAISS index
- **Cell 5:** retrieve(query, k) semantic search
- **Cell 6:** generate_answer() with citation prompt
- **Cell 7:** answer_query() wrapper + quick test
- **Cell 8:** Evaluate Precision@1 & ROUGE-1 on 3 queries
- **Cell 9:** Gradio UI (gr.Interface) for single Q&A

# Challenges & Solutions

- **Demonstration speed:** Needed a corpus so small it runs instantly.
- **Balancing detail vs. brevity:** Citation prompts ensure academic style without overwhelming context.
- **Evaluation clarity:** Chose Precision@1 and ROUGE-1 on a toy test set to show effectiveness.

# Future Work

- **Swap in a slightly larger corpus (e.g. 50 docs) to showcase scaling.**
- **Add chat history in the UI for multi-turn flows.**
- **Experiment with local small LLMs for generation (no API calls).**

# Architecture Flow

[User Query]  
↓  
Embed with local SentenceTransformer  
↓  
FAISS IndexFlatIP search → top-k docs  
↓  
Prompt assembly with numbered abstracts  
↓  
OpenAI ChatCompletion → Answer  
↓  
Display (Gradio interface)
