<h1 style="color: white;">Empowering Educators with AI</h1>
<h2 style="color: white;">The Story Behind Beacon House AI Presentation Platform</h2>


## <h3 style="color: white;">Introduction</h3>

Imagine a world where teachers can generate engaging, curriculum-aligned presentations in minutes, not hours. That's the vision behind the Beacon House AI Presentation Platform—a smart, AI-driven tool designed to help educators create high-quality, visually appealing slide decks with just a few clicks.

Built for schools, teachers, and educational organizations, this platform solves the age-old problem of time-consuming lesson preparation. By harnessing the power of artificial intelligence, it transforms simple prompts into full-fledged presentations, complete with speaker notes, charts, and tailored content. The result? More time for teaching, less time spent on formatting slides.

## <h3 style="color: white;">General Overview</h3>

At its core, the Beacon House AI Presentation Platform is a web-based solution that automates the creation of educational presentations. Users simply enter a topic, select a class or subject, and the platform generates a ready-to-use Google Slides presentation—complete with structured outlines, content, images, and even speaker notes.

The system integrates advanced AI models for content generation, leverages Google APIs for slide creation, and provides a seamless, secure user experience from login to download.

## <h3 style="color: white;">Tech Stack</h3>

- **Frontend:** Next.js 14, React, NextUI v2, Tailwind CSS, TypeScript
- **Backend:** FastAPI (Python), asynchronous architecture
- **Database:** MongoDB (via Prisma ORM)
- **AI/ML:** OpenAI GPT (via API), custom prompt engineering
- **Other Integrations:** Google Slides & Drive APIs, OAuth (Google SSO), Email notifications
- **DevOps/Infra:** Poetry (Python), Vercel (frontend), Uvicorn (backend), environment-based config

## <h3 style="color: white;">How AI Powers the Project</h3>

### <h4 style="color: white;">Overview of AI Usage</h4>

AI is the beating heart of the platform. It's responsible for:
- Generating slide outlines and detailed content from user prompts
- Creating speaker notes tailored to each slide
- Suggesting presentation structures and content improvements
- Summarizing, classifying, and enhancing user input

### <h4 style="color: white;">Model Details</h4>

- **Model:** OpenAI GPT (e.g., GPT-4, via API)
- **Usage:** Models are accessed via API (not fine-tuned), with carefully crafted prompts for each task (outline, content, notes, suggestions).
- **Prompt Engineering:** Custom templates and chaining strategies ensure the AI's output matches educational standards and slide formats.

### <h4 style="color: white;">AI Capabilities</h4>

- **Natural Language Processing:** Summarization, classification, content generation, and context-aware note creation.
- **Content Structuring:** AI classifies user input into slide types (introduction, body, conclusion, etc.) and generates JSON schemas for consistent formatting.
- **Recommendations:** The AI suggests improvements, additional slides, and even visual elements (like images or charts).

### <h4 style="color: white;">Integration</h4>

- **Real-Time Generation:** AI is called synchronously during the user's session, ensuring fast feedback.
- **Chaining:** Multiple AI calls may be chained (e.g., outline → content → notes) for richer results.
- **Latency & Cost:** Prompt design and retries are optimized for speed and token efficiency, with error handling for token limits or API failures.

### <h4 style="color: white;">Challenges Solved with AI</h4>

- **Scalability:** Manual slide creation is slow; AI enables instant, scalable content generation.
- **Consistency:** AI ensures every presentation follows best practices and educational guidelines.
- **Personalization:** Each output is tailored to the user's subject, class, and language needs.
- **Engineering Solutions:** The team implemented retries, prompt validation, and output mapping to handle API quirks, token limits, and ensure reliability.

## <h3 style="color: white;">Technical Deep Dive</h3>

### <h4 style="color: white;">Database Structure</h4>

- **MongoDB** is used for flexible, scalable storage.
- **Key Models:** User, Presentation, SpeakerNote
  - Presentations store URLs, outlines, AI responses, images, and user metadata.
  - SpeakerNotes are linked to slides and presentations for easy retrieval.

### <h4 style="color: white;">Backend Architecture</h4>

- **FastAPI** provides a modular, async API layer.
- **Routers** handle authentication, content generation, notes, suggestions, analytics, and integration with external services (Google, Beaconhouse).
- **Middleware** manages CORS, usage logging, and error handling.

### <h4 style="color: white;">API Structure</h4>

- **RESTful Endpoints:** For login, presentation generation, notes, suggestions, analytics, and user info.
- **Authentication:** JWT-based, with Google SSO integration.
- **Security:** Token verification, domain restrictions, and email validation.

### <h4 style="color: white;">Notable Engineering Challenges</h4>

- **Google API Integration:** Handling async slide creation, permissions, and file management.
- **AI Output Validation:** Ensuring AI responses fit the required schema and are safe for classroom use.
- **Performance:** Async I/O, background tasks, and efficient database queries keep the platform responsive.

### <h4 style="color: white;">Security, Scalability, and Performance</h4>

- **Security:** JWT tokens, OAuth, and environment-based secrets.
- **Scalability:** Async backend, stateless API, and cloud-native frontend.
- **Performance:** Caching, efficient batching, and error retries for AI and Google API calls.

## <h3 style="color: white;">User Journey Walkthrough</h3>

