# **Hybrid Log Classification System**

A powerful **hybrid log classification framework** that combines rule-based, machine-learning, and LLM-based approaches for robust and scalable log analysis.
This system intelligently classifies logs even when patterns vary from simple and predictable to highly complex and poorly structured.

---

## 🚀 **Overview**

This project implements a **three-layer hybrid classification pipeline**, designed to handle all types of log data:

### **1️⃣ Regex-Based Classification**

* Fast and rule-driven
* Best for simple, recurring, and well-structured log formats
* Uses manually-crafted regex patterns

### **2️⃣ Sentence Transformer + Logistic Regression**

* Ideal for moderately complex logs
* Requires labeled training data
* Generates embeddings using a Sentence Transformer model
* Trains a Logistic Regression classifier on embeddings

### **3️⃣ LLM-Based Classification (Fallback Mode)**

* Handles difficult logs where training data is insufficient
* Uses powerful reasoning capabilities from LLMs to infer labels
* Ensures coverage for unknown or rare log patterns

This hybrid design ensures **high accuracy**, **flexibility**, and **real-world robustness**.

---

## 🏗️ **Architecture**

```
┌─────────────────────────────────┐
│            Input Logs           │
└─────────────────────────────────┘
                ↓
┌─────────────────────────────────┐
│     Regex Classification        │──▶ Simple / predictable logs
└─────────────────────────────────┘
                ↓ (if no match)
┌─────────────────────────────────┐
│  Transformer + Logistic Reg     │──▶ Complex logs (training data available)
└─────────────────────────────────┘
                ↓ (if low confidence)
┌─────────────────────────────────┐
│          LLM Classifier         │──▶ Rare / unseen / inconsistent logs
└─────────────────────────────────┘
                ↓
┌─────────────────────────────────┐
│          Final Label            │
└─────────────────────────────────┘
```

---

## 📁 **Folder Structure**

```
project/
│── training/
│     ├── train_model.py
│     ├── regex_classifier.py
│     └── utils.py
│
│── models/
│     ├── sentence_transformer/
│     └── log_classifier.joblib
│
│── resources/
│     ├── test.csv
│     ├── samples/
│     └── output/
│
│── server.py
│── requirements.txt
│── README.md
```

### **training/**

Contains:

* Regex classification rules
* Training pipeline for Transformer + Logistic Regression
* Scripts to generate embeddings and save models

### **models/**

Stores:

* Trained Logistic Regression model
* Saved embedding model
* Feature files

### **resources/**

Includes:

* Test CSVs
* Output samples
* Supporting assets (images, examples, etc.)

### **Root Directory**

Contains:

* **FastAPI server (server.py)**
* Entry point for API-based classification

---

## ⚙️ **Setup Instructions**

### **1. Install Dependencies**

```bash
pip install -r requirements.txt
```

### **2. Start the FastAPI Server**

```bash
uvicorn server:app --reload
```

### **3. API Endpoints**

| URL                                                            | Description                 |
| -------------------------------------------------------------- | --------------------------- |
| **[http://127.0.0.1:8000/](http://127.0.0.1:8000/)**           | Main health/status endpoint |
| **[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)**   | Swagger UI (interactive)    |
| **[http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)** | ReDoc documentation         |

---

## 📤 **Usage**

### **1. Prepare Input CSV**

Your CSV must contain:

| Column        | Description                            |
| ------------- | -------------------------------------- |
| `source`      | Application or service generating logs |
| `log_message` | Raw log string to classify             |

Example:

```
source,log_message
app1,"Connection timeout after 30s"
app2,"User login successful"
```

### **2. Upload CSV to API**

Send the file using:

* Swagger UI
* Postman
* Curl
* Any frontend client

### **3. Receive Output CSV**

The API returns:

* The original CSV
* Plus a new column `target_label` with predicted class for each log

Example output:

```
source,log_message,target_label
app1,"Connection timeout after 30s",Network Error
app2,"User login successful",Authentication
```

---

## 🧠 **How the Hybrid Model Decides**

| Stage                     | When Used                                         | Strength                             |
| ------------------------- | ------------------------------------------------- | ------------------------------------ |
| **Regex**                 | If log matches known patterns                     | Fast + accurate for simple logs      |
| **ML (Transformer + LR)** | When regex fails & model confidence is high       | Learns from dataset, handles variety |
| **LLM**                   | When ML confidence is low or data is insufficient | Best reasoning for unknown patterns  |

This ensures **maximum coverage** and **minimum misclassification**.

---

## 🛠️ **Technologies Used**

* Python
* FastAPI
* Sentence Transformers
* Logistic Regression
* Regex
* Joblib
* Uvicorn
* Pandas

---

## 📌 **Future Enhancements**

* Add confidence scoring and threshold tuning
* Add more regex patterns for new log types
* Add GPU-based transformer inference
* Automatic LLM feedback to improve training dataset

