# 🔐 SecDevOps Vulnerable Backend

> **A deliberately vulnerable Flask API for SecDevOps security testing, penetration practice, and CI/CD pipeline integration**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)

> ⚠️ **WARNING: This application is intentionally insecure. It is designed for security research, DevSecOps pipeline testing, and educational purposes only. DO NOT deploy in production.**

---

## 📌 What This Project Does

This is a **purposely vulnerable e-learning platform backend** built with Flask, designed to simulate a real-world application with common security weaknesses. It is used to:

- Practice **penetration testing** against realistic API vulnerabilities
- Build and test **DevSecOps CI/CD pipelines** with SAST/DAST tools
- Demonstrate **OWASP Top 10** vulnerabilities in a controlled environment
- Train developers to **identify and fix** security flaws

---

## 🧩 System Architecture

```
Client Request
     │
     ▼
Flask REST API (app.py)
     │
     ├── /api/login          → SQL Injection vulnerability
     ├── /api/register       → Plaintext password storage
     ├── /api/courses        → JWT auth (teacher/student roles)
     ├── /api/enroll         → No duplicate enrollment check
     ├── /api/submit-assignment → Insecure file upload
     ├── /api/download       → Path traversal vulnerability
     ├── /api/export-grades  → Command injection vulnerability
     └── /api/grade-submission → Missing auth/IDOR
          │
          ▼
     SQLite Database (learning.db)
     │
     ▼
GitHub Actions CI/CD Pipeline
     (.github/workflows)
```

---

## 🐛 Intentional Vulnerabilities (OWASP Top 10)

| # | Vulnerability | Location | Description |
|---|---|---|---|
| 1 | **SQL Injection** | `/api/login` | Raw string concatenation in SQL query |
| 2 | **Broken Authentication** | All routes | Hardcoded secret key, no token expiry check |
| 3 | **Plaintext Passwords** | `/api/register` | Passwords stored without hashing |
| 4 | **IDOR** | `/api/student-submissions/<id>` | No auth check — any user can access any submission |
| 5 | **Stored XSS** | `Course.description` | No input sanitization on course description |
| 6 | **Insecure File Upload** | `/api/submit-assignment` | No file type validation |
| 7 | **Path Traversal** | `/api/download/<filename>` | No path validation on file download |
| 8 | **Command Injection** | `/api/export-grades` | `os.system()` with unsanitized input |
| 9 | **Broken Access Control** | `/api/grade-submission` | No authentication or authorization check |
| 10 | **Role Manipulation** | `/api/register` | User can self-assign any role |

---

## 📁 Project Structure

```
SecDevops-back/
│
├── .github/
│   └── workflows/           # CI/CD pipeline definitions (GitHub Actions)
│
├── app.py                   # Main Flask application (593 lines, all vulnerabilities here)
├── test_app.py              # Test suite for API endpoints
├── Dockerfile               # Container definition
├── requirements.txt         # Python dependencies
└── .gitignore
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Docker (optional)

### Run Locally

```bash
# Clone the repo
git clone https://github.com/Harikanth2307/SecDevops-back.git
cd SecDevops-back

# Install dependencies
pip install -r requirements.txt

# Run the app
python app.py
```

App runs on: `http://localhost:4000`

### Run with Docker

```bash
# Build the image
docker build -t secdevops-back .

# Run the container
docker run -p 4000:4000 secdevops-back
```

---

## 🔗 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | Health check |
| `POST` | `/api/register` | Register user (student/teacher) |
| `POST` | `/api/login` | Login and receive JWT token |
| `GET` | `/api/courses` | List courses |
| `POST` | `/api/courses` | Create a course (teacher only) |
| `POST` | `/api/enroll` | Enroll in a course (student only) |
| `POST` | `/api/submit-assignment` | Submit assignment file |
| `GET` | `/api/download/<filename>` | Download submitted file |
| `POST` | `/api/grade-submission` | Grade a submission |
| `POST` | `/api/export-grades` | Export grades report |

### Default Test User

```
Username: john.smith
Password: teacher123
Role: teacher
```

---

## ⚙️ CI/CD Pipeline

This project includes a **GitHub Actions workflow** that demonstrates how DevSecOps pipelines can be set up to automatically scan for vulnerabilities on every push — integrating security into the development lifecycle.

---

## 🔧 Tech Stack

| Layer | Technology |
|---|---|
| Backend Framework | Flask (Python) |
| Database | SQLite + SQLAlchemy ORM |
| Authentication | JWT (PyJWT) |
| Containerisation | Docker |
| CI/CD | GitHub Actions |
| Testing | pytest |

---

## 👤 Author

**Hari Kanth Karne** — Cloud Engineer | Cybersecurity | AI | ML

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hari-kanth-karne-741083368)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Harikanth2307)

---

> This project is for **educational and security research purposes only**. Never deploy this in a production environment.
