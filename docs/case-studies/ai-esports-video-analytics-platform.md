# AI-Powered Esports Video Analytics Platform

<h2 style="color: white;">Introduction</h2>

In the fast-growing world of esports, analyzing gameplay videos for highlights, statistics, and player performance is both crucial and time-consuming. Our project—an AI-powered video analytics platform—was built to automate this process for tournament organizers, teams, and content creators. By leveraging advanced computer vision and AI models, we extract key moments (like "kill cams" and scoreboard data) from raw gameplay footage, making insights accessible, searchable, and actionable.

<h2 style="color: white;">General Overview</h2>

The platform ingests raw gameplay videos, processes them through a robust AI pipeline, and delivers structured data and highlight clips. Key features include:

- **Automated Kill Cam Extraction:** Detects and segments highlight moments.
- **Scoreboard OCR:** Reads and digitizes in-game scoreboard data.
- **Video Preprocessing:** Standardizes video format, resolution, and quality for consistent AI analysis.
- **Cloud Integration:** Stores and retrieves processed assets via AWS S3.
- **User Dashboard:** Lets users upload videos, view results, and download highlights.

<h2 style="color: white;">Tech Stack</h2>

**Frontend:**  
- React (TypeScript) with Vite for fast, modern UI  
- Material UI for design  
- Redux for state management  
- React Router for navigation

**Backend:**  
- NestJS (TypeScript) REST API  
- TypeORM for database operations  
- AWS SDK for S3 integration  
- Docker & Kubernetes for deployment

**AI/ML:**  
- FastAPI (Python) for AI microservices  
- OpenCV, PyTorch, ONNX, OpenVINO for computer vision and inference  
- Google Cloud Vision API for OCR  
- OpenAI API for advanced language tasks  
- Ultralytics YOLO for object detection

**Infrastructure:**  
- Docker Compose for local development  
- Helm & Kubernetes for scalable deployment  
- AWS S3 for media storage

<h2 style="color: white;">How AI Powers the System</h2>

AI is the heart of the platform, automating what would otherwise be hours of manual video review:

- **Video Preprocessing:**  
  - Uses FFmpeg and OpenCV to standardize video format (MP4, 360p, 10fps, grayscale, edge detection).
- **Kill Cam & Scope Detection:**  
  - Custom-trained YOLO models (via Ultralytics) identify and segment highlight moments.
  - Edge detection and contour analysis (Canny, findContours) pinpoint relevant frames.
- **Scoreboard OCR:**  
  - Google Cloud Vision API extracts text from scoreboard images.
  - OpenAI’s GPT models may be used to parse, validate, or summarize extracted data.
- **Cloud Integration:**  
  - Processed files are uploaded to AWS S3 for persistent, scalable storage.
- **Challenges Solved:**  
  - Handling diverse video qualities with preprocessing.
  - Achieving high-accuracy detection with custom-trained models.
  - Efficient, asynchronous processing using FastAPI and background jobs.

<h2 style="color: white;">Technical Breakdown</h2>

- **Database & Storage:**  
  - Uses AWS S3 for storing raw and processed videos/images.
  - Backend likely uses a relational database (via TypeORM) for metadata and user management.

- **Backend Architecture:**  
  - Microservices: AI runs as a separate FastAPI service, backend as NestJS.
  - RESTful APIs connect frontend, backend, and AI services.
  - Background jobs handle file uploads and post-processing.

- **Key API Routes:**  
  - `/scope/detection`: Accepts a video, returns detected highlight timestamps.
  - `/scoreboard/extraction`: Accepts an image, returns parsed scoreboard data.

- **Engineering Decisions:**  
  - Decoupled AI and backend for scalability.
  - Used industry-standard models (YOLO, OpenCV) and cloud APIs for reliability.
  - Employed Docker/Kubernetes for easy deployment and scaling.

<h2 style="color: white;">User Journey Walkthrough</h2>

1. **Upload:**  
   - User logs in and uploads a gameplay video via the dashboard.

2. **Preprocessing:**  
   - Frontend sends the video to the backend, which stores it in S3 and triggers the AI service.

3. **AI Analysis:**  
   - AI service preprocesses the video (resizing, grayscale, edge detection).
   - Runs object detection to find kill cams and scopes.
   - Extracts scoreboard frames and runs OCR.

4. **Data Storage:**  
   - Processed highlights and extracted data are saved to S3.
   - Metadata and results are stored in the backend database.

5. **Results Display:**  
   - User receives a notification when processing is complete.
   - Dashboard displays highlight clips, scoreboard data, and download options.

<h2 style="color: white;">Text-Based Flowchart / Architecture</h2>

```
User
  ↓
Frontend (React)
  ↓ (uploads video, requests results)
Backend (NestJS API)
  ↓ (stores file, triggers AI)
AI Service (FastAPI)
  → Preprocess video (OpenCV, FFmpeg)
  → Detect highlights (YOLO, custom models)
  → Extract scoreboard (Google Vision OCR)
  → Summarize/validate (OpenAI API)
  ↓
AWS S3 (stores processed files)
  ↓
Backend (updates DB, notifies user)
  ↓
Frontend (displays results, allows downloads)
```

<h2 style="color: white;">Conclusion</h2>

This project demonstrates our ability to blend advanced AI, scalable cloud infrastructure, and user-friendly design to solve real-world problems in esports analytics. By automating video review and data extraction, we empower users to focus on strategy and storytelling—not manual labor. Our modular, cloud-native approach means the platform can easily expand to new games, analytics, or media types.

**Future plans:**  
- Add real-time analytics and live event support  
- Expand AI models for new games and event types  
- Integrate deeper insights and reporting tools

