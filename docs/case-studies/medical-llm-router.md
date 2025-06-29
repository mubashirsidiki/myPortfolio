# Behind the Build: How We Created an AI-Powered Medical Query Router

## Introduction

The Medical LLM Router is an advanced AI-driven platform designed to help users get personalized answers to health-related questions by analyzing their medical history. Built for patients, healthcare providers, and digital health innovators, it bridges the gap between complex medical records and actionable insights. The system stands out by routing each query to a specialized AI agent—ensuring that every question is answered with domain-specific expertise and context from the user's own medical documents.

## General Overview

In simple terms, the Medical LLM Router lets users upload their medical history (as a PDF) and ask any health question. The system:

- Classifies the question by medical specialty (General, Neurology, Cardiology, Orthopedics)
- Searches the uploaded document for relevant information
- Routes the query to a specialist AI agent
- Returns a personalized, context-aware response

**Key Features:**

- Medical document processing (PDFs)
- Intelligent query classification
- Specialist AI agents for different medical domains
- Retrieval-Augmented Generation (RAG) for context-aware answers
- Fast, cached vector search for repeated queries

## Tech Stack

**Frontend:**  
- Streamlit: Provides a clean, interactive web interface for uploading documents, entering questions, and viewing results.

**Backend:**  
- Python 3.11: Core application logic and orchestration.
- LlamaIndex: Handles document parsing, vector storage, and retrieval.
- Custom workflow and agent classes for query routing and response generation.

**Database/Storage:**  
- Local file system: Stores vector indexes and temporary files for fast retrieval and caching.

**Infrastructure/DevOps:**  
- Environment variables managed via `.env` files for API keys and model selection.
- Deployable on Streamlit Cloud or any Python server.

**AI/ML Tools and Frameworks:**  
- NVIDIA LLMs (e.g., Llama-3): For both query classification and answer generation.
- OpenAI GPT-4o (fallback): Ensures reliability if NVIDIA models are unavailable.
- NVIDIA Embedding Models: For document chunk embedding and vector search.
- LlamaParse: Converts PDFs into structured, AI-readable text.

## How AI Powers the System

**AI’s Role:**

- **Query Understanding:** Uses LLMs to classify each question into a medical specialty.
- **Context Retrieval:** Embeds and searches the user’s medical history for relevant information using vector databases.
- **Specialist Response Generation:** Each domain (General, Neurology, Cardiology, Orthopedics) has a dedicated AI agent, powered by LLMs, that crafts a personalized answer using both the question and retrieved context.

**Models Used:**

- NVIDIA Llama-3 (primary) and OpenAI GPT-4o (fallback) for both classification and response.
- NVIDIA Embedding models for vector search.

**Integration Method:**

- Models are accessed via API keys, with dynamic selection based on environment configuration.
- LlamaIndex orchestrates embedding, storage, and retrieval.

**AI Tasks:**

- Natural Language Processing (NLP): Query classification, summarization, and answer generation.
- Information Retrieval: Semantic search over medical documents.
- Contextualization: Merges user-specific data with general medical knowledge.

**AI Challenges & Solutions:**

- **Challenge:** Ensuring fast responses for large documents.  
  - **Solution:** Vector store caching and re-use, so documents are only embedded once.
- **Challenge:** Accurate domain classification.  
  - **Solution:** Prompt engineering and fallback logic to default to “General” if uncertain.
- **Challenge:** Personalized, safe medical advice.  
  - **Solution:** All responses include disclaimers and are grounded in both the user’s data and medical best practices.

## Technical Breakdown

**Database Structure & Storage:**

- No traditional database; uses local directories to store vector indexes keyed by document hash.
- Each uploaded PDF is parsed, chunked, embedded, and stored for future queries.

**Backend Design:**

- Monolithic Python app with modular agent classes.
- REST-like workflow, but all logic is handled within Streamlit’s event-driven model.

**Key Engineering Decisions:**

- **Vector Store Registry:** Tracks which documents have already been embedded, saving time and compute.
- **Specialist Agent Classes:** Each medical domain has its own agent class for tailored responses.
- **Session State Management:** Uses Streamlit’s session state to track progress, logs, and results for a smooth UX.

**Key API/Internal Services:**

- `/process_document`: Orchestrates the full pipeline—file upload, classification, retrieval, and response.
- `classify_query`: Uses LLM to determine the medical specialty.
- `process_with_agent`: Routes the query to the correct specialist agent.

## User Journey Walkthrough

1. **Upload Medical History**  
   - User uploads a PDF of their medical records.  
   - The system parses and embeds the document for fast, future queries.

2. **Ask a Health Question**  
   - User enters a question (e.g., “Should I be concerned about my headaches?”).

3. **Query Classification**  
   - The AI classifies the question as General, Neurology, Cardiology, or Orthopedics.

4. **Context Retrieval**  
   - The system searches the user’s medical history for relevant information.

5. **Specialist Agent Response**  
   - The query and context are routed to the appropriate AI agent.  
   - The agent generates a personalized, markdown-formatted answer.

6. **Results & Download**  
   - The user sees the answer, a summary of the process, and can download the response.  
   - All responses include a medical disclaimer.

## Text-Based Flowchart / Architecture

<br>
<img src="../../images/projects/router-chart.png"
      style="float:center; width:2000px; height:4000px;">
<br>

## Conclusion

The Medical LLM Router demonstrates how advanced AI can make complex medical data accessible and actionable for everyone. By combining robust NLP, smart retrieval, and specialist agents, the platform delivers safe, personalized health information at scale. This project highlights our team’s expertise in AI integration, user-centric design, and medical data handling. Looking ahead, the system can be expanded to cover more specialties, integrate with EHRs, or support multilingual queries—offering even greater value to users and partners.
