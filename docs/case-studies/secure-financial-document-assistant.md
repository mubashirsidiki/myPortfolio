# Behind the Build: How We Created a Secure, AI-Powered Financial Document Assistant for State Bank

## Introduction

In the world of finance, navigating complex documents quickly and securely is a constant challenge. For State Bank, privacy and data security are paramount—especially when leveraging the power of AI. Our team was tasked with building a solution that could answer questions about sensitive financial documents, all while ensuring data never left the organization’s secure environment.

The result? **Pennywise**: a local, AI-powered financial expert bot that combines cutting-edge language models, Retrieval Augmented Generation (RAG), and image understanding—all running privately, with no data sent to the cloud.

## General Overview

**Pennywise** is a secure, on-premises assistant that allows users to:

- Upload financial documents (PDFs, images)
- Ask natural language questions about their content
- Receive clear, context-aware answers—even for information not present in the AI’s original training data

Key features include:

- **Local LLM (Llama3) for privacy**: All processing happens on-site, ensuring sensitive data never leaves the bank’s infrastructure.
- **RAG (Retrieval Augmented Generation)**: Combines document search with AI reasoning for accurate, up-to-date answers.
- **Image-to-Text Integration**: Extracts and explains information from images within documents, ensuring no data is lost.
- **Fast, user-friendly API**: Built with FastAPI for seamless integration and rapid response times.

## Tech Stack

- **Frontend**: (Not specified in code; API-first design allows for web, desktop, or internal tool integration)
- **Backend**: Python, FastAPI
- **Database**: ChromaDB (vector database for semantic search)
- **Infrastructure/DevOps**: Runs locally/on-premises; Uvicorn server with SSL support for secure deployment
- **AI/ML Tools**:
  - Llama3 (8B, 4-bit quantized, via Langchain)
  - Sentence Transformers (all-MiniLM-L6-v2 for embeddings)
  - Langchain, ChromaDB, OpenAI API (for hybrid or fallback scenarios)
  - PyPDF2, image-to-text modules for document and image parsing

## How AI Powers the System

AI is at the heart of Pennywise, enabling it to understand, search, and explain complex financial documents:

- **Local LLM (Llama3)**: The core language model, running entirely on the bank’s hardware, ensures privacy and compliance.
- **RAG Pipeline**: When a user asks a question, the system:
  1. Searches the uploaded documents using semantic embeddings (all-MiniLM-L6-v2)
  2. Retrieves the most relevant passages
  3. Feeds them, along with the user’s question, into the LLM for a tailored answer
- **Image Understanding**: If a document contains images (e.g., charts, scanned tables), the system uses GPT or similar models to generate text explanations, which are then indexed alongside the rest of the document. This ensures no information is lost, and users can query image content as easily as text.
- **Integration**: All AI components are orchestrated via Langchain, with ChromaDB providing fast, semantic search over both text and image-derived content.
- **Challenges Solved**:
  - **Data Privacy**: By running all models locally, no sensitive data is exposed to external APIs.
  - **Image Data Loss**: By extracting and saving image explanations, the system ensures complete document coverage.
  - **Performance**: Efficient vector search and quantized models keep response times low, even on large documents.

## Technical Breakdown

- **Database Structure**: ChromaDB stores high-dimensional vector embeddings for all document chunks (text and image explanations), enabling fast similarity search.
- **Backend Architecture**:
  - FastAPI app with modular routers for PDF processing and query handling
  - Middleware for CORS and logging
  - SSL support for secure deployment
- **Key API Routes**:
  - `/process_pdf/`: Accepts PDF uploads, extracts text (and image explanations), splits into chunks, embeds, and stores in ChromaDB
  - `/process_query/`: Accepts user questions, retrieves relevant document chunks, and generates answers via the LLM
- **Engineering Decisions**:
  - **Local-first AI**: Chosen for privacy and compliance
  - **RAG over pure LLM**: Ensures up-to-date, document-specific answers
  - **Image-to-Text**: Prevents data loss from non-textual content

## User Journey Walkthrough

1. **User uploads a financial document** (PDF, possibly containing images) via the API or UI.
2. **Backend processes the document**:
   - Extracts all text using PyPDF2
   - Detects images, generates text explanations using GPT or similar
   - Splits content into manageable chunks
   - Embeds each chunk using all-MiniLM-L6-v2
   - Stores embeddings in ChromaDB for fast retrieval
3. **User asks a question** about the document (e.g., “What is the total revenue in Q2?”)
4. **System retrieves relevant chunks** from ChromaDB using semantic similarity
5. **RAG pipeline combines** the retrieved context with the user’s question
6. **Local LLM (Llama3) generates an answer**, using both the question and the retrieved document content
7. **User receives a clear, context-aware response**—with privacy and security guaranteed

## Text-Based Flowchart / Architecture

```
User
  ↓
Uploads Document (PDF/Image) → [API: /process_pdf/]
  ↓
Backend
  → Extracts text from PDF
  → Detects images, generates text explanations
  → Splits content into chunks
  → Embeds chunks (text + image explanations)
  → Stores embeddings in ChromaDB
  ↓
User
  ↓
Asks Question → [API: /process_query/]
  ↓
Backend
  → Retrieves relevant chunks from ChromaDB (semantic search)
  → Combines context with user question (RAG)
  → Passes to Local LLM (Llama3)
  → Generates answer
  ↓
Returns Answer to User
```

## Conclusion

Pennywise demonstrates how advanced AI can be harnessed for sensitive, real-world applications—without sacrificing privacy or security. By combining local LLMs, RAG, and image-to-text integration, we delivered a solution that’s both powerful and compliant with the strictest data protection requirements.

This project highlights our team’s ability to:

- Build secure, AI-driven systems for regulated industries
- Integrate state-of-the-art language and vision models
- Solve real business problems with creative engineering

**Future plans** include expanding to more document types, adding richer analytics, and further optimizing performance for even larger datasets. If you’re looking to bring secure, AI-powered insights to your organization, let’s connect!
