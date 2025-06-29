# Behind the Build: How We Created an AI-Powered Drone Pilot Assessment & Feedback Platform

## Introduction {style="color: white;"}

In the rapidly evolving world of drone technology, both aspiring and experienced pilots need smarter, more interactive tools to assess their readiness, receive personalized training recommendations, and interact with AI-driven systems. Our project answers this need—a modular, AI-powered platform designed to streamline drone pilot assessment, feedback, and real-time interaction.

Built for drone training organizations, tech startups, and individual enthusiasts, this platform leverages state-of-the-art AI to deliver instant, actionable insights and a seamless user experience. What sets it apart is its deep integration of OpenAI’s language models, real-time feedback, and a robust, scalable architecture.

---

## General Overview {style="color: white;"}

At its core, the platform enables users to:

- **Assess their drone pilot readiness** through a conversational AI interface.
- **Receive personalized training module recommendations** based on their experience and goals.
- **Interact with a real-time console** for chat, feedback, and drone-related queries.
- **Get instant, AI-powered feedback** on their responses and progress.

**Key Features:**

- Conversational AI chatbot for assessment and Q&A
- Automated extraction of user profile and experience
- Dynamic training module recommendations
- Real-time feedback and progress tracking
- Modern, responsive web interface

---

## Tech Stack {style="color: white;"}

**Frontend:**  
- React (TypeScript)
- React Router for navigation
- Leaflet for interactive maps
- Three.js for 3D visualization
- OpenAI Realtime API (browser client)
- Sass for styling

**Backend:**  
- NestJS (Node.js, TypeScript)
- Prisma ORM (database abstraction)
- Axios for HTTP requests
- Swagger for API documentation
- Class-validator for input validation

**AI Backend:**  
- FastAPI (Python)
- Uvicorn (ASGI server)
- OpenAI Python SDK
- Custom prompt engineering

**Database:**  
- Managed via Prisma (commonly PostgreSQL or MySQL)

**Infrastructure / DevOps:**  
- Poetry for Python dependency management
- npm for Node/React
- Modular microservices (potential for Docker/Kubernetes)

**AI/ML Tools:**  
- OpenAI GPT models (via API)
- Custom prompt templates and response parsing

---

## How AI Powers the System {style="color: white;"}

AI is the heart of this platform, driving the assessment, feedback, and recommendation engines.

**AI’s Role:**
- **Natural Language Understanding:** Extracts user experience, goals, and knowledge from free-form text.
- **Personalized Recommendations:** Suggests training modules tailored to each user’s background.
- **Conversational Agent:** Engages users in dynamic, context-aware dialogue.
- **Profile Extraction:** Summarizes user data for backend storage and analytics.

**Models Used:**
- OpenAI GPT (e.g., GPT-4) for all NLP tasks.

**Integration Method:**
- The AI backend (FastAPI) communicates with OpenAI via the official Python SDK.
- Prompts are carefully engineered and dynamically filled with user input.
- Responses are parsed, validated, and returned to the main backend and frontend.

**AI Tasks:**
- Information extraction (from user input)
- Question answering
- Module recommendation
- Profile summarization

**Challenges & Solutions:**
- **Parsing AI Output:** Custom logic ensures robust extraction of structured data from GPT’s responses, even when output is not perfectly formatted.
- **Prompt Engineering:** Iterative refinement of prompts to maximize accuracy and relevance.
- **Error Handling:** Decorators and retries for resilient API calls.

---

## Technical Breakdown {style="color: white;"}

**Database Structure:**
- User records, chat logs, assessment results, and module recommendations are stored via Prisma ORM.
- Flexible schema supports rapid iteration and new features.

**Backend Design:**
- **NestJS** serves as the main orchestrator, exposing RESTful APIs for chat, assessment, and recommendations.
- **FastAPI microservice** handles all AI-related tasks, keeping AI logic isolated and scalable.
- **Relay server** (Node.js) manages real-time communication and API key security.

**Key API Routes:**
- `/bot/drone-assessment` (POST): Triggers AI-driven assessment and information extraction.
- `/chat`: Retrieves chat history for a user.
- `/module-recommendation`: Returns personalized training modules.

**Engineering Decisions:**
- **Microservices:** Decouples AI from business logic for scalability and maintainability.
- **Async Operations:** Both Python and Node backends use async patterns for high throughput.
- **Global Middleware:** Handles CORS, validation, and error management.

---

## User Journey Walkthrough {style="color: white;"}

1. **Landing on the Platform**
   - User visits the web console (React app).
   - Presented with options: start a chatbot session or view feedback.

2. **Starting an Assessment**
   - User initiates a chat with the AI.
   - The frontend sends user input to the backend API.

3. **Backend Processing**
   - The main backend receives the request and forwards it to the AI backend.
   - The AI backend crafts a prompt and calls the OpenAI API.
   - AI extracts user experience, goals, and knowledge from the input.

4. **AI-Driven Recommendation**
   - AI backend returns structured data (profile, assessment, recommendations).
   - Backend stores results and sends them to the frontend.

5. **User Receives Feedback**
   - The frontend displays personalized feedback and recommended training modules.
   - User can review their assessment transcript and explore suggested courses.

6. **Real-Time Interaction**
   - Users can continue chatting, ask questions, or provide feedback.
   - All interactions are logged and analyzed for continuous improvement.

---

## Text-Based Flowchart / Architecture {style="color: white;"}

```
User
  ↓
Frontend (React App)
  → User enters input (chat, assessment, feedback)
  ↓
Backend API (NestJS)
  → Receives request
  → Validates and logs input
  ↓
AI Backend (FastAPI)
  → Receives request from main backend
  → Crafts prompt for OpenAI GPT
  → Calls OpenAI API
  → Parses and validates AI response
  ↓
Backend API (NestJS)
  → Stores results in database (Prisma)
  → Returns structured response to frontend
  ↓
Frontend (React App)
  → Displays feedback, recommendations, and chat history
  → User continues interaction or explores further
```

---

## Conclusion {style="color: white;"}

This project demonstrates the power of combining modern web technologies with advanced AI to deliver a seamless, intelligent user experience. By leveraging microservices, robust backend frameworks, and state-of-the-art language models, we’ve built a platform that’s scalable, maintainable, and truly impactful for drone pilot training and assessment.

Our team’s expertise in AI integration, prompt engineering, and full-stack development shines through in every aspect of the system. Looking ahead, we plan to expand the platform with more AI-driven features, deeper analytics, and broader integrations—empowering users and organizations to reach new heights in drone technology.
