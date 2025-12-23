 🔍 Hybrid Log Classification System

A *production-oriented hybrid log classification framework* that intelligently classifies system and application logs by combining *rule-based*, *machine learning*, and *LLM-based* approaches.

This system is designed to handle logs ranging from *simple and predictable* to *highly complex, rare, or unseen*, ensuring *high accuracy, robustness, and scalability* in real-world environments.

---

✨ Key Features

 ✅ Multi-layer *hybrid classification pipeline*
 ✅ Handles *structured, semi-structured, and unstructured logs*
 ✅ LLM fallback for *unknown or rare log patterns*
 ✅ FastAPI-based REST API
 ✅ Modular, extensible architecture
 ✅ Recruiter & production friendly design

---

 🧠 System Overview

The project implements a *three-layer decision pipeline*:

1. *Regex-Based Classification*

   * Fast and deterministic
   * Best for recurring and predictable log formats

2. *Sentence Transformer + Logistic Regression*

   * Uses semantic embeddings
   * Handles moderately complex logs
   * Requires labeled training data

3. *LLM-Based Classification (Fallback)*

   * Activated when confidence is low or no pattern matches
   * Handles rare, unseen, or inconsistent logs
   * Ensures maximum coverage

---

 🏗 Architecture

```text
Input Log Message
        |
        v
Regex-Based Classification
        |──► High confidence → Final Label
        |
        v
Sentence Transformer + Logistic Regression
        |──► High confidence → Final Label
        |
        v
LLM Classifier (Fallback)
        |
        v
Final Predicted Label
```

---

 ⚙️ Classification Flow Logic

* Regex match found → *Regex result returned*
* No regex match → *Transformer model invoked*
* Low confidence / insufficient data → *LLM fallback*
* Final label returned with *maximum confidence available*

This layered approach minimizes misclassification while maintaining speed.

---

📁 Project Structure

```text
logs-classification-system/
├── training/
│   ├── train_model.py
│   └── sentence_transformer/
├── models/
│   ├── log_classifier.joblib
│   └── regex_classifier.py
├── utils/
│   ├── preprocessing.py
│   └── confidence.py
├── resources/
│   └── sample_logs.csv
├── server.py
├── requirements.txt
├── .env.example
└── README.md
```

---

🚀 Setup Instructions

1️⃣ Clone the Repository

```bash
git clone https://github.com/Umeshpanchal187/Logs-classification-system.git
cd Logs-classification-system
```

---

2️⃣ Create Virtual Environment

```bash
python -m venv venv
venv\Scripts\activate   # Windows
```

---

3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

---

4️⃣ Configure Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_api_key_here
```
---
5️⃣ Run the API Server

```bash
uvicorn server:app --reload
```

Server will start at:

```
http://127.0.0.1:8000
```

---

📡 API Usage

🔹 Endpoint

```http
POST /classify
```

---

🔹 Request Body

```json
{
  "log_message": "Connection timeout after 30 seconds"
}
```

---

🔹 Response

```json
{
  "predicted_label": "Network Error"
}
```

---

🔹 Interactive API Docs

* Swagger UI:

  ```
  http://127.0.0.1:8000/docs
  ```

---

🧪 Example Log Inputs

| Log Message                    | Predicted Label   |
| ------------------------------ | ----------------- |
| `User login successful`        | Authentication    |
| `Connection timeout after 30s` | Network Error     |
| `Disk space below threshold`   | Resource Warning  |
| `Unexpected token at line 24`  | Application Error |

---

🧠 How the Hybrid Model Decides

* *Regex Layer* → Known patterns, high precision
* *ML Layer* → Semantic similarity via embeddings
* *LLM Layer* → Reasoning for unknown patterns

This ensures:

 🔹 Maximum coverage
 🔹 Minimal false negatives
 🔹 Real-world robustness

---

🛠 Tech Stack

* *Python*
* *FastAPI*
* *Sentence Transformers*
* *Scikit-learn*
* *Regex*
* *Groq LLM API*
* *Uvicorn*
* *Joblib*

---

🔮 Future Enhancements

 🔹 Confidence scoring & thresholds
 🔹 GPU-based transformer inference
 🔹 Automatic feedback loop for retraining
 🔹 Support for additional log formats
 🔹 Streaming log ingestion (Kafka / Flink)

---

👨‍💻 Author

Umesh Panchal
B.Tech AIML | AI & Data Science Enthusiast

GitHub: [https://github.com/Umeshpanchal187](https://github.com/Umeshpanchal187)



