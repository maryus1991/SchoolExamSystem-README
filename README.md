# School Exam System (Sorna)

> A full-featured online examination platform built with Django 5.2 — designed for schools, academies, and educational institutions in Iran.

![Django](https://img.shields.io/badge/Django-5.2-092E20?style=for-the-badge&logo=django&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-8-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Celery](https://img.shields.io/badge/Celery-5-37814A?style=for-the-badge&logo=celery&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)

---

## ✨ Overview

**School Exam System** (also known as **Sorna**) is a comprehensive online examination and question bank platform. It enables educational institutions to create, manage, and conduct online exams with advanced features tailored for the Iranian education system.

The platform supports multiple user roles (Students, Correctors/Sanatorium, Admins), complex exam configurations, automatic and manual grading, detailed reporting, and paid exam enrollment.

**Live Domains**: [sornac.ir](https://sornac.ir) | [sorna-academy.ir](https://sorna-academy.ir)

---

## 🚀 Key Features

### Question Bank (QBank)
- Multiple question types:
  - Multiple Choice (4 options)
  - True / False
  - Short Answer
  - Long Answer (Essay)
  - Image-based questions
  - PDF-based questions
- Difficulty levels
- Lesson / Topic categorization
- Answer keys with text, image, or PDF solutions
- Suggested solving time per question
- View tracking

### Exams & Quizzes
- **Comprehensive Exams** (multi-subject) and individual **Quizzes**
- Configurable timer and capacity limits
- Start / End / Last-entry time control
- Question order randomization
- Negative scoring support (configurable percentage)
- Allow/disallow going back to previous questions
- Allow/disallow editing answers after submission
- Online / Offline exam modes
- Province & City location support

### User Roles
| Role | Capabilities |
|------|--------------|
| **Student** | Register for exams, take online tests, view results & reports |
| **Sanatorium (Corrector)** | Grade essay/short-answer questions, review answer sheets |
| **Admin** | Full control over questions, exams, users, reports, and settings |

### Grading & Reports
- Automatic grading for multiple-choice questions
- Manual grading workflow for open-ended questions
- Detailed per-student and per-exam reports
- Score calculation with negative marking
- Result publication control

### Payments & Enrollment
- Paid exams with price configuration
- Order management system
- Correction fee per answer sheet

### Content & SEO
- Blog system
- Dynamic site settings
- Sitemaps support

### Technical Features
- Phone-number based authentication + OTP (Kavenegar)
- Jalali (Persian) calendar support
- S3-compatible Object Storage (Arvan / custom)
- Redis caching + django-cachalot
- Celery for background tasks
- HTML minification & static compression
- WebP image optimization
- Docker & Docker Compose ready
- Production-ready security headers (HSTS, Secure Cookies, etc.)

---

## 🛠 Tech Stack

| Layer              | Technology                          |
|--------------------|-------------------------------------|
| Backend            | Django 5.2                          |
| Database           | PostgreSQL 15                       |
| Cache / Broker     | Redis 8 + RabbitMQ                  |
| Task Queue         | Celery                              |
| Authentication     | Custom User (Phone + OTP)           |
| Rich Text          | CKEditor 5                          |
| Image Processing   | Easy Thumbnails (WebP)              |
| Object Storage     | django-storages + boto3 (S3)        |
| Date               | django-jalali-date                  |
| SMS                | Kavenegar                           |
| Frontend Assets    | django-compressor + minify-html     |
| Containerization  | Docker + Docker Compose             |

---

## 📁 Project Structure

```
SchoolExamSystem/
├── admin_panel/          # Super admin panel
├── blog/                 # Blog system
├── config/               # Settings, Celery, URLs, Storage
├── dashboard/            # User dashboard
├── docker/               # Docker files
├── docs/                 # Documentation
├── envs/                 # Environment variables
├── nginx/                # Nginx configuration
├── order/                # Payment & enrollment
├── qbank/                # Question Bank
├── quiz/                 # Exams & Quizzes
├── report/               # Reports & analytics
├── sanatorium/           # Corrector (grader) panel
├── sitesetting/          # Site-wide settings
├── static/               # Static files
├── template/             # Global templates
├── user/                 # Custom user model + auth
├── utils/                # Shared utilities
├── docker-compose.yml
├── production.yml
├── manage.py
├── requirements.txt
└── LICENSE
```

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/maryus1991/SchoolExamSystem.git
cd SchoolExamSystem
```

### 2. Create virtual environment

```bash
python -m venv venv
source venv/bin/activate   # Linux / macOS
# or
venv\Scripts\activate      # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
# For development tools:
pip install -r dev-requirements.txt
```

### 4. Environment variables

Create the file `envs/.envs` with the following variables:

```env
SECRET_KEY=your-very-secret-key
DEBUG=1
ALLOWED_HOSTS=localhost,127.0.0.1

POSTGRES_ENGIN=django.db.backends.postgresql
POSTGRES_DB=schoolexam
POSTGRES_USER=postgres
POSTGRES_PASSWORD=yourpassword
POSTGRES_HOST=localhost
POSTGRES_PORT=5432

# Kavenegar OTP
KAVEH_NEGAR_API_KEY=your-api-key

# Object Storage (S3 compatible)
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_S3_ENDPOINT_URL=...
AWS_STORAGE_BUCKET_NAME=sorna

# Admin panel secret path (production)
admin_panel_url=your-long-random-token
```

### 5. Database setup

```bash
python manage.py migrate
python manage.py createsuperuser
```

### 6. Run the development server

```bash
python manage.py runserver
```

### 7. Celery (recommended)

```bash
celery -A config worker -l info -Q default
```

---

## 🐳 Docker Setup (Recommended)

The project is fully Dockerized.

```bash
# Development
docker-compose up --build

# Production
docker-compose -f production.yml up --build -d
```

Services included:
- `app` (Django)
- `postgres`
- `redis`
- `rabbitmq`
- `celery`

---

## 📌 Important Notes

- The project uses **Asia/Tehran** timezone and full **Jalali date** support.
- In production, the admin panel is protected behind a long random URL token.
- Media files (questions, PDFs, images) can be stored on local disk or S3-compatible object storage.
- Negative scoring and answer editing rules are fully configurable per exam.
- Correctors (Sanatorium) have a dedicated workflow for grading open-ended questions.

---

## 📄 License

This project is released under a **Custom Commercial License**.  
See the [LICENSE](LICENSE) file for full terms.

**Copyright (c) 2026 Mostafa EbrahimZadeh. All Rights Reserved.**

Unauthorized copying, distribution, modification, or commercial use without written permission is strictly prohibited.

---

## 👨‍💻 Author

**maryus**  
GitHub: [maryus1991](https://github.com/maryus1991)

---

**Ready to revolutionize your exams? 🎓📝**
