# 🏛️ MCA eConsultation - Sentiment Analysis Web Application

A full-stack Django web application built for the **Ministry of Corporate Affairs (MCA)** e-Consultation Portal. This system processes public and stakeholder feedback on draft policy consultations, leveraging Machine Learning to run automated sentiment analysis, output detailed analytical charts, and generate interactive key summaries and word clouds for decision-makers.

---

## 🔗 Related Project Repositories

This web application serves as the **frontend & application layer** for the sentiment analysis system. The machine learning model training, algorithm benchmarks, accuracy evaluation, and dataset preprocessing notebooks are maintained in a separate dedicated repository:

* **ML Model Training & Research Repository:** [MCA eConsultation ML Engine](https://github.com/your-username/mca-econsultation-ml) *(Replace with your ML repo link)*

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Application Architecture](#-application-architecture)
- [Prediction & Analytics Workflow](#-prediction--analytics-workflow)
- [Tech Stack & Visualization Tools](#-tech-stack--visualization-tools)
- [Project Structure](#-project-structure)
- [Model Integration](#-model-integration)
- [Installation & Setup](#-installation--setup)
- [Application Screenshots](#-application-screenshots)
- [Future Improvements](#-future-improvements)

---

## 💡 Overview

Government e-consultation platforms receive large volumes of unstructured public feedback on proposed legislative policies and regulations. Manually reading and classifying every submission is slow and resource-intensive. 

This platform automates stakeholder feedback processing by providing:
1. **Public-Facing Portal:** Allows stakeholders to read draft consultation papers and submit their feedback online.
2. **Internal Admin Portal:** Enables ministry officials to create consultation papers, view feedback metrics, run ML-based sentiment analysis, view word clouds, and analyze stakeholder sentiment distributions through interactive charts.

---

## ✨ Key Features

* **Public Consultation View:** Interface for public users to browse active policy consultation papers.
* **Internal Admin Authentication:** Secure, role-based login system for authorized ministry personnel.
* **Consultation Management:** Create, publish, view, and delete policy consultation papers.
* **Automated Sentiment Classification:** Classifies public comments into **Positive**, **Neutral**, or **Negative** categories using integrated NLP models.
* **Interactive Data Visualizations:** Real-time donut distribution charts, frequency bar charts, and word clouds.
* **Ad-Hoc Sentiment Testing:** Built-in module for testing raw custom text against the sentiment engine on demand.

---

## 🏗️ Application Architecture

```
                       ┌────────────────────────────────┐
                       │   Public Stakeholder Portal   │
                       └───────────────┬────────────────┘
                                       │ Submits Feedback
                                       ▼
 ┌─────────────────────────────────────────────────────────────────────────────┐
 │                           Django Application                                │
 │                                                                             │
 │  ┌────────────────────────┐                   ┌──────────────────────────┐  │
 │  │      User Panel        │                   │       Admin Panel        │  │
 │  │ (Public Consultations) │                   │  (Management & Analytics)│  │
 │  └───────────┬────────────┘                   └────────────┬─────────────┘  │
 └──────────────│─────────────────────────────────────────────│────────────────┘
                │                                             │
                ▼                                             ▼
       ┌─────────────────┐                           ┌──────────────────┐
       │ SQLite Database │                           │  ML Inference Engine │
       │ (Consultations &│ ◄─────────────────────────┤  (`ml_model.py`) │
       │    Feedback)    │   Classified Sentiments   └─────────┬────────┘
       └─────────────────┘                                     │
                                                               ▼
                                                     ┌──────────────────┐
                                                     │ Visualization &  │
                                                     │  Summary Reports │
                                                     └──────────────────┘
```

---

## 🔄 Prediction & Analytics Workflow

1. **Submission:** A stakeholder submits text feedback on an open policy consultation via the public portal.
2. **Pre-processing:** Cleaned text data is extracted from the database and formatted for model evaluation.
3. **Inference:** The text is passed into `ml_model.py`, which loads pre-trained model artifacts (vectorizer & classifier) to predict sentiment scores.
4. **Aggregation:** Sentiments are recorded back to the database, updating aggregate counters (Positive, Neutral, Negative).
5. **Visualization Rendering:** Chart libraries and word cloud engines synthesize the classification metadata into dynamic dashboard metrics and visual frequency distributions.

---

## 🛠️ Tech Stack & Visualization Tools

* **Backend Framework:** Django 6.0 (Python 3.13)
* **Frontend UI:** HTML5, CSS3, JavaScript, Bootstrap 5
* **Database:** SQLite3
* **Machine Learning & Data Processing:**
  * `scikit-learn` (Classification Algorithms)
  * `nltk` / `spacy` (Text Preprocessing & NLP)
  * `pandas` & `numpy` (Data Processing)
  * `wordcloud` & `matplotlib` (Word Cloud Generation)
* **Visualizations:** Chart.js (Donut Distribution & Frequency Bar Charts)
* **Environment & Security:** `python-decouple` (Environment Variables)

---

## 📁 Project Structure

```text
sentiment_analysis/
│
├── __pycache__/
│   └── ml_model.cpython-313.pyc
│
├── admin_panel/               # Admin Portal App
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
│   ├── urls.py
│   └── views.py
│
├── ml_model/                  # Directory storing trained model weights/vectorizers
│
├── sentiment_analysis/        # Root Project Configuration
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── templates/                 # Global Base Layout Templates
│   ├── base.html
│   └── base2.html
│
├── user_panel/                # Public User App
│   ├── static/                # Static assets (images, CSS, JS)
│   ├── templates/
│   ├── admin.py
│   ├── models.py
│   ├── urls.py
│   └── views.py
│
├── db.sqlite3                 # Local Database
├── manage.py                  # Django Management Script
├── ml_model.py                # Model Loading & Inference Script
├── requirements.txt           # Project Dependencies
├── .env                       # Local Environment File
└── .gitignore
```

---

## 🤖 Model Integration

The ML pipeline is integrated directly into Django through `ml_model.py`. 

```python
# Example interface overview in ml_model.py
import joblib

# Load pre-trained models and vectorizer
VECTORIZER_PATH = 'ml_model/tfidf_vectorizer.pkl'
MODEL_PATH = 'ml_model/sentiment_classifier.pkl'

vectorizer = joblib.load(VECTORIZER_PATH)
model = joblib.load(MODEL_PATH)

def predict_sentiment(text: str) -> str:
    """Processes input text and returns predicted sentiment class."""
    cleaned_text = preprocess_text(text)
    vectorized_text = vectorizer.transform([cleaned_text])
    prediction = model.predict(vectorized_text)[0]
    return prediction
```

---

## ⚙️ Installation & Setup

### Prerequisites
* Python 3.10+
* Virtual Environment tool (`venv`)

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/mca-econsultation-web.git
cd mca-econsultation-web/sentiment_analysis
```

### 2. Set Up Virtual Environment
```bash
# Windows
python -m venv venv
.\venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables
Create a `.env` file in the root `sentiment_analysis/` folder:
```env
SECRET_KEY=your-django-secret-key
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost
```

### 5. Apply Migrations & Create Superuser
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

### 6. Run the Server
```bash
python manage.py runserver
```

Open `http://127.0.0.1:8000/` in your browser to access the portal.

---

## 💻 Application Screenshots

| Public Consultation Portal | Authorised Admin Login |
| :---: | :---: |
| *(Public user view for reading papers & feedback)* | *(Secure login for ministry officers)* |

| Consultation Management | Analytics Dashboard |
| :---: | :---: |
| *(Create & publish new policy documents)* | *(Real-time sentiment breakdown & word clouds)* |

| Sentiment Visualizations |
| :---: |
| *(Donut distribution & frequency bar charts)* |

---

## 🚀 Future Improvements

* **Multilingual Support:** Extend sentiment prediction to support local Indian languages (Hindi, Bengali, Tamil, etc.).
* **Aspect-Based Sentiment Analysis (ABSA):** Pinpoint exact policy clauses receiving negative feedback.
* **PDF Analysis Engine:** Automatically extract stakeholder feedback submitted as attached PDF letters/documents.
* **REST API Export:** Provide secure endpoints for exporting sentiment metrics to external government dashboard portals.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
