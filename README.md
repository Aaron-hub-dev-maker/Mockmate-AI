# MockMate AI — Intervexa

**An AI-powered multimodal interview platform for structured candidate assessment.**

MockMate AI, also presented as **Intervexa** in the project conference paper, is an AI-driven interview assessment platform designed to support recruitment at scale. It combines resume-aware question generation, interview answer evaluation, audio and video analysis, aptitude and coding assessments, and interview-integrity monitoring in one workflow.

> **Project context:** Academic major project developed at Rajagiri School of Engineering & Technology (RSET), Kerala, India. The system is intended to support recruiters with structured information and feedback—not replace human hiring decisions.

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Interview Workflow](#interview-workflow)
- [Technology Stack](#technology-stack)
- [Evaluation Results](#evaluation-results)
- [Results and Outputs](#results-and-outputs)
- [Ethics, Fairness, and Limitations](#ethics-fairness-and-limitations)
- [Repository Setup](#repository-setup)
- [Publication](#publication)
- [Future Work](#future-work)
- [Contributing](#contributing)
- [License](#license)

## Overview

Traditional interviews can be difficult to scale and may rely on inconsistent manual evaluation. MockMate AI aims to make assessment more structured by combining several evidence sources:

- Candidate resume and job-description context
- Technical and behavioral interview responses
- Speech transcription and audio-derived features
- Video-derived behavioral signals
- Aptitude and coding assessment results
- Interview-integrity events and logs

The platform uses a Retrieval-Augmented Generation (RAG) pipeline to generate role-specific questions, evaluates responses against structured criteria, and consolidates assessment outputs into candidate scores and feedback.

## Key Features

### 1. Resume Parsing and Context-Aware Questions

- Extracts candidate information from PDF resumes.
- Structures skills, education, certifications, and experience using DSPy and Pydantic.
- Uses resume and job-role context to retrieve relevant information and generate tailored interview questions.

### 2. AI Interview and Answer Evaluation

- Generates technical and behavioral questions based on candidate and role context.
- Evaluates responses for technical knowledge, relevance, language proficiency, and clarity.
- Produces structured scores and feedback.

### 3. Audio Analysis

- Uses Whisper for speech-to-text transcription.
- Analyzes speech rate, pauses, filler words, vocal energy, and pitch variation.
- Produces an audio-derived confidence indicator.

### 4. Video Analysis

- Uses MediaPipe and OpenCV to analyze visual signals such as gaze direction, blink rate, head movement, and facial landmarks.
- Combines video-derived features with other assessment signals for a broader view of interview performance.

### 5. Aptitude and Coding Assessments

- Retrieves role-relevant coding questions through semantic search.
- Selects aptitude questions from a structured question bank with balanced difficulty levels.
- Integrates assessment scores into the overall evaluation.

### 6. Security and Interview Integrity

- Uses speaker-recognition techniques to help identify an unexpected speaker.
- Detects events such as multiple faces or no face in the camera frame.
- Tracks selected hand-to-face behaviors and background changes.
- Logs potential violations for review.

### 7. Scoring and Feedback

- Normalizes scores from aptitude, coding, technical interview, and confidence analysis.
- Generates structured feedback for candidates and recruiters.
- Supports candidate comparison while keeping human oversight in the hiring process.

## System Architecture

The platform is organized into the following layers:

| Layer | Responsibility |
|---|---|
| Presentation Layer | Candidate and recruiter interfaces; captures responses and displays reports. |
| Interview Orchestration Layer | Manages sessions, delivers questions, and controls assessment flow. |
| AI Intelligence Layer | Resume parsing, RAG-based question generation, and answer evaluation. |
| Multimodal Analysis Layer | Speech transcription, audio feature extraction, and video analysis. |
| Security & Integrity Layer | Speaker verification, face-count checks, and potential integrity-event logging. |
| Hiring Tools Integration Layer | Connects aptitude tests, coding tests, and interview assessments. |
| Scoring & Feedback Layer | Normalizes and aggregates scores and generates feedback. |
| Data Layer | Stores resumes, questions, company objectives, feedback, cache data, session state, and logs. |

### High-Level Flow

```text
Candidate Resume + Job Description
                |
                v
       Resume Parsing / Structuring
                |
                v
       Context Retrieval (RAG Pipeline)
                |
                v
       Adaptive Interview Orchestration
                |
        +-------+--------+
        |       |        |
        v       v        v
    Interview  Coding  Aptitude
        |
        +--------------------------+
        |                          |
        v                          v
   Audio Analysis             Video Analysis
        |                          |
        +------------+-------------+
                     |
                     v
           Security & Integrity Checks
                     |
                     v
          Score Normalization & Aggregation
                     |
                     v
             Candidate Feedback / Ranking
```

## Interview Workflow

1. A candidate uploads a resume and the relevant job requirements are supplied.
2. The resume parser converts the resume into a structured candidate profile.
3. The RAG pipeline retrieves relevant candidate and role context.
4. The orchestration layer selects and delivers the next assessment stage.
5. Candidate responses are transcribed and evaluated; audio and video features are analyzed when enabled.
6. Aptitude and coding results are collected.
7. The scoring layer combines assessment results and generates structured feedback.
8. Recruiters review the report and make the final hiring decision.

An example adaptive sequence is:

`Interview → Coding → Interview → Aptitude`

## Technology Stack

| Area | Technologies |
|---|---|
| Frontend | React.js, HTML, CSS, JavaScript, TypeScript |
| Backend | Python, FastAPI, Uvicorn |
| AI / LLM Integration | OpenRouter APIs, GPT-4o, Claude Sonnet 4 |
| Resume Structuring | DSPy, Pydantic |
| Retrieval and Embeddings | Retrieval-Augmented Generation (RAG), Sentence Transformers, ChromaDB |
| Speech Processing | Whisper Automatic Speech Recognition (ASR) |
| Video / Computer Vision | MediaPipe, OpenCV |
| Audio Speaker Verification | SpeechBrain |
| Database | Supabase PostgreSQL |
| Workflow Orchestration | LangGraph-based workflow |
| API Testing and Development | Swagger, Postman, Visual Studio Code |
| Version Control | Git, GitHub |

*The technologies listed reflect the project documentation. Exact dependencies and configuration may differ by repository version.*

## Evaluation Results

The project documentation reports a feasibility evaluation using **15 simulated interview sessions**: five sessions each for text-only, text-plus-audio, and full multimodal configurations.

| Configuration | Relevance Score | Confidence Score | Completion Rate |
|---|---:|---:|---:|
| Text-only | 0.72 | 0.45 | 82% |
| Text + Audio | 0.81 | 0.63 | 90% |
| Full Multimodal (Text + Audio + Video) | 0.89 | 0.78 | 96% |

The reported results show improvements across these measures as additional modalities are included. The paper also reports that the security layer flagged **14 of 15 injected anomalous events (93.3%)** under controlled test conditions.

> **Important:** These are project-reported results from simulated scenarios, not evidence of validated performance on a large, real-world hiring dataset. Further evaluation is needed before using such scores in actual recruitment decisions.

## Results and Outputs

The screenshots below show selected screens and outputs from the application. Ensure the images are committed to the repository in the `images` directory with the exact filenames shown.

![Interviewer Login](Assets/1.png)

![Interviewer Dashboard](Assets/2.png)

![Candidate Management](Assets/3.png)

![Job Description Setup](Assets/4.png)

![Candidate Interview Status](Assets/5.png)

![Candidate Ranking](Assets/6.png)

![Audio Confidence Analysis](Assets/7.png)

![Multimodal Video Analysis](Assets/8.png)

![AI Question Generator and Resume Analyzer](Assets/9.png)

![AI Question Generator and Resume Analyzer](Assets/10.png)

![AI Question Generator and Resume Analyzer](Assets/11.png)

![AI Question Generator and Resume Analyzer](Assets/12.png)

![AI Question Generator and Resume Analyzer](Assets/13.png)

![AI Question Generator and Resume Analyzer](Assets/14.png)

## Ethics, Fairness, and Limitations

The system is designed to support—not replace—human decision-making. Automated behavioral signals can be affected by camera placement, lighting, audio quality, disability, neurodiversity, individual communication styles, and cultural differences. Eye contact or facial behavior should not be treated as a definitive measure of competence or confidence.

Key limitations identified in the project include:

- Evaluation was conducted on simulated interviews rather than a large real-world recruitment dataset.
- Audio and video quality can affect feature extraction.
- Real-time multimodal processing and cloud model calls introduce computational overhead and latency.
- Behavioral indicators may vary across individuals and cultures.
- More extensive fairness testing, calibration, explainability, privacy controls, and human review are needed before deployment.

Sensitive voice, video, and resume data should be handled with appropriate consent, access controls, retention limits, and applicable data-protection requirements.

## Repository Setup

The project documentation identifies the main technologies but does not specify a verified, repository-wide installation procedure. The commands below are starting points; adapt them to the actual folder structure, entry points, and dependency files in the repository.

### Prerequisites

- Python version compatible with the backend's dependency file
- Node.js and npm compatible with the frontend
- Access to the configured database
- API credentials for any external language-model provider used by the project
- A microphone and webcam for audio/video interview features

### 1. Clone the Repository

Replace the placeholders with your actual GitHub repository URL and folder name.

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

### 2. Configure the Backend

Create a Python virtual environment:

```bash
python -m venv .venv
```

Activate it in Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Or activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

If the backend includes a `requirements.txt` file, install its dependencies:

```bash
pip install -r requirements.txt
```

Configure the environment variables expected by the codebase. These may include model-provider API keys and Supabase/database credentials. **Do not commit API keys, passwords, or other secrets to GitHub.**

If the backend entry point is `main.py` and the FastAPI application is named `app`, a typical development command is:

```bash
uvicorn main:app --reload
```

Adjust the module and application names to match the actual project.

### 3. Configure the Frontend

From the frontend directory, install dependencies:

```bash
npm install
```

Start the development server using the script defined in `package.json`, commonly:

```bash
npm run dev
```

The exact commands, ports, environment-variable names, and database migrations should be confirmed against the repository's actual files.

**Project guide:** Dr. Jisha G., Associate Professor and Assistant Head of Department, Department of Computer Science and Engineering, RSET.

## Publication

**“Intervexa: A Fair and Scalable AI-Driven Multimodal Interviewing Platform for Automated Candidate Assessment.”**

The project documentation states that the paper was communicated to the **International Conference on Contemporary Computing and Communications (IC4), 2026**. This wording indicates submission/communication; do not describe the paper as accepted or published unless that status is confirmed.

## Future Work

- Validate the platform on larger and more representative datasets.
- Improve inference latency and deployment scalability.
- Expand multilingual interview support.
- Calibrate evaluation across demographic and communication differences.
- Improve anomaly detection and explainability.
- Explore domain-specific interviews beyond technical roles.
- Strengthen privacy, consent, and human-review mechanisms.

## Contributing

If you plan to accept contributions, document your preferred contribution workflow—for example, opening an issue before submitting a pull request.

## License

No license was specified in the supplied project documentation. Add a `LICENSE` file and update this section before allowing others to reuse or redistribute the code.

---

**Disclaimer:** MockMate AI / Intervexa is an academic project and decision-support prototype. Its generated scores and behavioral estimates should not be treated as definitive measures of candidate ability or used as the sole basis for hiring decisions.
