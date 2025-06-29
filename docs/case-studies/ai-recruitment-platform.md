<h1 style="color: white;">AI-Powered Recruitment/Interview Platform</h1>

---

<h2 style="color: white;">Project Purpose & Overview</h2>

<b>What is it?</b><br>
A modular, AI-powered recruitment/interview platform. The backend is built with FastAPI (Python), and the frontend uses Next.js (React/TypeScript). The system leverages advanced AI (OpenAI models, Whisper, TTS) to automate and enhance candidate interviews and assessments.

<b>Who is it for?</b><br>
Companies and recruiters seeking to streamline, automate, and improve the candidate interview process.

<b>What problem does it solve?</b><br>
It automates candidate interviews, provides AI-driven insights, and manages audio (speech-to-text, text-to-speech) interactions, saving time and improving the quality of hiring decisions.

<b>What makes it unique?</b><br>
- Deep AI integration (OpenAI, Whisper, TTS)<br>
- Modular, microservice-ready backend<br>
- Real-time audio processing and analytics<br>
- Modern, responsive frontend

---

<h2 style="color: white;">General Overview</h2>

<b>Key Features:</b>
- Automated candidate interviews (audio/text)
- AI-powered insights and analytics
- Speech-to-text (STT) and text-to-speech (TTS) services
- Usage tracking and reporting
- Admin and user portals

<b>Use Cases:</b>
- Screening candidates at scale
- Generating interview transcripts and summaries
- Providing instant feedback and analytics to recruiters

---

<h2 style="color: white;">Tech Stack</h2>

<b>Frontend:</b><br>
Next.js 14, NextUI, Tailwind CSS, TypeScript, Framer Motion

<b>Backend:</b><br>
FastAPI (Python), Uvicorn, Poetry, Prisma ORM

<b>Database:</b><br>
MongoDB (via Prisma)

<b>Infrastructure/DevOps:</b><br>
Poetry for Python dependency management, environment variables for config, S3 for storage

<b>AI/ML:</b><br>
OpenAI (GPT-4, GPT-3.5, etc.), Whisper (speech-to-text), TTS (text-to-speech), integrated via API keys

---

<h2 style="color: white;">How AI Powers the System</h2>

<b>Role of AI:</b><br>
- Converts candidate speech to text (Whisper)
- Generates interview questions, summaries, and insights (GPT-4, GPT-3.5)
- Converts text prompts to audio (TTS)
- Tracks and analyzes usage for reporting

<b>Models Used:</b><br>
- OpenAI GPT-4, GPT-3.5 (NLP, summarization, question generation)
- Whisper (speech-to-text)
- TTS (text-to-speech, likely via OpenAI or another provider)

<b>Integration:</b><br>
- API-based (OpenAI keys in config)
- Modular routers for STT, TTS, and interview insights

<b>AI Tasks:</b><br>
- Natural language understanding and generation
- Audio transcription and synthesis
- Analytics and reporting

<b>Challenges & Solutions:</b><br>
- <b>Challenge:</b> Real-time audio processing<br>
  <b>Solution:</b> FastAPI async endpoints, efficient use of OpenAI/Whisper APIs<br>
- <b>Challenge:</b> Usage tracking<br>
  <b>Solution:</b> Dedicated <code>Usage</code> model in MongoDB, Prisma ORM

---

<h2 style="color: white;">Technical Breakdown</h2>

<b>Database:</b><br>
- MongoDB, managed via Prisma ORM
- Key model: <code>Usage</code> (tracks app, API, service, type, usage metrics, timestamps)

<b>Backend Architecture:</b><br>
- FastAPI app with modular routers for STT, TTS, and interview insights
- Middleware for CORS and usage tracking
- Prisma for async DB operations
- S3 integration for audio storage

<b>Frontend:</b><br>
- Next.js app with modular components for user/admin portals
- API integration for backend endpoints
- Real-time updates and analytics

<b>Key API Routes/Services:</b><br>
- <code>/stt</code> (speech-to-text)
- <code>/tts</code> (text-to-speech)
- <code>/interview-insights</code> (AI-powered analytics)
- Usage and admin endpoints

---

<h2 style="color: white;">User Journey Walkthrough</h2>

1. <b>User visits the portal</b> (Next.js frontend)
2. <b>User starts an interview</b> (audio or text)
3. <b>Frontend records/interacts with user</b> (audio capture, UI prompts)
4. <b>Frontend sends audio/text to backend</b> (<code>/stt</code> or <code>/interview-insights</code>)
5. <b>Backend processes request:</b>
   - If audio:  
     - Converts speech to text (Whisper)  
     - Stores audio in S3
   - If text:  
     - Sends to OpenAI for question generation/insights
6. <b>AI generates response/insights</b>
7. <b>Backend returns results to frontend</b>
8. <b>Frontend displays results, analytics, or next steps</b>
9. <b>Usage is tracked in the database</b>

---

<h2 style="color: white;">Text-Based Flowchart / Architecture</h2>

<pre style="color: white; background: #222; padding: 10px;">
User
  ↓
Frontend (Next.js)
  ↓
[User Action: Start Interview / Submit Audio/Text]
  ↓
API Call → Backend (FastAPI)
  ↓                                  
[Route: /stt, /tts, /interview-insights]
  ↓
Middleware (CORS, Usage Tracking)
  ↓
Business Logic
  ↓
  ├─ If Audio: Whisper STT → S3 Storage
  ├─ If Text: OpenAI GPT (NLP, Summarization, Q&A)
  └─ TTS: Text-to-Speech Service
  ↓
Database (MongoDB via Prisma) ←→ Usage Logging
  ↓
Response to Frontend
  ↓
User Sees Results, Analytics, Next Steps
</pre>

---

<h2 style="color: white;">Conclusion</h2>

This project demonstrates a robust, modern approach to automating and enhancing the recruitment process with AI. By combining FastAPI, Next.js, and advanced AI models (OpenAI, Whisper, TTS), the team delivered a scalable, modular platform that streamlines candidate interviews and provides actionable insights for recruiters.

<b>Key strengths:</b>
- Deep AI integration for real-time audio and text analysis
- Clean, modular codebase for rapid iteration and scaling
- Modern, user-friendly frontend

<b>Future opportunities:</b>
- Expand AI capabilities (custom models, more analytics)
- Integrate with more HR tools and platforms
- Enhance real-time feedback and reporting
