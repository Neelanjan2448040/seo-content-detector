# SEO Content Quality & Duplicate Detector

## 📝 Project Overview
This project is a machine learning pipeline that analyzes web content for SEO quality. It parses HTML from a provided dataset, engineers features like word count and readability, detects duplicate content using cosine similarity, and scores content quality (Low, Medium, High) using a Random Forest model.

---

## 🚀 Setup & Quick Start

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Neelanjan2448040/seo-content-detector](https://github.com/Neelanjan2448040/seo-content-detector)
    ```

2.  **Navigate to the project directory:**
    ```bash
    cd seo-content-detector
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the analysis:**
    * Open and run the Jupyter Notebook located at:
        `notebooks/seo_pipeline.ipynb`
    * The notebook will read from `data/data.csv`, run the entire pipeline, and save all outputs (new CSVs and the `.pkl` model) to the correct `data/` and `models/` folders.

---

## 🛠️ Key Decisions

* **HTML Parsing:** Used **BeautifulSoup** to robustly parse HTML. The logic tries common content tags (`<article>`, `<main>`) first, then falls back to all `<p>` tags to ensure text is extracted even from non-standard pages.
* **Embeddings & Similarity:** Used **TF-IDF + TruncatedSVD** for embeddings. This is a fast, reliable, and classic NLP approach for similarity that doesn't require downloading large transformer models.
* **Similarity Threshold:** A threshold of **0.80** was used to define duplicate content. This value is a common baseline for identifying high similarity without flagging minor overlaps.
* **Model Selection:** Chose a **Random Forest Classifier** because it's excellent at handling numerical features with different scales (like `word_count` and `flesch_reading_ease`) and provides clear feature importances.

---

## 📊 Results Summary

* **Duplicate Detection:** Found **4 duplicate pairs** with a similarity score > 0.80.
* **Model Performance:**
    * **Model Accuracy: 0.92**
    * **Baseline Accuracy: 0.36**
    * The model's 92% accuracy significantly outperforms the 36% baseline, showing it learned the rules effectively.
* **Top 3 Features:**
    1.  `flesch_reading_ease` (Importance: 0.403)
    2.  `word_count` (Importance: 0.324)
    3.  `sentence_count` (Importance: 0.273)

---

## ⚠️ Limitations

* **Parser:** The HTML parser is heuristic and may struggle with sites that heavily rely on JavaScript to render content.
* **Scraper:** The `analyze_url` function uses a basic `requests.get()` scraper and will be blocked by many modern websites with anti-bot protections (e.g., Cloudflare).
* **Labels:** The quality labels are synthetic (rule-based) as per the assignment. A real-world model would require a much larger, human-labeled dataset to be truly effective.