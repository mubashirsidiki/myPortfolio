# Behind the Build: How We Created an AI-Powered Medical MCQ Test Generator

## Introduction

In the fast-evolving world of medical education, students and educators need smarter tools to create, review, and practice exam questions. Our Medical MCQ Test Generator is designed for medical students, teachers, and institutions who want to generate high-quality, context-aware multiple-choice questions (MCQs) instantly. By leveraging advanced AI and a modern web interface, this platform transforms static study materials into interactive, personalized learning experiences.

What sets this project apart is its seamless blend of AI-driven content generation, real-time feedback, and a user-friendly dashboard—making exam prep more effective and engaging.

---

## General Overview

The Medical MCQ Test Generator is a web-based platform that allows users to:

- **Generate MCQs** from medical documents or keywords using AI.
- **Receive instant feedback** on answers, including explanations and references.
- **Track performance** and review statistics via a modern dashboard.
- **Support educators** in creating question banks and practice tests efficiently.

**Key Features:**
- AI-powered MCQ generation based on difficulty, context, and keywords.
- Automated feedback and explanations for each question.
- Source referencing for transparency and further study.
- User dashboard with performance analytics.

---

## Tech Stack

**Frontend:**  
- Next.js (React) for a fast, interactive UI  
- Tailwind CSS for modern, responsive design  
- React Query, ApexCharts, and NextUI for state management and visualization

**Backend:**  
- FastAPI (Python) for robust, async REST APIs  
- Uvicorn for high-performance ASGI server  
- Prisma ORM for database access

**Database:**  
- MongoDB for flexible, scalable data storage  
- ChromaDB (vector database) for semantic search and document retrieval

**Infrastructure / DevOps:**  
- Docker for containerization  
- Docker Compose for service orchestration

**AI/ML Tools and Frameworks:**  
- OpenAI GPT (via API) for question and feedback generation  
- HuggingFace Transformers for embeddings  
- LangChain for document processing and vector search  
- PyTorch for model support

---

## How AI Powers the System

AI is the heart of this platform, enabling:

- **MCQ Generation:**  
  The system uses OpenAI’s GPT models to generate MCQs from provided context, keywords, or uploaded documents. Prompts are carefully crafted to ensure medical accuracy and relevance.

- **Feedback & Explanation:**  
  When a user answers a question, the AI provides instant feedback, including whether the answer is correct and a detailed explanation.

- **Semantic Search:**  
  HuggingFace embeddings and ChromaDB allow the system to find the most relevant document sections for question generation, ensuring contextually accurate MCQs.

**Integration:**  
- The backend orchestrates calls to OpenAI’s API and HuggingFace models using async Python services.
- LangChain pipelines manage document splitting, embedding, and retrieval.

**AI Challenges & Solutions:**  
- **Challenge:** Ensuring medical accuracy and plausible distractors in MCQs.  
  **Solution:** Custom prompt engineering and validation loops, retrying generation until quality criteria are met.
- **Challenge:** Fast, relevant context retrieval from large documents.  
  **Solution:** Vector search with ChromaDB and HuggingFace embeddings.

---

## Technical Breakdown

**Database Structure:**  
- **MongoDB** stores users, usage stats, and keywords.
- **ChromaDB** stores vectorized document chunks for semantic search.

**Backend Architecture:**  
- Modular FastAPI app with routers for MCQ, chat, document, and keyword APIs.
- Prisma ORM for async database operations.
- Middleware for logging, CORS, and usage tracking.

**Key API Routes:**  
- `/api/bot/mcq/generate`: Generate MCQs based on keywords, difficulty, and context.
- `/api/bot/mcq/feedback`: Submit answers and receive AI-generated feedback.
- Additional endpoints for document upload, keyword extraction, and chat.

**Notable Engineering Decisions:**  
- Use of async/await throughout for scalability.
- Retry logic and validation for AI outputs.
- Modular service and schema layers for maintainability.

---

## User Journey Walkthrough

1. **Landing & Dashboard:**  
   The user logs in and lands on a modern dashboard showing test stats and performance.

2. **MCQ Generation:**  
   - User enters keywords or uploads a medical document.
   - Selects difficulty and number of questions.
   - Clicks “Generate MCQs”.

3. **Backend Processing:**  
   - Frontend sends a request to `/api/bot/mcq/generate`.
   - Backend retrieves relevant document sections using vector search.
   - Constructs a prompt and calls OpenAI’s GPT to generate MCQs.
   - Validates and returns the questions, choices, and sources.

4. **Taking the Test:**  
   - User answers the MCQs in the UI.
   - Submits answers for feedback.

5. **AI Feedback:**  
   - Frontend sends answers to `/api/bot/mcq/feedback`.
   - AI evaluates responses, generates explanations, and returns feedback.

6. **Review & Analytics:**  
   - User reviews explanations and sources.
   - Dashboard updates with new performance stats.

---

## Text-Based Flowchart / Architecture

```
User
  ↓
Frontend (Next.js Dashboard)
  ↓
[Generate MCQs] → API Request → /api/bot/mcq/generate
  ↓
Backend (FastAPI)
  → Vector DB (ChromaDB) → Retrieve relevant context
  → AI Service (OpenAI GPT via API) → Generate MCQs
  → Validate & format response
  ↓
Frontend displays MCQs
  ↓
User answers questions
  ↓
[Submit Answers] → API Request → /api/bot/mcq/feedback
  ↓
Backend
  → AI Service (OpenAI GPT) → Evaluate answers, generate feedback
  ↓
Frontend displays feedback, explanations, and analytics
  ↓
User reviews results and continues learning
```

---

## Conclusion

The Medical MCQ Test Generator is a showcase of how AI can revolutionize education—making content creation, assessment, and personalized feedback faster and smarter. Our team combined deep technical expertise in AI, backend engineering, and modern frontend development to deliver a seamless, impactful product.

**Future plans** include adaptive learning paths, more granular analytics, and support for additional medical specialties. We’re excited to help shape the future of medical education and welcome collaboration or new client opportunities!