1. **Login:** The user signs in via Google SSO, ensuring secure access.
2. **Prompt Entry:** On the dashboard, the user enters a topic (e.g., "Boolean Algebra for Grade 9") and selects class/subject options.
3. **AI Magic:** The backend sends the prompt to the AI, which:
   - Classifies the outline (slide types)
   - Generates detailed content for each slide
   - Suggests images, charts, and speaker notes
4. **Slide Generation:** The system uses Google Slides API to create a new presentation, populating it with AI-generated content and visuals.
5. **Review & Edit:** The user receives a link to the Google Slides file, with options to review, edit, or download.
6. **Speaker Notes:** For each slide, AI-generated notes are available to help the teacher present confidently.
7. **Analytics:** The platform tracks usage, presentations created, and provides insights for both users and admins.
8. **Notifications:** The user receives an email with the presentation link and summary.

## <h3 style="color: white;">System Architecture Diagram</h3>
Below is a text-based flowchart showing the system architecture:

```
┌─────────────────┐
│      USER       │
│   (Teacher)     │
└─────────┬───────┘
          │
          ▼
┌─────────────────────────────────┐
│        FRONTEND                 │
│   (Next.js/React/NextUI)       │
│   • Dashboard Interface         │
│   • Topic Input Form           │
│   • Class/Subject Selection     │
└─────────┬───────────────────────┘
          │
          ▼
┌─────────────────────────────────┐
│      API GATEWAY                │
│      (FastAPI Backend)          │
└─────────┬───────────────────────┘
          │
          ├─────────────────────────────────────────────────────────┐
          │                                                         │
          ▼                                                         ▼
┌─────────────────┐                                    ┌─────────────────┐
│ AUTHENTICATION  │                                    │   AI SERVICE    │
│     SERVICE     │                                    │     LAYER       │
│                 │                                    │                 │
│ • Google SSO    │                                    │ • OpenAI GPT    │
│ • JWT Tokens    │                                    │ • Prompt Eng.   │
│ • User Session  │                                    │ • Content Gen.  │
└─────────────────┘                                    │ • Chaining      │
          │                                             └─────────┬───────┘
          │                                                       │
          ▼                                                       ▼
┌─────────────────┐                                    ┌─────────────────┐
│   CONTENT       │                                    │   NOTES         │
│   SERVICE       │                                    │   SERVICE       │
│                 │                                    │                 │
│ • Google Slides │                                    │ • Speaker Notes │
│ • Image Gen.    │                                    │ • AI Generated  │
│ • Chart Creation│                                    │ • Slide-linked  │
└─────────┬───────┘                                    └─────────────────┘
          │
          ├─────────────────────────────────────────────────────────┐
          │                                                         │
          ▼                                                         ▼
┌─────────────────┐                                    ┌─────────────────┐
│  SUGGESTION     │                                    │   ANALYTICS     │
│   SERVICE       │                                    │   SERVICE       │
│                 │                                    │                 │
│ • AI Recs.      │                                    │ • Usage Tracking│
│ • Improvements  │                                    │ • User Metrics  │
│ • Add Slides    │                                    │ • Admin Insights│
└─────────────────┘                                    └─────────────────┘
          │
          ▼
┌─────────────────────────────────┐
│      DATABASE                   │
│    (MongoDB via Prisma)         │
│                                 │
│ • User Profiles                 │
│ • Presentations                 │
│ • Speaker Notes                 │
│ • Analytics Data                │
└─────────┬───────────────────────┘
          │
          ▼
┌─────────────────────────────────┐
│    EMAIL SERVICE                │
│   (Notifications)               │
│                                 │
│ • Presentation Links            │
│ • Summary Emails                │
│ • Status Updates                │
└─────────┬───────────────────────┘
          │
          ▼
┌─────────────────┐
│      USER       │
│   (Teacher)     │
│   (Receives)    │
└─────────────────┘
```

**Flow Description:**
1. **User Input** → Teacher enters topic and selects class/subject
2. **Frontend Processing** → Next.js handles form validation and UI updates
3. **API Gateway** → FastAPI routes requests to appropriate services
4. **Authentication** → Google SSO verifies user identity
5. **AI Processing** → OpenAI generates content, notes, and suggestions
6. **Content Creation** → Google Slides API creates presentation
7. **Data Storage** → MongoDB stores all metadata and user data
8. **Notifications** → Email service sends presentation links
9. **User Receives** → Teacher gets ready-to-use presentation

**Key Integration Points:**
- **AI Service** is central to content generation, notes, and suggestions
- **Google APIs** handle slide creation and file management
- **MongoDB** stores all persistent data with Prisma ORM
- **Async Architecture** enables concurrent processing for better performance

## <h3 style="color: white;">Conclusion</h3>

The Beacon House AI Presentation Platform is a leap forward for educational technology. By blending advanced AI with seamless integrations and a user-friendly interface, it empowers teachers to focus on what matters most: teaching.

The AI component isn't just a feature—it's the engine that makes instant, high-quality, and personalized presentations possible. With a scalable, secure, and robust architecture, the platform is ready to grow, adapt, and serve educators everywhere.

**Looking ahead:** The team plans to add more languages, richer analytics, and deeper curriculum integration—showcasing a commitment to innovation and technical excellence. 