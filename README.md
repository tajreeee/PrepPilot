# PrepPilot

# 🎤 PrepPilot — Adaptive AI Interview Simulator

> **Practice interviews. Improve your answers. Get better before the real interview.**

PrepPilot is an **AI-powered, time-constrained interview simulator** that conducts realistic technical and behavioral interviews. The system dynamically generates questions, evaluates candidate responses, adapts question difficulty, asks contextual follow-up questions, and provides a detailed performance report after the interview.

Unlike a simple chatbot that only asks interview questions, **PrepPilot manages the complete interview process** — including time, interview state, question selection, evaluation, difficulty adaptation, analytics, and progress tracking.

---

## ✨ Features

### ⏱️ Time-Constrained Interviews

Choose an interview duration such as **5, 10, or 15 minutes** and complete the interview under real interview time pressure.

### 🤖 AI Question Generation

Questions are dynamically generated based on:

* Job role
* Experience level
* Interview type
* Difficulty
* Previous questions
* Previous answers
* Candidate performance
* Remaining interview time

### 🔄 Contextual Follow-Up Questions

PrepPilot analyzes the candidate's previous answer and can ask a relevant follow-up question instead of randomly changing topics.

**Example:**

> **AI:** What is polymorphism?

> **Candidate:** Polymorphism means one thing can have multiple forms.

> **AI:** Can you give me a Java example of polymorphism?

This makes the interview feel more like a real conversation.

### 🎚️ Adaptive Difficulty

The interview dynamically adjusts difficulty based on the candidate's performance:

```text
Score ≥ 80  → Increase difficulty
Score 60–79 → Maintain difficulty
Score < 60  → Decrease difficulty
```

### ⏰ Time-Aware Question Selection

PrepPilot considers the remaining interview time when selecting the next question.

```text
10 minutes remaining
        ↓
Technical questions
        ↓
5 minutes remaining
        ↓
Problem-solving questions
        ↓
2 minutes remaining
        ↓
Short behavioral question
        ↓
Interview ends
```

### 📝 Multi-Dimensional Answer Evaluation

Each answer is evaluated across multiple criteria:

* Technical accuracy
* Relevance
* Communication
* Completeness
* Overall performance

Candidates also receive actionable feedback after each response.

### 📊 Performance Report

After completing an interview, PrepPilot generates a detailed performance report containing:

* Overall score
* Technical knowledge
* Communication
* Problem solving
* Relevance
* Completeness
* Strengths
* Areas for improvement
* Time analysis

### 📈 Interview History

Previous interviews are stored so candidates can track their improvement over time.

```text
Interview 1 → 64
Interview 2 → 69
Interview 3 → 73
Interview 4 → 78
Interview 5 → 81
```

### 🧠 Recurring Weakness Tracker

PrepPilot identifies weaknesses that repeatedly appear across multiple interviews.

**Example:**

```text
Recurring Weaknesses

1. Behavioral questions
2. Giving concrete examples
3. Concise communication
4. Technical fundamentals
```

The system can then recommend targeted practice areas.

### 🧑‍💼 Interviewer Personalities

Choose different interviewer styles:

* Professional
* Friendly
* Strict
* HR

Each personality changes the way the AI communicates with the candidate.

---

## 🎯 Supported Interview Types

The MVP supports:

* Technical interviews
* Behavioral interviews
* Technical + Behavioral interviews

### Supported Roles

* Software Engineer
* Web Developer
* Data Analyst
* ML Engineer

More roles can be added in future versions.

---

## 🏗️ System Architecture

```text
                    ┌─────────────────┐
                    │     Next.js     │
                    │    Frontend     │
                    └────────┬────────┘
                             │
                          REST API
                             │
                    ┌────────▼────────┐
                    │     FastAPI     │
                    │     Backend     │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
       Interview Engine   LLM API        SQLite
              │
       ┌──────┴──────┐
       ▼             ▼
     Timer       Evaluation
       │             │
       └──────┬──────┘
              ▼
       Interview Report
```

---

## 🛠️ Tech Stack

### Frontend

* **Next.js**
* **TypeScript**
* **React**
* **Tailwind CSS**
* **Recharts**

### Backend

* **FastAPI**
* **Python**

### AI

* Large Language Model API
* Structured JSON responses for question generation and evaluation

### Database

* **SQLite**

SQLite is sufficient for the MVP and can later be replaced with PostgreSQL.

---

## 🔄 How It Works

The complete interview flow is:

```text
User
 ↓
Select Job Role
 ↓
Select Experience
 ↓
Select Difficulty
 ↓
Select Interview Type
 ↓
Select Duration
 ↓
Select Interviewer Personality
 ↓
Start Interview
 ↓
AI Generates Question
 ↓
Candidate Answers
 ↓
AI Evaluates Answer
 ↓
Update Performance
 ↓
Determine Difficulty
 ↓
Consider Remaining Time
 ↓
Generate Next Question
 ↓
Repeat
 ↓
Time = 0
 ↓
Generate Final Report
 ↓
Save Interview History
```

