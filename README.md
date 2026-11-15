# Indian Startup Legal Assistant

An early stage AI powered legal assistance prototype for aspiring entrepreneurs and startup founders in India, built using Retrieval Augmented Generation (RAG).

The project explores how an intelligent legal assistant can help founders understand legal obligations, navigate legal information and identify considerations they might not know to ask about.

## 1. Problem Statement

Starting and operating a business involves navigating numerous legal requirements, including registrations, licences, taxation, contracts, employment regulations and intellectual property.

However, aspiring entrepreneurs often lack awareness of which legal obligations apply to their specific business situation.

The challenge is not simply finding answers to legal questions. It is also identifying the questions that founders should be asking in the first place.

## 2. Project Objective

The objective is to develop a RAG based legal assistant that provides evidence grounded responses using a structured corpus of Indian legal information.

The broader vision is to build a legal companion that helps founders:

1. Understand legal requirements relevant to their business.
2. Explore applicable registrations and compliance obligations.
3. Understand contracts, agreements and legal responsibilities.
4. Identify potential legal risks during different stages of business development.
5. Discover legal considerations they may otherwise overlook.

## 3. Technical Architecture

The system combines semantic retrieval, keyword retrieval and LLM based answer generation.

| Component | Technology |
|---|---|
| Programming Language | Python |
| Embedding Model | Sentence Transformers: all MiniLM L6 v2 |
| Vector Search | FAISS |
| Keyword Retrieval | BM25 |
| Hybrid Retrieval | Weighted Reciprocal Rank Fusion |
| LLM | Google Gemini API |
| Workflow Orchestration | LangGraph |
| Development Environment | Google Colab |

### Retrieval Architecture

The retrieval pipeline uses two complementary approaches:

**Semantic Retrieval:** FAISS retrieves legally relevant documents based on embedding similarity.

**Keyword Retrieval:** BM25 identifies documents containing relevant legal terminology and keywords.

**Hybrid Ranking:** Weighted Reciprocal Rank Fusion combines the two retrieval rankings, followed by deduplication and metadata based filtering.

## 4. Dataset and Implementation Scale

The current legal corpus and retrieval pipeline have the following scale:

| Metric | Value |
|---|---:|
| Legal Records | 7,702 |
| Retrieval Chunks | 15,008 |
| Retrieval Methods | 2 |
| Final Retrieved Chunks | 5 |
| Embedding Dimensions | 384 |
| Data Preparation Notebooks | 1 |
| Backend Notebooks | 1 |

The document processing pipeline includes extraction, metadata normalisation, text cleaning, boundary aware chunking, embedding generation and index construction.

The chunking implementation uses a configured chunk size of 1,100 characters and an overlap of 160 characters.

These figures describe the current implementation and do not represent measured retrieval accuracy or legal coverage.

## 5. System Workflow

The current backend follows a structured LangGraph workflow.

1. **Query Understanding:** Identifies the user's intent, relevant entities and missing information.
2. **Clarification:** Requests additional information when the query requires it.
3. **Hybrid Retrieval:** Searches the legal corpus using semantic and keyword retrieval.
4. **Answer Synthesis:** Uses retrieved evidence to generate a structured response through Gemini.
5. **Citation Integrity Checks:** Validates citation identifiers against the retrieved documents.
6. **Response Generation:** Returns the answer or communicates when sufficient evidence is unavailable.

## 6. Repository Structure

```text
startup-legal-assistant/
│
├── notebooks/
│   ├── 01_Data_Preparation_and_Indexing_CLEAN.ipynb
│   └── 02_Legal_RAG_Backend_CLEAN.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

### Notebook 01: Data Preparation and Indexing

Handles legal data ingestion, document extraction, metadata normalisation, text processing, chunking, embedding generation and FAISS and BM25 index construction.

### Notebook 02: Legal RAG Backend

Implements artifact loading, hybrid retrieval, query understanding, Gemini integration, answer synthesis, citation integrity checks and LangGraph orchestration.

## 7. Setup and Execution

### Requirements

Python 3.10 or later is recommended. The notebooks were developed and tested primarily in Google Colab.

Install the dependencies using:

```bash
pip install -r requirements.txt
```

### Configuration

The backend requires:

1. Access to the generated retrieval artifacts.
2. The Sentence Transformer embedding model.
3. A valid Google Gemini API key.

The notebooks currently use Google Drive for storing the legal corpus, embedding model and retrieval artifacts.

Configure the Gemini API key securely through Google Colab Secrets. Do not hardcode credentials into the notebooks.

The retrieval artifacts are not included in this repository.

## 8. Current Status and Limitations

This project is an early stage prototype focused on developing the underlying legal retrieval and response generation pipeline.

The current implementation demonstrates hybrid retrieval, structured query processing, evidence grounded answer synthesis and citation integrity checks.

However, several limitations remain:

1. The existing corpus does not establish comprehensive coverage of Indian startup law.
2. Retrieval relevance and legal accuracy require further systematic evaluation.
3. Citation integrity checks do not independently verify whether every generated legal claim is supported by its cited source.
4. The current implementation is notebook based and depends on external Google Drive artifacts.
5. The system is not yet a comprehensive founder facing legal assistance application.

The project should be treated as an experimental research prototype rather than a production ready legal service.

## 9. Future Development

Planned areas of development include:

1. Expanding legal coverage across business formation, taxation, intellectual property, employment, contracts and regulatory compliance.
2. Improving legal document metadata and source traceability.
3. Developing more rigorous claim level evidence verification.
4. Building a founder facing web application.
5. Introducing guided business onboarding and business specific legal assessments.
6. Developing workflows that proactively identify relevant legal considerations as a business evolves.

## 10. Disclaimer

This project is an educational and experimental prototype. It does not provide professional legal advice or establish an advocate client relationship.

Legal information generated by the system should be independently verified. Users should consult qualified legal professionals before making decisions or acting on legal matters.
