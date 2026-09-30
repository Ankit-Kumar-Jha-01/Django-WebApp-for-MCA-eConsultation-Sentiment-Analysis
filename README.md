<div align="center">

# 🏛️ MCA eConsultation Sentiment Analysis — Django Web Application

**A Django-based web platform that serves the MCA eConsultation sentiment analysis model live — public comment submission, admin dashboard, and analytics**

![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![DistilBERT](https://img.shields.io/badge/Model-DistilBERT-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

## 🔗 Related Project Repositories

This is the **application/deployment repo** — it serves a model trained in a separate repository. For training code, algorithms, preprocessing pipeline, and evaluation metrics, see:

> 🧠 **ML Training Repo:** [`mca-econsultation-sentiment-analysis-ml`](<link-to-your-ML-repo>) — DistilBERT fine-tuning, leakage-free train/val/test split, augmentation pipeline, and evaluation results

---

## 📑 Table of Contents

1. [Overview](#-overview)
2. [Requirements](#-requirements)
3. [Application Architecture](#-application-architecture)
4. [Features](#-features)
5. [Prediction Workflow](#-prediction-workflow)
6. [Visualization](#-visualization)
7. [Technology Used](#-technology-used)
8. [Project Structure](#-project-structure)
9. [Installation & Setup](#-installation--setup)
10. [Model Integration](#-model-integration)
11. [Application](#-application)
12. [Future Improvements](#-future-improvements)

---

## 🔎 Overview

This Django application brings the MCA eConsultation sentiment analysis model into a usable, live web platform. Citizens/stakeholders can submit comments on proposed rules through a **user panel**, while an **admin panel** lets administrators review submitted consultations, run sentiment analysis, view word clouds, and see summarized analytics — all backed by the DistilBERT model trained in the companion ML repo.

The app is split into two Django apps:
- **`user_panel`** — public-facing comment submission interface
- **`admin_panel`** — authenticated dashboard for managing consultations, running analysis, and viewing reports

---

## ⚙️ Requirements

- Python 3.13
- Django (see `requirements.txt` for pinned version)
- SQLite (bundled — no external DB server needed)
- The trained model artifacts from the ML repo (tokenizer + fine-tuned DistilBERT weights)

All Python dependencies are listed in [`requirements.txt`](./requirements.txt).

---

## 🏗️ Application Architecture

```
                ┌─────────────────┐
                │   User Panel     │  ← public comment submission
                └────────┬─────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   ml_model.py    │  ← loads DistilBERT, runs prediction
                └────────┬─────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   db.sqlite3     │  ← stores comments + predicted sentiment
                └────────┬─────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   Admin Panel    │  ← dashboard, analysis, word cloud, summary
                └─────────────────┘
```

- **`sentiment_analysis/`** (project package) — Django settings, URL routing, WSGI/ASGI entry points
- **`user_panel/`** — models, views, and templates for public-facing comment submission
- **`admin_panel/`** — models, views, and templates for the admin dashboard, analysis tools, and reporting
- **`ml_model.py`** — central module that loads the trained model and exposes a prediction function used by both apps

---

## ✨ Features

- 📝 Public comment submission form (user panel)
- 🔐 Admin login and authenticated dashboard
- 📋 Manage consultations — view and organize submitted comments
- 🤖 Run sentiment analysis on submitted comments (Positive / Negative / Neutral)
- ☁️ Word cloud visualization per sentiment category
- 📊 Summary reports — sentiment distribution and key statistics
- 💾 Persistent storage of comments and predictions via SQLite

---

## 🔄 Prediction Workflow

1. A user submits a comment through the **user panel** form
2. The comment is saved to the database (`user_panel` models)
3. The admin (or an automated trigger) initiates analysis from the **admin panel**
4. `ml_model.py` loads the fine-tuned DistilBERT model and tokenizer, applies the same preprocessing pipeline used in training, and returns a predicted sentiment label
5. The prediction is stored and linked back to the original comment
6. The **admin dashboard** aggregates predictions into sentiment distribution stats, word clouds, and summary reports for review

---

## 📈 Visualization

Rendered in the admin panel (`word_cloud.html`, `summary.html`, `sentiment_analysis.html`):
- ☁️ Word clouds generated per sentiment class from submitted comments
- 📊 Sentiment distribution summary (Positive / Negative / Neutral breakdown)
- 📋 Tabular view of individual comment-level predictions for manual review

*(Add real dashboard screenshots here once available, e.g. `![Dashboard](screenshots/dashboard.png)` — happy to wire these in with real filenames/images.)*

---

## 🧰 Technology Used

| Category | Tools |
|---|---|
| Backend framework | ![Django](https://img.shields.io/badge/Django-092E20?logo=django&logoColor=white) |
| Language | ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) |
| Database | ![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white) |
| ML Model | ![DistilBERT](https://img.shields.io/badge/DistilBERT-blue) via 🤗 Transformers |
| Frontend | Django Templates (HTML) |
| Environment config | `.env` (via `python-decouple` / `django-environ`, or similar) |

---

## 🗂️ Project Structure

```
sentiment_analysis/
│
├── admin_panel/                  # Admin dashboard app
│   ├── migrations/
│   ├── templates/
│   │   ├── analysis.html
│   │   ├── dashboard.html
│   │   ├── login.html
│   │   ├── manage_consultations.html
│   │   ├── sentiment_analysis.html
│   │   ├── summary.html
│   │   └── word_cloud.html
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│
├── ml_model/                     # (model artifacts / tokenizer, loaded by ml_model.py)
│
├── sentiment_analysis/           # Django project package
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── templates/                    # Shared/base templates
│   ├── base.html
│   └── base2.html
│
├── user_panel/                   # Public-facing app
│   ├── migrations/
│   ├── static/
│   ├── templates/
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│
├── db.sqlite3
├── manage.py
├── ml_model.py                   # loads model + runs predictions
├── requirements.txt
├── .env                          # environment variables (not committed)
└── .gitignore
```

---

## 🛠️ Installation & Setup

```bash
# 1. Clone the repository
git clone <your-django-repo-url>
cd sentiment_analysis

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set up environment variables
cp .env.example .env            # then fill in SECRET_KEY, DEBUG, etc.

# 5. Apply database migrations
python manage.py migrate

# 6. Create a superuser (for admin panel access)
python manage.py createsuperuser

# 7. Run the development server
python manage.py runserver
```

Then visit `http://127.0.0.1:8000/` for the user panel, and the admin login page for the dashboard.

---

## 🔌 Model Integration

- The fine-tuned DistilBERT model and tokenizer (trained in the [ML repo](<link-to-your-ML-repo>)) are loaded inside `ml_model.py`, placed in the `ml_model/` directory
- `ml_model.py` exposes a prediction function that:
  1. Applies the **same preprocessing pipeline** used during training (emoji removal, special character stripping, lowercasing) — for consistency between training and inference
  2. Tokenizes the cleaned comment
  3. Runs a forward pass through the model
  4. Returns the predicted sentiment label (Positive / Negative / Neutral)
- Both `user_panel` and `admin_panel` call into this shared module rather than duplicating model-loading logic

> ⚠️ Model weights are not committed to this repo (excluded via `.gitignore`) — download/copy them from the ML repo into `ml_model/` before running locally.

---

## 🖥️ Application

*(Add screenshots of the live application here — login page, dashboard, comment submission form, sentiment analysis view, word cloud, and summary report. Example:)*

```markdown
![Dashboard](screenshots/dashboard.png)
![Word Cloud View](screenshots/word_cloud.png)
![Summary Report](screenshots/summary.png)
```

---

## 🚀 Future Improvements

- 🔄 Replace local model loading with a dedicated inference API/microservice for scalability
- 🗄️ Migrate from SQLite to PostgreSQL for production deployment
- 📈 Add real-time analytics updates instead of on-demand analysis runs
- 🔐 Add role-based access control for multiple admin permission levels
- 🌐 Deploy publicly (e.g. Render, Railway, or AWS) with CI/CD
- 📱 Add a responsive/mobile-friendly UI for the public comment submission form
- 🧪 Add automated tests for prediction consistency between this app and the ML training repo

---

<div align="center">
Django application for the MCA eConsultation Sentiment Analysis project
</div>
