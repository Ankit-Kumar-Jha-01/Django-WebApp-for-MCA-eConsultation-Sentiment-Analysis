# 💬 MCA eConsultation — Sentiment Analysis Web Application

A Django-based web application that integrates a fine-tuned **DistilBERT sentiment analysis model** to classify MCA eConsultation comments as **Positive, Neutral, or Negative**.

This repository focuses on the **application and deployment side** of the project, including the Django backend, frontend interface, model integration, prediction workflow, and web application configuration.

> **ML Model:** The sentiment classification model was trained separately and integrated into this Django application for inference.

---

## 🔗 Related Repository

### 🧠 NLP Model & Training Pipeline

The complete dataset preparation, preprocessing, augmentation, model training, evaluation, and visualization pipeline is available here:

**[NLP-model-for-MCA-eConsultation-Sentiment-Analysis](https://github.com/Ankit-Kumar-Jha-01/NLP-model-for-MCA-eConsultation-Sentiment-Analysis)**

---

## 📌 Overview

The application provides a web interface where users can enter an MCA eConsultation comment and receive a predicted sentiment.

### Supported Sentiments

* 🟢 **Positive**
* ⚪ **Neutral**
* 🔴 **Negative**

The trained DistilBERT model is loaded by the Django backend and used to perform sentiment inference on new comments.

---

## ✨ Features

* 💬 Sentiment prediction for MCA eConsultation comments
* 🤖 Fine-tuned DistilBERT model integration
* 🌐 Django-based backend
* 🖥️ Web-based frontend
* ⚡ Real-time prediction
* 🔄 Reusable model inference pipeline
* 📊 Sentiment result visualization
* 📱 Responsive user interface

---

## 🏗️ Application Architecture

```text
                    User
                     │
                     ▼
              Django Frontend
                     │
                     ▼
              Django Backend
                     │
                     ▼
             Text Preprocessing
                     │
                     ▼
          DistilBERT Tokenizer
                     │
                     ▼
           Fine-tuned DistilBERT
                     │
                     ▼
             Sentiment Prediction
                     │
                     ▼
          Positive / Neutral / Negative
                     │
                     ▼
                 Web UI
```

---

## 🔄 Prediction Workflow

```text
User enters comment
        ↓
Django receives the input
        ↓
Input is preprocessed
        ↓
Tokenizer converts text into model inputs
        ↓
Fine-tuned DistilBERT performs inference
        ↓
Prediction probabilities are generated
        ↓
Highest-probability sentiment is selected
        ↓
Result is displayed on the webpage
```

---

## 🛠️ Technologies Used

| Category             | Technology                |
| -------------------- | ------------------------- |
| Backend              | Django                    |
| Programming Language | Python                    |
| NLP Model            | DistilBERT                |
| Deep Learning        | PyTorch                   |
| NLP Framework        | Hugging Face Transformers |
| Frontend             | HTML, CSS, JavaScript     |
| Template Engine      | Django Templates          |
| Version Control      | Git & GitHub              |

---

## 📂 Project Structure

```text
MCA-eConsultation-Sentiment-Analysis-Django/
│
├── manage.py
│
├── project/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── mainApp/
│   ├── views.py
│   ├── urls.py
│   ├── models.py
│   └── ...
│
├── templates/
│   └── ...
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── ml_model/
│   └── ...
│
├── requirements.txt
└── README.md
```

> The exact structure may vary depending on the current implementation.

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/Ankit-Kumar-Jha-01/MCA-eConsultation-Sentiment-Analysis-Django.git
cd MCA-eConsultation-Sentiment-Analysis-Django
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it:

**Windows**

```bash
venv\Scripts\activate
```

**Linux / macOS**

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Apply migrations

```bash
python manage.py migrate
```

### 5. Start the development server

```bash
python manage.py runserver
```

Open the application at:

```text
http://127.0.0.1:8000/
```

---

## 🤖 Model Integration

The application uses the fine-tuned **DistilBERT** model developed in the companion ML repository.

The model performs **three-class sentiment classification**:

```text
0 → Negative
1 → Neutral
2 → Positive
```

The Django application handles:

1. Loading the trained model and tokenizer
2. Receiving user input
3. Preprocessing the comment
4. Tokenizing the input
5. Running model inference
6. Converting model output into a sentiment label
7. Displaying the prediction to the user

---

## 📊 Model Information

| Parameter               | Value                            |
| ----------------------- | -------------------------------- |
| Base Model              | `distilbert-base-uncased`        |
| Task                    | 3-Class Sentiment Classification |
| Classes                 | Positive, Neutral, Negative      |
| Maximum Sequence Length | 90                               |
| Framework               | PyTorch                          |
| Transformers            | Hugging Face                     |

For the complete training methodology and evaluation results, see the **[ML repository](https://github.com/Ankit-Kumar-Jha-01/NLP-model-for-MCA-eConsultation-Sentiment-Analysis)**.

---

## 🖥️ Application

### Input

The user enters an MCA eConsultation comment through the web interface.

### Processing

Django sends the comment through the integrated NLP inference pipeline.

### Output

The application displays the predicted sentiment:

```text
Comment
   ↓
Model
   ↓
Sentiment
```

Example:

```text
Input:
"The proposed amendment will make compliance easier for small businesses."

Prediction:
Positive
```

---

## ⚠️ Important Note

The model was developed and evaluated using a **synthetic dataset created for prototyping**.

The current model achieved very high evaluation scores on this dataset, but these results should **not be interpreted as production-level performance on real-world MCA submissions**.

Real-world comments may contain:

* Ambiguous language
* Sarcasm
* Mixed sentiments
* Hindi or code-mixed text
* Domain-specific terminology
* Unseen writing patterns

Therefore, further validation using genuine, unseen MCA consultation comments would be required before production deployment.

---

## 🚀 Future Improvements

* 🌐 Deploy the application publicly
* 🇮🇳 Support Hindi and code-mixed comments
* 📊 Add sentiment analytics dashboard
* 📈 Display confidence scores
* 📁 Support batch comment analysis
* 🔐 Add authentication and user management
* 🔄 Improve model using real-world data
* 📱 Improve mobile responsiveness
* 🧪 Add automated testing
* ⚡ Optimize inference for production

---

## 🔗 Project Repositories

### 🧠 Model & Training

**NLP-model-for-MCA-eConsultation-Sentiment-Analysis**

Complete NLP pipeline including dataset preparation, preprocessing, augmentation, training, evaluation, and visualization.

### 🌐 Django Application

**MCA-eConsultation-Sentiment-Analysis-Django**

Django web application integrating the trained model for real-time sentiment prediction.

---

## 👨‍💻 Author

**Ankit Kumar Jha**

B.Tech CSE — Data Science

Interested in **Machine Learning, NLP, Data Science, and AI/ML Applications**.

---

## 📄 License

This project is intended for educational and research purposes.