---

## 🧠 AI Interview Engine

The backend controls the interview logic rather than allowing the LLM to control the entire application.

The process is:

```text
Candidate Answer
       ↓
Check Remaining Time
       ↓
Evaluate Answer
       ↓
Update Score
       ↓
Determine Next Difficulty
       ↓
Determine Question Type
       ↓
Generate Next Question
       ↓
Save Interview Data
       ↓
Return Question
```

This separation makes the system more predictable, controllable, and easier to maintain.

---

## 📦 Example AI Input

The application sends structured information to the LLM:

```json
{
  "role": "Software Engineer",
  "experience": "Fresher",
  "difficulty": "Medium",
  "interview_type": "Technical + Behavioral",
  "remaining_seconds": 420,
  "previous_questions": [
    "Tell me about yourself.",
    "What is polymorphism?"
  ],
  "previous_answer": "Polymorphism means one thing can have multiple forms."
}
```

The AI can return:

```json
{
  "question": "Can you give me a Java example of polymorphism?",
  "type": "technical",
  "difficulty": "medium",
  "expected_topics": [
    "compile-time polymorphism",
    "runtime polymorphism"
  ]
}
```

---

## 📝 Example Answer Evaluation

The AI evaluates each response using structured output:

```json
{
  "technical_accuracy": 82,
  "relevance": 90,
  "communication": 75,
  "completeness": 70,
  "overall": 80,
  "feedback": "Good explanation, but provide a concrete example."
}
```

Structured responses allow the backend to calculate scores and generate consistent analytics.

---

## ⏱️ Secure Interview Timer

The frontend displays the countdown:

```text
10:00
09:59
09:58
...
```

However, the backend also stores:

```text
interview_started_at
interview_duration
```

The actual remaining time is calculated using the server-side interview state rather than trusting the browser timer alone.

This prevents users from manipulating the client-side countdown.

---

## 🗄️ Database Structure

### Users

```text
users
-----
id
name
email
created_at
```

### Interviews

```text
interviews
----------
id
user_id
role
experience
difficulty
duration
personality
started_at
ended_at
overall_score
```

### Questions

```text
questions
---------
id
interview_id
question_text
question_type
difficulty
asked_at
```

### Answers

```text
answers
-------
id
question_id
answer_text
response_time
technical_score
communication_score
relevance_score
overall_score
feedback
```

---

## 🔌 API Endpoints

| Method | Endpoint                      | Description                          |
| ------ | ----------------------------- | ------------------------------------ |
| `POST` | `/api/interviews`             | Create an interview                  |
| `POST` | `/api/interviews/{id}/start`  | Start an interview                   |
| `POST` | `/api/interviews/{id}/answer` | Submit an answer                     |
| `GET`  | `/api/interviews/{id}`        | Get interview details                |
| `GET`  | `/api/interviews/{id}/result` | Get final report                     |
| `GET`  | `/api/interviews/history`     | Get previous interviews              |
| `GET`  | `/api/dashboard`              | Get progress and weakness statistics |

---

## 🖥️ Main Pages

PrepPilot consists of five main pages:

### 1. Landing Page

Introduces PrepPilot and allows users to start an interview.

### 2. Interview Setup

Users select:

* Job role
* Experience
* Difficulty
* Interview type
* Duration
* Interviewer personality

### 3. Interview Screen

Displays:

* AI question
* Remaining time
* Answer input
* Question number
* Submit button

### 4. Interview Report

Displays:

* Overall score
* Category scores
* Strengths
* Weaknesses
* Time analysis
* AI feedback

### 5. Dashboard

Displays:

* Interview history
* Score progression
* Recurring weaknesses
* Recommended practice areas

---

## 📊 Time Management Analytics

Because interviews are explicitly time-based, PrepPilot also analyzes how candidates use their time.

**Example:**

```text
Questions answered:     9
Average answer time:   42 sec
Longest answer:       1m 38s
Shortest answer:      12 sec
Time utilization:      87%
```

The system can provide feedback such as:

> You spent too much time on technical explanations, leaving less time for behavioral questions.

---

## 🆚 PrepPilot vs ChatGPT

PrepPilot is **not designed to be another ChatGPT-style chatbot**.

### ChatGPT

```text
User
 ↓
"Ask me an interview question"
 ↓
AI Question
 ↓
User Answer
 ↓
AI Feedback
```

### PrepPilot

```text
Candidate
 ↓
Choose Role + Duration
 ↓
Timed Interview
 ↓
AI Question
 ↓
Answer
 ↓
Multi-Dimensional Evaluation
 ↓
Adaptive Difficulty
 ↓
Contextual Follow-Up
 ↓
Time-Aware Question Selection
 ↓
Interview Ends Automatically
 ↓
Performance Analysis
 ↓
Historical Weakness Tracking
```

