# 🎯 InterviewEdge — Smart Interview Preparation Portal

> An end-to-end interview-prep and recruitment ecosystem where candidates practice, coders code, and recruiters recruit — all under one roof, with a proctor quietly watching in the background.

[![Java](https://img.shields.io/badge/Java-Servlets%20%2F%20JSP-orange)]()
[![MySQL](https://img.shields.io/badge/Database-MySQL-blue)]()
[![Judge0](https://img.shields.io/badge/Code%20Execution-Judge0%20API-green)]()
[![Status](https://img.shields.io/badge/Status-Academic%20Project-lightgrey)]()

---

## 🧠 The Idea

Job seekers juggle five different tools to prepare for one interview — a quiz site here, a coding judge there, a mock-interview forum somewhere else. Meanwhile, recruiters running campus drives or small hiring rounds often can't afford enterprise platforms like HackerRank or AMCAT.

**InterviewEdge puts both sides of the table in one system**: a practice-and-prep space for candidates, and a lightweight, proctored assessment engine for recruiters — built entirely with core Java (Servlets/JSP) and MySQL, no heavy frameworks required.

---

## 👥 Three Roles, One Platform

| Role | What they do |
|---|---|
| 🧑‍💻 **Candidate** | Practice topic-wise MCQs, solve coding problems with a live compiler, attempt recruiter-created exams, track topic-wise accuracy, and browse/share real interview experiences |
| 🏢 **Recruiter** | Create custom exams, manage candidate pipelines, review proctoring snapshots, and leave feedback/ratings on attempts |
| 🛠️ **Admin** | Approve recruiters & candidates, curate the question bank, and keep the platform running |

---

## ✨ Feature Highlights

- **⚡ Live Code Execution** — Candidates write and run code directly in the browser via the **Judge0 API**, no local IDE needed.
- **📝 Configurable Question Engine** — A template-driven generator creates MCQs by industry, language, topic, and difficulty, with an `AppConfig` switch designed to plug in a real LLM later without touching the rest of the codebase.
- **👁️ Exam Proctoring** — Webcam snapshots are captured at intervals during an attempt, and tab-switching is detected and flagged in real time, with auto-submit after repeated violations.
- **📊 Performance Analytics** — Every candidate gets topic-wise accuracy tracking, so "where am I weak?" has an actual answer.
- **🗣️ Interview Experience Board** — A Glassdoor-style space where candidates share what a company's interview actually looked like.
- **🔐 Role-Based Access** — Three completely separate dashboards and permission sets for Admin, Recruiter, and Candidate.

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java (Servlets, JSP) |
| Database | MySQL (JDBC) |
| Code Execution | Judge0 CE API (RapidAPI) |
| Frontend | HTML, CSS, Bootstrap, JavaScript |
| Data Interchange | Gson, org.json |
| Build/Deploy | WAR packaging (Apache Tomcat) |

---

## 🗂️ Architecture at a Glance

```
Controller (Servlets)  →  DAO (JDBC)  →  MySQL
        ↓
     JSP Views  →  Role-based dashboards (Admin / Recruiter / Candidate)
```

- **39 Servlet controllers** handling everything from login to exam submission
- **12 DAO classes** for clean separation between business logic and SQL
- **14 JavaBeans** modeling candidates, exams, questions, submissions, and more
- **19 relational tables** — including dedicated tables for proctoring data, coding submissions, and performance history
- **35 JSP pages** split cleanly across three role-based folders

---

## 🗄️ Database Snapshot

Some of the more interesting tables in the schema:

```sql
exam_attempts        -- tracks score, tab-switch count, suspicious_flag, timestamps
exam_snapshots        -- stores webcam captures as BLOBs, linked to an attempt
coding_submissions     -- candidate code + Judge0 output, per question
candidate_performance   -- topic-wise accuracy, auto-updated on every attempt
recruiter_feedback     -- rating + notes, tied to a specific exam attempt
```

---

## 🚀 Getting Started

1. **Clone the repo**
   ```bash
   git clone <repo-url>
   ```
2. **Set up MySQL**
   - Create the `interviewedge` database
   - Import the schema from `/database/interviewedge.sql`
3. **Configure the connection**
   - Update credentials in `com.connection.DBConnection`
4. **Add your Judge0 API key**
   - Set your RapidAPI key in `com.service.Judge0Service` (⚠️ never commit a real key — use an environment variable or config file excluded from version control)
5. **Deploy**
   - Drop the WAR into Apache Tomcat's `webapps/` folder and start the server

---

## 📌 Project Status & Honest Notes

This was built as a final-year academic project, and a few things are worth being upfront about:

- The question generator is currently **rule-based/template-driven**, not a live LLM call — the `AppConfig.USE_REAL_AI` flag exists specifically so a real AI service can be swapped in later.
- Proctoring currently covers **tab-switch detection and webcam snapshots**; fullscreen-exit and copy-paste detection have schema support (`fullscreen_exit_count`, `copy_attempt_count` columns) but aren't wired up on the frontend yet — planned as a next step.

---

## 🧾 Recognition

A research paper based on this project received **Government Copyright Registration** from the Copyright Office, Government of India (Certificate No. LD-20260190541, 2026).

---

## 👩‍💻 Team

Built by a 4-member team as a final-year Computer Engineering project — Department of Computer Engineering, RTC Pune.

---

## 📄 License

Academic project — for educational and portfolio purposes.
