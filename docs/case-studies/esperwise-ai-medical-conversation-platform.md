<h1 style="color: white;">From Audio to Insights: Building an AI-Powered Medical Conversation Platform</h1>

<h2 style="color: white;">Introduction</h2>

In today’s fast-paced healthcare environment, clinicians are burdened with documentation, often spending more time on notes than with patients. Our project, <strong>EsperWise</strong>, is designed to change that. Built for healthcare providers, software vendors, and clinical teams, EsperWise leverages advanced AI to automatically generate clinical notes and extract medical insights from patient-clinician conversations. This not only saves time but also improves accuracy and compliance, making it a game-changer for modern healthcare.

<h2 style="color: white;">General Overview</h2>

EsperWise is a web-based platform that allows users to upload or record audio of medical conversations. The system transcribes, analyzes, and summarizes these conversations using state-of-the-art AI services. Key features include:

<ul>
<li><strong>Audio Upload & Recording:</strong> Users can upload existing audio files or record new ones directly in the browser.</li>
<li><strong>Automated Transcription & Summarization:</strong> Conversations are transcribed and summarized into structured clinical notes.</li>
<li><strong>Medical Insights Extraction:</strong> Integration with Amazon Comprehend Medical extracts medical terms, codes, and ontologies (ICD-10, SNOMED CT, RxNorm).</li>
<li><strong>Secure Storage & Access:</strong> All data is securely stored in AWS S3, with strict access controls.</li>
<li><strong>User-Friendly Interface:</strong> A modern, intuitive UI guides users through every step, from upload to results review.</li>
</ul>

<h2 style="color: white;">Tech Stack</h2>

<strong>Frontend:</strong><br>
- ReactJS (with TypeScript)<br>
- Cloudscape Design System (for AWS-styled UI components)<br>
- Vite (for fast development and builds)

<strong>Backend & Infrastructure:</strong><br>
- AWS Amplify (for deployment, authentication, and resource management)<br>
- Amazon Cognito (user authentication)<br>
- AWS Lambda (custom backend logic)<br>
- Amazon S3 (audio and results storage)<br>
- AWS IAM (fine-grained access control)

<strong>AI/ML Tools:</strong><br>
- Amazon Transcribe Medical (HealthScribe) for transcription and clinical note generation<br>
- Amazon Comprehend Medical for medical entity recognition and ontology inference<br>
- Amazon Polly for text-to-speech (audio generation)

<h2 style="color: white;">How AI Powers the System</h2>

AI is at the heart of EsperWise, transforming raw audio into actionable clinical insights:

<ul>
<li><strong>Transcription & Summarization:</strong><br>
Audio files are processed by Amazon Transcribe Medical (HealthScribe), which not only transcribes the conversation but also generates structured clinical documentation, segments the transcript, and maps evidence for each clinical note.</li>
<li><strong>Medical Entity Recognition:</strong><br>
The transcribed text is further analyzed by Amazon Comprehend Medical, which detects medical terms, conditions, medications, and infers standard medical codes (ICD-10, SNOMED CT, RxNorm).</li>
<li><strong>Integration:</strong><br>
All AI services are accessed securely via AWS SDKs and APIs, with results stored and linked for easy retrieval in the user interface.</li>
<li><strong>Challenges & Solutions:</strong><br>
<ul>
<li><strong>Audio Quality:</strong> Ensuring accurate transcription required robust audio preprocessing and user guidance.</li>
<li><strong>Data Security:</strong> Strict IAM roles and S3 policies were implemented to protect sensitive health data.</li>
<li><strong>Latency:</strong> Asynchronous job handling and progress notifications keep users informed during processing.</li>
</ul>
</li>
</ul>

<h2 style="color: white;">Technical Breakdown</h2>

<ul>
<li><strong>Database & Storage:</strong><br>
No traditional database is used; all audio files and results are stored in Amazon S3, with metadata managed via job names and S3 object keys.</li>
<li><strong>Backend Architecture:</strong><br>
<ul>
<li><strong>AWS Amplify</strong> orchestrates deployment and resource management.</li>
<li><strong>Lambda Functions</strong> handle custom tasks, such as enabling S3 bucket logging.</li>
<li><strong>RESTful APIs</strong> (via AWS SDK) connect the frontend to AWS services for job submission, status checks, and result retrieval.</li>
</ul>
</li>
<li><strong>Key Engineering Decisions:</strong><br>
<ul>
<li><strong>Serverless-first:</strong> Leveraging AWS managed services reduces operational overhead and scales automatically.</li>
<li><strong>Fine-grained IAM:</strong> Custom roles ensure only authenticated users can access or trigger sensitive operations.</li>
<li><strong>Modular Frontend:</strong> React components are lazy-loaded for performance and maintainability.</li>
</ul>
</li>
<li><strong>API Routes & Services:</strong><br>
<ul>
<li><strong>/new:</strong> Submit new audio for processing.</li>
<li><strong>/conversations:</strong> List and view processed conversations.</li>
<li><strong>/conversation/:id:</strong> View detailed results, including transcript, clinical notes, and extracted medical entities.</li>
</ul>
</li>
</ul>

<h2 style="color: white;">User Journey Walkthrough</h2>

<ol>
<li><strong>Login:</strong><br>
The user authenticates via a secure login (Amazon Cognito).</li>
<li><strong>Start New Conversation:</strong><br>
<ul>
<li>User clicks “New Conversation.”</li>
<li>They can upload an audio file or record directly in the browser.</li>
<li>User selects language and audio settings.</li>
</ul>
</li>
<li><strong>Submit Audio:</strong><br>
<ul>
<li>Audio is uploaded to a secure S3 bucket.</li>
<li>A HealthScribe job is created to process the audio.</li>
</ul>
</li>
<li><strong>Processing:</strong><br>
<ul>
<li>The backend monitors job status.</li>
<li>Once complete, results (transcript, clinical notes, insights) are stored in S3.</li>
</ul>
</li>
<li><strong>Review Results:</strong><br>
<ul>
<li>User navigates to “Conversations” to see a list of processed jobs.</li>
<li>Clicking a conversation shows the transcript, clinical notes, and medical insights.</li>
<li>Users can view evidence mapping, structured terms, and download results.</li>
</ul>
</li>
<li><strong>Advanced Insights:</strong><br>
Users can trigger further analysis with Amazon Comprehend Medical to extract ontologies and medical codes.</li>
</ol>

<h2 style="color: white;">Text-Based Flowchart / Architecture</h2>

<pre style="color: white; background: #222; padding: 1em;">
User → Web App (React)
    → [Login via Cognito]
    → [Upload/Record Audio]
        → Audio File → S3 Bucket
        → Trigger HealthScribe Job
            → HealthScribe (Transcribe Medical)
                → Transcription & Clinical Notes
                → Store Results in S3
            → (Optional) Comprehend Medical
                → Extract Medical Entities & Codes
                → Store Insights in S3
    → [Frontend Polls for Job Status]
    → [Display Results: Transcript, Notes, Insights]
    → [User Downloads or Reviews Data]
</pre>

<h2 style="color: white;">Conclusion</h2>

EsperWise demonstrates the power of combining cloud-native engineering with advanced AI to solve real-world healthcare challenges. The project showcases expertise in serverless architecture, secure AWS integration, and seamless AI orchestration. By automating clinical documentation and insight extraction, EsperWise empowers clinicians to focus on what matters most: patient care.

<strong>Future plans</strong> include expanding language support, integrating more AI models, and offering real-time analytics. If you’re looking to build innovative, AI-driven healthcare solutions, our team is ready to help you take the next step.
