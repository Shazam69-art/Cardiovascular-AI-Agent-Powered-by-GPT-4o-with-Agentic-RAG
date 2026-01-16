# Cardiovascular-AI-Agent-Powered-by-GPT-4o-with-Agentic-RAG
AI Agent with Textbook Grounded Agentic RAG system for cardiovascular physiology questions, built on "The Gross Physiology of the Cardiovascular System" using GPT-4o and semantic search.
## Overview

CardioRAG is an educational, textbook-grounded medical AI assistant that answers questions about cardiovascular physiology using **agentic Retrieval-Augmented Generation (RAG)**.  
All responses are strictly derived from the freely available textbook *The Gross Physiology of the Cardiovascular System* by Robert M. Anderson, MD, combined with GPT-4o reasoning, self-validation, conversation memory, and real-time PubMed literature fallback.

**Key Features**

- Semantic search over 82 textbook chunks using BAAI/bge-small-en-v1.5 embeddings  
- Agentic workflow: query classification → subquery generation → retrieval → generation → validation  
- Multi-turn conversation memory  
- Real-time PubMed literature summaries when retrieval confidence is low  
- Professional Gradio interface with source display, metadata, and structured markdown answers  
- Designed for education, research prototyping, and self-study — **not** for clinical use

**Important Disclaimer**  
This project is for **educational and research purposes only**. It is not a medical device, not validated for clinical decision-making, and should never replace consultation with qualified healthcare professionals.

## Source Material

**Book**: *The Gross Physiology of the Cardiovascular System*  
**Author**: Robert M. Anderson, MD  
**Edition**: Freely distributed digital version (2012)  
**Direct PDF download**: [https://cardiac-output.info/Cardiovascular_System.pdf](https://cardiac-output.info/Cardiovascular_System.pdf)  
**Website**: [https://cardiac-output.info](https://cardiac-output.info)  
**License note**: The book is made freely available by the estate of the author for non-commercial educational use (subject to the website’s Terms & Conditions).

## Dataset & Embeddings

- PDF → text extraction → page-level filtering → chunking (500 words with 100-word overlap)  
- Result: **82 clean chunks** stored in `cardio_chunks.txt`  
- Embedding model: `BAAI/bge-small-en-v1.5` (384 dimensions, normalized)  
- Output files: `cardio_embeddings.npy` + `cardio_chunks.txt`

## Architecture

**Embedding Generation**  
- Sentence-Transformers → batch encoding → NumPy save  

**Inference Pipeline (Agentic RAG)**  
1. Query analysis (complexity, intent, specialty) via GPT-4o  
2. Subquery rewriting for complex questions  
3. Dense retrieval → relevance ranking → top chunks  
4. Context-aware generation with strict grounding instruction  
5. Self-validation pass to eliminate hallucinations  
6. Optional PubMed E-utilities literature augmentation  
7. Structured markdown output with inline citations and metadata footer  

**Core model**: OpenAI GPT-4o (reasoning + prompt engineering)

## Requirements

- Python 3.10+  
- `openai`, `sentence-transformers`, `numpy`, `gradio`, `requests`, `pypdf`, `tqdm`
