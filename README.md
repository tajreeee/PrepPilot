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



## 👩‍💻 Developers

### Jannatul Ferdous Tajree

Software Engineering Student
Shahjalal University of Science and Technology

### Nishat Tasnim Nishu

Software Engineering Student
Shahjalal University of Science and Technology

---



## ⭐ Support

If you find **PrepPilot** useful or interesting, consider giving the repository a ⭐ on GitHub!

---

<p align="center">
  Made with ❤️ by <strong>Jannatul Ferdous Tajree</strong> & <strong>Nishat Tasnim Nishu</strong>
</p>
