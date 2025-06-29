# AI-Powered Procurement Platform

<h2 style="color: white;">Introduction</h2>

A platform designed to streamline procurement processes, leveraging AI to automate and enhance user interactions, data management, and decision-making. It simplifies procurement management, automates repetitive tasks, and provides intelligent assistance, reducing manual effort and errors.

<h2 style="color: white;">Key Features & User Experience</h2>

- **Frontend:**  
  Built with Next.js and React, offering modules for procurement forms, chat, questions, history, and user selection.
- **Backend:**  
  FastAPI server with modular routing, Prisma ORM for database access, and robust middleware (CORS, logging, error handling).
- **Database:**  
  PostgreSQL managed via Prisma, with a `Collection` model for user procurement data.
- **AI Integration:**  
  The backend is designed to handle AI APIs (OpenAI integration is referenced), suggesting features like smart chat, automated form filling, or intelligent recommendations.

<h2 style="color: white;">Tech Stack</h2>

**Frontend:** Next.js, React, Tailwind CSS  
**Backend:** FastAPI (Python), Uvicorn, Prisma ORM  
**Database:** PostgreSQL (via Prisma)  
**AI/ML:** OpenAI API (NLP tasks), dotenv for config  
**Infrastructure:** SSL support, CORS, environment-based config

<h2 style="color: white;">AI System Details</h2>

- **Role:**  
  AI powers backend APIs, likely for chat, question answering, and smart procurement suggestions.
- **Integration:**  
  Uses OpenAI API via environment variable, integrated into FastAPI endpoints.
- **Tasks:**  
  Natural language processing, possibly classification, summarization, or conversational AI.
- **Challenges:**  
  Secure API key management, async integration, error handling, and ensuring AI responses are relevant to procurement.

<h2 style="color: white;">Technical Breakdown</h2>

- **Database:**  
  - `Collection` model: stores user procurement data, actions, timestamps.
  - Uses Prisma for async, type-safe queries.
- **Backend:**  
  - Modular FastAPI app with routers for procurement actions.
  - Middleware for CORS and logging.
  - Prisma client with retry logic for robust DB connections.
  - API endpoints for creating and deleting collections.
- **Frontend:**  
  - Modular React components for each procurement function.
  - Main page focuses on user selection, with other modules likely loaded as needed.

<h2 style="color: white;">User Journey Walkthrough</h2>

1. **User visits the platform**  
   → Sees a clean UI with user selection (e.g., buyer, seller, agent).
2. **User selects their role**  
   → Frontend loads relevant modules (form, chat, history, questions).
3. **User interacts (e.g., fills form, asks questions, chats)**  
   → Frontend sends requests to FastAPI backend.
4. **Backend processes request**  
   → If AI is needed (e.g., chat, question answering), backend calls OpenAI API.
5. **Database operations**  
   → User actions (create/delete collections) are stored/retrieved via Prisma.
6. **AI response or DB result returned**  
   → Backend sends processed data or AI-generated content to frontend.
7. **User sees results**  
   → UI updates with new information, chat responses, or confirmation messages.

<h2 style="color: white;">Text-Based Flowchart / Architecture</h2>

```
User
  ↓
Frontend (Next.js/React)
  ↓
[User Selection] → [Procurement Form] → [Chat] → [Questions] → [History]
  ↓
API Request (REST)
  ↓
Backend (FastAPI)
  → [Router: /api/db/collection/create | /delete]
  → [AI Logic: OpenAI API call if needed]
  → [Database: Prisma ORM → PostgreSQL]
  ↓
Response
  ↓
Frontend UI Update
  ↓
User sees result
```

<h2 style="color: white;">Conclusion</h2>

This procurement platform demonstrates a modern, AI-powered approach to business process automation. The combination of a robust FastAPI backend, a modular Next.js frontend, and seamless AI integration showcases the team’s technical depth and creativity. The use of Prisma and PostgreSQL ensures data integrity and scalability, while OpenAI’s NLP capabilities add intelligence and automation.

**Future plans:**  
- Expand AI features (e.g., predictive analytics, document processing)  
- Deeper workflow automation  
- Broader integration with enterprise systems

<h2 style="color: white;">Navigation</h2>

<p>
<a href="../case-studies/previous-case-study.md" style="float:left;">&laquo; Previous</a>
<a href="../case-studies/next-case-study.md" style="float:right;">Next &raquo;</a>
</p>
