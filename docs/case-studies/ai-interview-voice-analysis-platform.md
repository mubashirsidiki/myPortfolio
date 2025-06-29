# Behind the Build: How We Created an AI-Powered Interview Voice Analysis Platform

## Introduction

In today’s competitive job market, communication skills are as important as technical expertise. Our project, the **Interview Warmup Voice Analysis Platform**, is designed for job seekers, career coaches, and HR professionals who want to gain deep insights into spoken communication during interviews. By leveraging advanced AI and speech analysis, this platform helps users understand not just what is said, but how it’s said—revealing confidence, nervousness, and other key emotional cues. What sets this project apart is its blend of state-of-the-art AI models, robust engineering, and a focus on actionable feedback for real-world improvement.

## General Overview

The platform analyzes recorded interview responses to extract rich voice features and emotional signals. Users upload or record their answers, and the system processes the audio to deliver:
- **Speech metrics** (syllables, pauses, rate, articulation)
- **Emotional cues** (confidence, nervousness, excitement, calmness)
- **Pronunciation and gender/mood detection**
- **Noise removal and speech enhancement**
- **Speech-to-text transcription**

**Key use cases:**
- Practicing for interviews and receiving objective feedback
- Coaching clients on communication skills
- Screening candidates with consistent, unbiased metrics

## Tech Stack

**Backend & Analysis:**
- **Python 3.11**: Core language for all processing
- **Praat & Parselmouth**: For acoustic and prosodic feature extraction
- **pandas, numpy, scipy**: Data processing and statistical analysis
- **praatio**: TextGrid parsing for detailed speech segmentation

**AI/ML Components:**
- **Wav2Vec2 (HuggingFace Transformers)**: Deep learning model for extracting speech features
- **Mayavoz**: Deep neural network for noise reduction and speech enhancement
- **SpeechRecognition & PocketSphinx**: For speech-to-text transcription

**Infrastructure:**
- **Poetry**: Dependency and environment management
- **Jupyter Notebooks**: Prototyping and experimentation

## How AI Powers the System

AI is at the heart of this platform, enabling nuanced analysis beyond traditional signal processing:

- **Noise Removal**: The Mayavoz DCCRN model denoises user audio, ensuring clean input for analysis.
- **Feature Extraction**: Facebook’s Wav2Vec2 model generates high-level speech representations, capturing subtle vocal patterns.
- **Speech Recognition**: Google Web Speech API and PocketSphinx transcribe spoken words for further analysis.
- **Emotion & Pronunciation Analysis**: Custom algorithms, powered by Praat and statistical models, infer confidence, nervousness, and pronunciation quality from extracted features.

**Integration:**  
AI models are accessed via Python APIs and HuggingFace’s SDK, with pre-trained weights for rapid, accurate inference. The pipeline is modular, allowing easy upgrades or swaps of AI components.

**Challenges & Solutions:**
- **Noisy Real-World Audio:** Integrated Mayavoz for robust denoising.
- **Emotion Detection:** Combined statistical analysis with acoustic features for reliable inference.
- **Model Compatibility:** Standardized audio preprocessing to ensure smooth handoff between modules.

## Technical Breakdown

**Data Storage & Structure:**
- Audio files are processed in-memory or from disk.
- Intermediate results (TextGrid, DataFrames) are generated for each analysis step.

**Backend Architecture:**
- Modular Python scripts and classes (e.g., `MyVoiceAnalysis`) encapsulate each analysis stage.
- Praat scripts are invoked via Parselmouth for low-level feature extraction.
- AI models (Wav2Vec2, Mayavoz) are loaded and run as needed, with results passed to downstream modules.

**Key API/Service Functions:**
- `MyVoiceAnalysis`: Extracts all prosodic and acoustic features, returns results as DataFrames.
- `Mayamodel.enhance`: Denoises audio before analysis.
- `Wav2Vec2Model`: Extracts deep speech features for advanced analytics.
- `recognize_sphinx_wav`: Transcribes speech for text-based feedback.

**Engineering Decisions:**
- Chose pre-trained, open-source models for rapid development and high accuracy.
- Used Praat for its proven reliability in speech science.
- Modularized code for easy extension (e.g., adding new emotion categories).

## User Journey Walkthrough

1. **User Uploads or Records Audio**
   - The user provides an interview response as a `.wav` file.

2. **Noise Removal**
   - The audio is passed through the Mayavoz model to remove background noise.

3. **Speech Feature Extraction**
   - The cleaned audio is analyzed by Praat (via Parselmouth) to extract:
     - Syllable count, pauses, speech rate, articulation, pitch statistics, etc.

4. **AI-Powered Analysis**
   - Wav2Vec2 extracts deep speech features.
   - Custom algorithms assess confidence, nervousness, and other emotions.
   - Pronunciation and gender/mood are inferred.

5. **Speech-to-Text Transcription**
   - The audio is transcribed using PocketSphinx or Google’s API.

6. **Results Presentation**
   - The user receives a detailed report:
     - Quantitative metrics (e.g., number of pauses, pitch variability)
     - Qualitative feedback (e.g., “Your delivery was confident and clear”)
     - Transcribed text for review

## Text-Based Flowchart / Architecture

```
User
  ↓
[Upload/Record Audio]
  ↓
[Noise Removal (Mayavoz)]
  ↓
[Speech Feature Extraction (Praat/Parselmouth)]
  ↓
[AI Analysis (Wav2Vec2, Custom Algorithms)]
  ↓
[Speech-to-Text (PocketSphinx/Google API)]
  ↓
[Results Aggregation]
  ↓
[User Receives Feedback & Report]
```

**Component Relationships:**
- User → Audio Input → Noise Remover → Feature Extractor → AI Models → Transcriber → Results Engine → User

## Conclusion

The Interview Warmup Voice Analysis Platform demonstrates how advanced AI and speech science can empower users to improve their communication skills. By combining robust engineering, state-of-the-art models, and a user-friendly workflow, we’ve created a tool that delivers actionable insights for interview preparation and coaching. This project showcases our team’s expertise in AI integration, audio processing, and user-centric design. Looking ahead, we plan to expand emotion categories, add real-time feedback, and integrate with video analysis for even richer insights.
