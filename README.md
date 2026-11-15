# Indian Startup Legal Assistant

An early stage legal assistance prototype for aspiring entrepreneurs and startup founders in India, built using Retrieval Augmented Generation (RAG).

## Problem

Aspiring founders often overlook legal requirements when starting and operating a business. They may not know which registrations, compliances, agreements, or legal obligations apply to their situation.

## Objective

The project explores how a RAG based legal assistant can help founders understand legal questions using information retrieved from a legal corpus, with an emphasis on evidence grounded responses and source references.

The broader vision is to help founders identify legal considerations they may not know to ask about.

## Technical Architecture

  **Embeddings:** Sentence Transformers (`all MiniLM L6 v2`)
  **Vector Search:** FAISS
  **Keyword Search:** BM25
  **Retrieval:** Hybrid retrieval with weighted Reciprocal Rank Fusion (RRF)
  **LLM:** Google Gemini API
  **Workflow:** LangGraph

## Workflow

1. User submits a legal query.
2. Query understanding identifies intent and relevant details.
3. Hybrid retrieval searches the legal corpus using semantic and keyword search.
4. Retrieved evidence is passed to the LLM for answer generation.
5. Citation integrity checks validate references against retrieved documents.
6. The system returns an answer or communicates insufficient evidence.

## Repository Structure

```text
startup legal assistant/
├── notebooks/
│   ├── 01_Data_Preparation_and_Indexing.ipynb
│   └── 02_Legal_RAG_Backend.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Setup

Install dependencies:

```bash
pip install  r requirements.txt
```

The notebooks were developed in Google Colab. The backend expects retrieval artifacts and the embedding model to be available in the configured Google Drive directory.

A Google Gemini API key is also required. Configure it securely through Colab Secrets; do not hardcode API keys in the notebooks.

## Current Status and Limitations

This is an early stage prototype. Its current legal corpus and retrieval capabilities do not establish comprehensive coverage of Indian startup law.

Citation integrity checks confirm that cited document identifiers exist in the retrieved evidence. They do not independently establish that every legal claim is correct.

The system is intended for research and informational assistance, not as a substitute for advice from a qualified legal professional.

## Future Scope

  Expand coverage of startup formation, registrations, taxation, contracts, intellectual property, employment, and regulatory compliance.
  Improve evidence verification and evaluation.
  Develop a guided founder facing interface.
  Add workflows that proactively surface relevant legal considerations.

## Disclaimer

This project is an educational prototype. It does not provide legal advice or create an advocate client relationship. Users should consult qualified legal professionals before acting on legal matters.
