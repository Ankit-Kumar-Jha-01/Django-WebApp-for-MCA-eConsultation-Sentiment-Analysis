# 🏛️ MCA eConsultation - Sentiment Analysis Web Application

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Django-6.0-092E20?style=for-the-badge&logo=django&logoColor=white" alt="Django">
  <img src="https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white" alt="Bootstrap">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chart.js&logoColor=white" alt="Chart.js">
  <img src="https://img.shields.io/badge/Status-Active_Development-brightgreen?style=for-the-badge" alt="Status">
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License">
</p>

---

> 🎯 **Goal:** An AI-powered decision support platform built for the **Ministry of Corporate Affairs (MCA)** e-Consultation Portal. It automates the classification of public feedback on draft policies into actionable sentiment analytics, real-time distribution charts, and word clouds.

---

## 🔗 Related Project Repositories

> 💡 **Repository Architecture:** This web app serves as the **application & dashboard layer**. Model research, feature extraction, dataset prep, and algorithm benchmarks are hosted in a dedicated ML repository.

* 🧠 **Machine Learning Engine Repository:** [MCA eConsultation ML Engine](https://github.com/your-username/mca-econsultation-ml) *(Replace with your actual ML repo link)*

---

## 📋 Table of Contents

* [💡 Overview](#-overview)
* [✨ Key Features](#-key-features)
* [🏗️ Application Architecture](#️-application-architecture)
* [🔄 Prediction & Analytics Workflow](#-prediction--analytics-workflow)
* [🛠️ Tech Stack & Visualizations](#️-tech-stack--visualizations)
* [📁 Project Structure](#-project-structure)
* [🤖 Model Integration](#-model-integration)
* [⚙️ Installation & Setup](#️-installation--setup)
* [📱 Application Screenshots](#-application-screenshots)
* [🚀 Future Improvements](#-future-improvements)

---

## 💡 Overview

Government e-consultation platforms process high volumes of unstructured feedback on proposed legislative policies. Reading and categorizing every submission manually creates operational bottlenecks.

This platform streamlines stakeholder feedback processing:

* 🌐 **Public-Facing Portal:** Stakeholders can easily browse draft consultation documents and submit feedback.
* 🛡️ **Internal Officers Portal:** Ministry officials manage consultations, monitor automated sentiment metrics, inspect key summaries, and view word cloud distributions.

---

## ✨ Key Features

| Feature | Description | Target User |
| :--- | :--- | :--- |
| 📑 **Consultation Portal** | View draft policies, reference numbers, and submission deadlines. | Public Stakeholders |
| 🔐 **Role-Based Auth** | Secure login portal designed for ministry officials. | Authorized Personnel |
| 📝 **Paper Management** | Publish, track status (`OPEN` / `CLOSED`), and delete consultation papers. | Ministry Admins |
| 🤖 **Automated Sentiment** | Classifies incoming feedback into **Positive**, **Neutral**, or **Negative**. | Internal System |
| 📊 **Analytics Dashboard** | Live donut charts, frequency distributions, and feedback lists. | Policy Analysts |
| ☁️ **Word Cloud Engine** | Highlights dominant keywords and emerging policy concerns visually. | Decision Makers |

---

## 🏗️ Application Architecture

```text
                        ┌─────────────────────────────────┐
                        │    Public Stakeholder Portal    │
                        └────────────────┬────────────────┘
                                         │ Submits Feedback
                                         ▼
 ┌──────────────────────────────────────────────────────────────────────────────┐
 │                            Django Web Application                            │
 │                                                                              │
 │  ┌──────────────────────────┐                   ┌─────────────────────────┐  │
 │  │        User Panel        │                   │       Admin Panel       │  │
 │  │  (Public Consultations)  │                   │ (Management & Analytics)│  │
 │  └────────────┬─────────────┘                   └────────────┬────────────┘  │
 └───────────────│──────────────────────────────────────────────│───────────────┘
                 │                                              │
                 ▼                                              ▼
        ┌──────────────────┐                          ┌───────────────────┐
        │  SQLite Database │                          │ ML Inference Engine│
        │ (Consultations & │ ◄────────────────────────┤  (`ml_model.py`)  │
        │    Feedback)     │   Classified Sentiments  └─────────┬─────────┘
        └──────────────────┘                                    │
                                                                ▼
                                                      ┌───────────────────┐
                                                      │  Chart.js / Word  │
                                                      │  Cloud Engine     │
                                                      └───────────────────┘
```

---

## 🔄 Prediction & Analytics Workflow

```text
 📥 1. Feedback Submission
    └─ Stakeholder submits raw feedback on a policy via the user portal.

 🧹 2. Preprocessing
    └─ Text cleaned and normalized in `ml_model.py`.

 🔮 3. Sentiment Classification
    └─ Pre-trained vectorizer & ML classifier assign Positive / Neutral / Negative class.

 💾 4. Database Persistence
    └─ Predictions saved into `db.sqlite3` with relation to specific Consultation ID.

 📈 5. Visual Rendering
    └─ Chart.js renders donut & bar graphs; WordCloud engine renders visual topic maps.
```

---

## 🛠️ Tech Stack & Visualizations

### 💻 Backend & Frontend Frameworks
* ![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white) **Django 6.0 (Python 3.13)** - Web framework & database ORM
* ![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white) **Bootstrap 5** - Responsive UI & government-style portal layouts
* ![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white) **SQLite3** - Relational database storage

### 🧠 Machine Learning & Data Processing
* ![scikit-learn](https://img.shields.io/badge/scikit_learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) **Scikit-Learn** - Model classification pipeline
* ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white) **Pandas & NumPy** - Data transformation
* ![NLTK](https://img.shields.io/badge/NLTK-3776AB?style=flat-square&logo=python&logoColor=white) **NLTK / SpaCy** - Text pre-processing & tokenization

### 📊 Visualizations
* ![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chart.js&logoColor=white) **Chart.js** - Interactive Donut & Frequency Bar Charts
* ☁️ **WordCloud & Matplotlib** - Feedback word cloud generation

---

## 📁 Project Structure

```text
sentiment_analysis/
│
├── ⚙️ sentiment_analysis/     # Core Project Settings
│   ├── settings.py            # Static, Database & App Configs
│   ├── urls.py                # Global URL Routing
│   └── wsgi.py
│
├── 🛡️️ admin_panel/            # Internal Portal Application
│   ├── templates/             # Dashboard, Charts & Consultation Views
│   │   ├── analysis.html
│   │   ├── dashboard.html
│   │   ├── login.html
│   │   ├── manage_consultations.html
│   │   ├── sentiment_analysis.html
│   │   └── word_cloud.html
│   ├── views.py               # Analytics & Portal Logic
│   └── urls.py
│
├── 🌐 user_panel/             # Public Consultation Application
│   ├── static/                # Images, CSS, & JS Assets
│   ├── templates/
│   └── views.py
│
├── 🤖 ml_model/               # Model Artifacts Directory (.pkl)
├── 📄 ml_model.py             # Inference Script & Model Loader
├── 📑 templates/              # Global Base Layouts (base.html)
├── 🗄️ db.sqlite3               # SQLite Database
├── 🚀 manage.py               # Django CLI Tool
├── 📋 requirements.txt        # Python Dependencies
└── 🔑 .env                    # Environment Variables
```

---

## 🤖 Model Integration

The ML pipeline connects to Django views via `ml_model.py`:

```python
import joblib
from pathlib import Path

# Paths to trained model artifacts
BASE_DIR = Path(__file__).resolve().parent
VECTORIZER_PATH = BASE_DIR / 'ml_model' / 'tfidf_vectorizer.pkl'
MODEL_PATH = BASE_DIR / 'ml_model' / 'sentiment_classifier.pkl'

# Load model pipeline
vectorizer = joblib.load(VECTORIZER_PATH)
model = joblib.load(MODEL_PATH)

def predict_sentiment(text_comment: str) -> str:
    """Cleans input text, vectorizes, and predicts sentiment category."""
    processed_text = preprocess_text(text_comment)
    vectorized_text = vectorizer.transform([processed_text])
    prediction = model.predict(vectorized_text)[0]
    return prediction
```

---

## ⚙️ Installation & Setup

### 1️⃣ Prerequisites
* **Python 3.10+**
* **Git**

### 2️⃣ Clone Repository & Setup Virtual Environment
```bash
# Clone repository
git clone https://github.com/your-username/mca-econsultation-web.git
cd mca-econsultation-web/sentiment_analysis

# Create & activate virtual environment
python -m venv venv

# Windows
.\venv\Scripts\activate

# Linux/macOS
source venv/bin/activate
```

### 3️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 4️⃣ Configure `.env` File
Create a `.env` file in the root `sentiment_analysis/` directory:
```env
SECRET_KEY=your-django-secret-key
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost
```

### 5️⃣ Run Migrations & Start Server
```bash
# Apply database migrations
python manage.py makemigrations
python manage.py migrate

# Create admin credentials
python manage.py createsuperuser

# Launch server
python manage.py runserver
```

> 🌐 Visit `http://127.0.0.1:8000/` in your browser to view the portal!

---

## 📱 Application Screenshots

| 🌐 Public Consultation Portal | 🔐 Authorised Internal Login |
| :---: | :---: |
| *(Public view for reading policies & submitting feedback)* | *(Secure login for ministry officers)* |

| 📝 Consultation Paper Management | 📊 Analytics Dashboard |
| :---: | :---: |
| *(Create & manage consultation drafts)* | *(Real-time feedback counters & word cloud)* |

| 📈 Interactive Sentiment Charts |
| :---: |
| *(Donut distribution & frequency bar charts)* |

---

## 🚀 Future Improvements

- [ ] 🗣️ **Multilingual Support:** Extend NLP pipeline to process regional Indian languages (Hindi, Tamil, Bengali, etc.).
- [ ] 📌 **Aspect-Based Sentiment Analysis (ABSA):** Identify specific policy clauses receiving feedback.
- [ ] 📄 **Automated PDF Parser:** Extract text directly from submitted PDF letter attachments.
- [ ] ⚡ **REST API Integration:** Expose secure analytical metrics to external government monitoring portals.

---

<p align="center">
  <b>Built for Ministry of Corporate Affairs e-Consultation Portal</b>
</p>
