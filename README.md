# SHL Assessment Recommendation System

A FastAPI-based recommendation system that suggests the most relevant SHL assessments based on a Job Description, Natural Language Query, or Job URL.

---
#deploy link
https://shl-assessment-recommender-o0vz.onrender.com
---
# Features

- SHL Assessment Recommendation Engine
- Semantic Search using Sentence Transformers
- Gemini LLM Re-ranking (Optional)
- SHL Assessment Scraper
- FastAPI REST API
- HTML Frontend
- Supports:
  - Natural Language Queries
  - Job Descriptions
  - Job URLs
- Returns Top 10 Recommended SHL Assessments

---

# Project Structure

```
.
├── api.py
├── recommender.py
├── scraper.py
├── build_embeddings.py
├── frontend.html
├── requirements.txt
├── README.md
├── shl_assessments.json
├── embeddings.npy
├── assessments_index.pkl
├── .env
```

---

# Requirements

Python 3.10+

Install all dependencies:

```bash
pip install -r requirements.txt
```

---

# Environment Variable

Create a `.env` file in the project folder.

Example:

```
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
```

Gemini is optional.

If no API key is provided, the recommender still works using semantic search.

---

# Build Dataset

Run the SHL scraper.

```bash
python scraper.py
```

Output

```
shl_assessments.json
```

---

# Build Embeddings

```bash
python build_embeddings.py
```

Outputs

```
embeddings.npy

assessments_index.pkl
```

---

# Run API

Start the FastAPI server.

```bash
uvicorn api:app --reload
```

Server starts at

```
http://127.0.0.1:8000
```

---

# Open Swagger UI

```
http://127.0.0.1:8000/docs
```

---

# Open Frontend

```
http://127.0.0.1:8000/
```

---

# API Endpoints

## Health Check

```
GET /health
```

Response

```json
{
    "status":"healthy"
}
```

---

## Recommend Assessments

```
POST /recommend
```

Request

```json
{
    "query":"Java Developer with SQL and Python"
}
```

Example Response

```json
{
  "recommended_assessments": [
    {
      "name": "Java 8",
      "url": "https://www.shl.com/solutions/products/product-catalog/view/java-8-new/",
      "description": "SHL Assessment: Java 8",
      "duration": null,
      "remote_support": "Yes",
      "adaptive_support": "No",
      "test_type": []
    }
  ]
}
```

---

# Supported Inputs

The recommender accepts

- Natural Language Queries

Example

```
Java Developer
```

```
Python SQL Analyst
```

```
Marketing Executive
```

```
Java Developer with collaboration skills
```

It also accepts

- Complete Job Descriptions

and

- Job Posting URLs

---

# Recommendation Pipeline

```
User Query
      │
      ▼
FastAPI API
      │
      ▼
SHL Recommender
      │
      ▼
Semantic Search
(Sentence Transformers / TF-IDF)
      │
      ▼
Gemini Re-ranking (Optional)
      │
      ▼
Top 10 SHL Assessments
```

---

# Technologies Used

- Python
- FastAPI
- Sentence Transformers
- Scikit-Learn
- NumPy
- Pandas
- BeautifulSoup
- Requests
- Gemini API
- Uvicorn

---

# Example Query

```
Java Developer
```

Returns

- Java 8
- Core Java Entry Level
- Core Java Advanced Level
- SQL Server
- Python
- Automata SQL
- Verify Interactive Inductive Reasoning
- OPQ Personality Questionnaire
- Verify Numerical Ability
- Verify Verbal Ability

---

# Running the Project

Step 1

```bash
pip install -r requirements.txt
```

Step 2

```bash
python scraper.py
```

Step 3

```bash
python build_embeddings.py
```

Step 4

```bash
uvicorn api:app --reload
```

Step 5

Open

```
http://127.0.0.1:8000/
```

or

```
http://127.0.0.1:8000/docs
```

---

# Deployment

Deploy on Render, Railway, or any platform supporting FastAPI.

Start Command

```bash
uvicorn api:app --host 0.0.0.0 --port $PORT
```

Build Command

```bash
pip install -r requirements.txt
```

Environment Variable

```
GEMINI_API_KEY=YOUR_API_KEY
```

---

# Author

SHL Assessment Recommendation System

Built using FastAPI, Semantic Search, and Gemini AI.