The key difference is that **PrepPilot is an application built around an LLM**, rather than simply being an interface to an LLM.

The application itself manages interview state, timing, question selection, evaluation, adaptation, analytics, and progress tracking.

---

## 🚀 MVP Scope

The core MVP focuses on:

| Feature                        | Priority |
| ------------------------------ | -------- |
| Job/role selection             | ⭐⭐⭐      |
| Timed interview                | ⭐⭐⭐⭐⭐    |
| AI question generation         | ⭐⭐⭐⭐⭐    |
| AI answer evaluation           | ⭐⭐⭐⭐⭐    |
| Dynamic follow-ups             | ⭐⭐⭐⭐⭐    |
| Adaptive difficulty            | ⭐⭐⭐⭐     |
| Final performance report       | ⭐⭐⭐⭐⭐    |
| Interview history & weaknesses | ⭐⭐⭐⭐     |

---

## 🗺️ Future Work

Potential future improvements include:

* 🎙️ Voice-based interviews
* 🗣️ Speech-to-text
* 🔊 AI interviewer voice
* 👤 AI interviewer avatar
* 💼 Job-description-specific interviews
* 🔗 Resume/CV-based interview generation
* 📱 Mobile application
* 📊 Advanced performance analytics

The MVP intentionally focuses on **text-based interviews** to keep the system manageable and reliable.

---

## 📅 Development Roadmap

### Phase 1 — Project Setup

* Next.js setup
* FastAPI setup
* SQLite database
* Basic UI
* API structure

### Phase 2 — Interview System

* Interview configuration
* Interview state
* Timer
* Question display
* Answer submission

### Phase 3 — AI Integration

* Question generation
* Answer evaluation
* Structured JSON responses
* Follow-up questions

### Phase 4 — Adaptive Interview

* Difficulty adaptation
* Remaining-time awareness
* Question-type selection
* Contextual follow-ups

### Phase 5 — Analytics

* Final report
* Interview history
* Score progression
* Time analysis
* Weakness tracking

### Phase 6 — Polish

* UI improvements
* Error handling
* Loading states
* Testing
* Deployment
* Documentation

---

## 📁 Project Structure

Suggested project structure:

```text
preppilot/
│
├── frontend/
│   ├── app/
│   ├── components/
│   ├── lib/
│   ├── hooks/
│   └── public/
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── interview_engine/
│   │   └── main.py
│   │
│   └── requirements.txt
│
├── README.md
└── .gitignore
```

---

## ⚙️ Getting Started

### Prerequisites

Make sure you have installed:

* Node.js
* Python 3.10+
* Git

### Clone the Repository

```bash
git clone https://github.com/your-username/preppilot.git
cd preppilot
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

The frontend will run locally using the Next.js development server.

### Backend

```bash
cd backend

python -m venv venv
```

Activate the virtual environment.

**Windows:**

```bash
venv\Scripts\activate
```

**Linux/macOS:**

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start FastAPI:

```bash
uvicorn app.main:app --reload
```

---

## 🔐 Environment Variables

Create a `.env` file in the backend:

```env
LLM_API_KEY=your_api_key
DATABASE_URL=sqlite:///./preppilot.db
```

> ⚠️ Never commit your API keys or `.env` files to GitHub.

---

## 🎓 Academic / Project Motivation

PrepPilot is designed as a practical application of **Generative AI, adaptive systems, web development, and software engineering**.

Instead of using an LLM only for text generation, the system combines it with deterministic application logic for:

* Interview state management
* Time management
* Difficulty adaptation
* Performance evaluation
* Historical analytics
* Weakness detection

This creates a complete AI-powered interview simulation platform that provides candidates with a structured environment for realistic interview practice.

---

## 📌 Project Description

**PrepPilot — Adaptive AI Interview Simulator**

*Next.js, TypeScript, FastAPI, Python, LLM API, SQLite*

> A time-constrained AI interview platform that dynamically generates and adapts technical and behavioral questions based on candidate responses, performance, and remaining interview time. PrepPilot provides multi-dimensional answer evaluation, adaptive difficulty, contextual follow-up questions, interview analytics, and recurring weakness tracking across sessions.

---

## 👩‍💻 Developers

### Jannatul Ferdous Tajree

Software Engineering Student
Shahjalal University of Science and Technology

### Nishat Tasnim Nishu

Software Engineering Student
Shahjalal University of Science and Technology

---

## ⭐ Contributing

Contributions, suggestions, and improvements are welcome!

If you would like to contribute:

1. Fork the repository
2. Create a new branch
3. Make your changes
4. Commit your changes
5. Push the branch
6. Open a Pull Request

---

## ⭐ Support

If you find **PrepPilot** useful or interesting, consider giving the repository a ⭐ on GitHub!

---

<p align="center">
  Made with ❤️ by <strong>Jannatul Ferdous Tajree</strong> & <strong>Nishat Tasnim Nishu</strong>
</p>
