# SHL Assessment Recommendation System – Approach Document

**Candidate:** Abhi Ram

**Assignment:** SHL Research Engineer Intern – Generative AI Assessment

---

# 1. Introduction

The objective of this project is to develop an intelligent recommendation system that suggests the most relevant SHL Individual Test Solutions based on:

- Natural language queries
- Job descriptions
- Job description URLs

The system returns the top recommended SHL assessments using semantic search combined with an optional Large Language Model (LLM) reranking stage.

The solution has been implemented using Python, FastAPI, Sentence Transformers, and BeautifulSoup.

---

# 2. Solution Overview

The recommendation system follows the workflow below.

```
User Query / Job Description / URL
                │
                ▼
        URL Text Extraction
                │
                ▼
     Semantic Embedding Search
                │
                ▼
      Similarity Ranking
                │
                ▼
 Optional Gemini LLM Reranking
                │
                ▼
     Final SHL Recommendations
```

The system is modular, making it easy to maintain and extend.

---

# 3. Data Collection

The SHL assessment catalogue is collected using a custom web scraper.

The scraper performs the following tasks:

- Visits the SHL Product Catalogue.
- Extracts Individual Test Solutions.
- Stores assessment names.
- Stores assessment URLs.
- Extracts available descriptions.
- Retrieves duration when available.
- Detects assessment type.
- Saves all collected information into a JSON dataset.

The processed dataset is stored as:

```
shl_assessments.json
```

This file serves as the primary knowledge base for the recommendation engine.

---

# 4. Semantic Search

To improve recommendation quality, semantic search is used instead of simple keyword matching.

Each assessment is converted into a rich text representation containing:

- Assessment name
- Description
- Assessment type
- Duration
- Domain keywords

Sentence Transformers (all-MiniLM-L6-v2) generates vector embeddings for every assessment.

The generated vectors are stored as:

```
embeddings.npy
```

Metadata is stored inside:

```
assessments_index.pkl
```

These files allow fast semantic similarity search without rebuilding embeddings every time.

---

# 5. Recommendation Engine

The recommendation engine is implemented in `recommender.py`.

Its workflow is:

1. Receive the user query.
2. Generate query embeddings.
3. Compute cosine similarity.
4. Retrieve the most relevant assessments.
5. Optionally rerank results using Google's Gemini API.
6. Return the Top 10 recommendations.

If the Gemini API is unavailable, the system automatically falls back to semantic similarity ranking, ensuring uninterrupted functionality.

---

# 6. API Development

The backend is developed using FastAPI.

The available endpoints are:

### GET /health

Checks whether the API is running.

Example response:

```json
{
    "status": "healthy"
}
```

---

### POST /recommend

Accepts a query and returns recommended SHL assessments.

Example request:

```json
{
    "query":"Java Developer with SQL"
}
```

Example response:

```json
{
    "recommended_assessments":[
        {
            "name":"Java 8",
            "url":"https://www.shl.com/...",
            "duration":null
        }
    ]
}
```

The endpoint also accepts Job Description URLs.

If a URL is provided, BeautifulSoup extracts the webpage text before sending it to the recommendation engine.

---

# 7. Frontend

The project includes a lightweight HTML frontend served directly by FastAPI.

The frontend allows users to:

- Enter natural language queries
- Paste job descriptions
- Submit job posting URLs
- View recommended SHL assessments
- Open SHL assessment pages directly

The interface communicates with the backend using REST API requests.

---

# 8. Technologies Used

The project is implemented using the following technologies:

- Python
- FastAPI
- Sentence Transformers
- Scikit-learn
- NumPy
- BeautifulSoup
- Requests
- Uvicorn
- HTML
- JavaScript

---

# 9. Project Structure

```
api.py
recommender.py
scraper.py
build_embeddings.py
frontend.html
requirements.txt
README.md
shl_assessments.json
embeddings.npy
assessments_index.pkl
```

Each module performs an independent task, making the project easier to maintain.

---

# 10. Features

The implemented system supports:

- Semantic search
- Natural language queries
- Job description processing
- URL processing
- FastAPI REST API
- Interactive HTML frontend
- SHL assessment recommendations
- Optional Gemini LLM reranking
- Automatic fallback when Gemini is unavailable

---

# 11. Future Improvements

Possible future enhancements include:

- Improved ranking using larger embedding models.
- Personalized recommendations based on user profiles.
- Chat-based recommendation interface.
- Better metadata extraction from SHL pages.
- Additional assessment filtering options.

---

# 12. Conclusion

This project successfully implements an intelligent SHL Assessment Recommendation System using semantic search and machine learning techniques.

The system retrieves relevant SHL assessments from natural language queries, job descriptions, and URLs while providing a simple REST API and user-friendly web interface.

The modular architecture allows future improvements and easy deployment to cloud platforms such as Render.