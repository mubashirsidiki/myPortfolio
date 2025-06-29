---

# Behind the Build: Crafting a Custom AI Math Tutor for the Classroom

---

## Introduction

In today’s digital learning landscape, personalized education is more important than ever. Our team set out to build an AI-powered math chatbot tailored for a German math teacher and her students—a platform that not only solves math problems, but does so in the teacher’s unique, step-by-step style. This case study explores how we combined cutting-edge AI, thoughtful engineering, and real classroom feedback to create a truly impactful educational tool.

---

## General Overview

At its core, this platform is an interactive AI chatbot designed to help students solve math problems just like their teacher would. Students log in, ask questions, and receive detailed, step-by-step solutions—mirroring the exact methods taught in class. The system supports chat history, secure authentication, and a modern, user-friendly interface.

**Key Features:**
- AI-powered math problem solving
- Step-by-step solutions following the teacher’s method
- Chat history and session management
- Secure login (Google or credentials)
- Responsive, accessible UI

**Use Cases:**
- Homework help for students
- Supplementary teaching tool for educators
- Consistent, method-aligned explanations

---

## Tech Stack

**Frontend:**
- **Next.js 14** (App Router, React Server Components)
- **React** (18+)
- **Tailwind CSS** & **shadcn/ui** for styling
- **Radix UI** for accessible components

**Backend:**
- **Next.js API routes** (serverless functions)
- **Vercel AI SDK** for streaming chat and AI integration
- **Vercel KV** (key-value store) for chat/session data

**Authentication:**
- **NextAuth.js** (credentials + Google OAuth)

**AI/ML:**
- **OpenAI GPT-3.5/4** (with support for Anthropic, Cohere, Hugging Face, LangChain)
- **Custom fine-tuning** and **prompt engineering**
- **Manual solution database** for math books

**Infrastructure:**
- **Vercel** (hosting, serverless, KV storage)
- **TypeScript** for type safety

---

## How AI Powers the System

AI is the heart of this platform. Here’s how it works:

- **Initial Approach:**  
  We started with generic LLMs (like GPT-3.5) to answer math questions. However, these models often used different solution methods than the teacher, causing confusion for students.

- **Fine-Tuning:**  
  To address this, we fine-tuned the model using solutions provided by the teacher. This helped the AI mimic the teacher’s step-by-step approach, improving consistency and learning outcomes.

- **Hybrid Solution (Final Iteration):**  
  For maximum accuracy, we built a database of manual solutions from the math books. When a student asks a question, the system retrieves the relevant solution (by question number) and includes it in the AI’s prompt. The AI then explains the solution in a conversational, student-friendly way.

- **Integration:**  
  - **Vercel AI SDK** streams responses for a real-time chat experience.
  - **OpenAI API** (and other providers) power the LLM.
  - **Prompt engineering** ensures the AI follows the teacher’s method.

**AI Tasks:**
- Natural Language Understanding (NLP)
- Step-by-step solution generation
- Explanation and elaboration
- Contextual adaptation to teacher’s style

**Challenges & Solutions:**
- **Challenge:** LLMs not following the teacher’s method  
  **Solution:** Fine-tuning and prompt engineering
- **Challenge:** Inconsistent or incorrect answers  
  **Solution:** Hybrid approach with a solution database + AI explanation

---

## Technical Breakdown

**Database & Storage:**
- **Vercel KV** stores chat history, user sessions, and solution references.
- **Manual solution database** (for math books) is indexed by question number.

**Backend Architecture:**
- **Next.js API routes** handle authentication, chat, and restricted content.
- **Server Actions** manage chat state, user sessions, and data retrieval.
- **AI integration** via Vercel AI SDK and OpenAI API.

**Key Engineering Decisions:**
- **Streaming UI:** Real-time feedback using Vercel AI SDK.
- **Serverless:** Scalable, low-maintenance deployment on Vercel.
- **Hybrid AI+DB:** Ensures both accuracy and pedagogical alignment.

**API & Internal Services:**
- `/api/auth/[...nextauth]`: Handles authentication (credentials, Google)
- `/api/restricted`: Example of protected content
- actions.tsx: Core AI logic, chat state, and tool invocation
- actions.ts: Chat/session management, data access

---

## User Journey Walkthrough

**Step 1: Login**
- User visits the platform and logs in (Google or credentials).

**Step 2: Start a Chat**
- User enters a math question (e.g., “How do I solve equation 3.2 from the book?”).

**Step 3: Backend Processing**
- The system checks if the user is authenticated.
- Retrieves the relevant solution from the manual solution database (by question number).
- Constructs a prompt for the AI, embedding the solution and instructions to explain it in the teacher’s style.

**Step 4: AI Response**
- The AI (via OpenAI API) generates a step-by-step explanation, streamed to the user in real time.

**Step 5: User Interaction**
- User can ask follow-up questions, request clarifications, or try another problem.
- All chat history is saved for future reference.

**Step 6: Logout or Continue**
- User can log out or continue chatting.

---

## Text-Based Flowchart / Architecture

```
User → Frontend (Next.js/React UI)
    → [Login Page] → Auth API (NextAuth.js)
        → [Success] → Chat Interface
            → [User submits question]
                → Backend (API Route/Server Action)
                    → [Check authentication]
                    → [Retrieve solution from DB by question number]
                    → [Construct AI prompt with solution]
                    → AI Model (OpenAI GPT, fine-tuned)
                        → [Generate step-by-step explanation]
                    → Backend streams response
                → Frontend displays AI response in chat
            → [User asks follow-up] → (loop to Backend)
    → [Chat history/session stored in Vercel KV]
    → [Logout or continue]
```

---

## Conclusion

This project demonstrates how thoughtful AI integration can transform education—bridging the gap between generic technology and personalized learning. By iterating with real classroom feedback, fine-tuning models, and ultimately combining AI with a curated solution database, we delivered a platform that truly supports both teachers and students.

Our team’s technical expertise, creative problem-solving, and commitment to user experience made this project a success. Looking ahead, we plan to expand the platform to support more subjects, languages, and adaptive learning features—empowering educators and learners everywhere.

---

**Notable Iterations:**
- Built for a German math teacher’s classroom
- Evolved from generic LLMs → fine-tuned models → hybrid DB+AI solution
- Achieved high accuracy and pedagogical alignment by embedding teacher-provided solutions in the AI workflow
