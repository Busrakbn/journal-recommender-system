# Journal Finder — Data Mining Final Project

A computer science journal recommendation system. Given an article's abstract, it returns the **top 5 most relevant journals** for submission using TF-IDF vectorization, K-Means clustering, and cosine similarity.

---

## Dataset

- `journal_data.csv` — 7,711 articles from 175 Computer Science journals
- The CSV has **no header row**. Columns are assigned manually in code:
  `AcademicRecordId`, `AbstractText`, `JournalName`, `Keywords`, `Subjects`

---

## Requirements

Install all dependencies before running:

```bash
pip install pandas scikit-learn matplotlib nltk
```

NLTK data (stopwords, wordnet) will be downloaded automatically the first time you run the preprocessing cell. An internet connection is required for that step only.

---

## How to Run

### Option 1: Local (VS Code or JupyterLab) — Recommended

1. Make sure `journal_data.csv` and `DM_hw.ipynb` are in the **same folder**.
2. Open a terminal in that folder and run:
   ```bash
   jupyter notebook DM_hw.ipynb
   ```
   Or open `DM_hw.ipynb` directly in **VS Code** and select a Python kernel from the top-right corner.
3. Run all cells **in order from top to bottom**:
   - In Jupyter: **Kernel → Restart & Run All**
   - In VS Code: **Run All** button at the top of the notebook

### Option 2: Google Colab

1. Upload `journal_data.csv` to your **Google Drive** root (`My Drive/journal_data.csv`).
2. Open `DM_hw.ipynb` in Google Colab (File → Upload notebook).
3. Mount Google Drive when prompted, then run all cells in order.

---

## Cell-by-Cell Guide

| Cell | Description |
|------|-------------|
| **Cell 1** | Loads the dataset — auto-detects Google Drive vs. local path, assigns column names |
| **Cell 2** | Data verification — prints dataset shape, column list, and unique journal count |
| **Cell 3** | NLP preprocessing — removes HTML, stopwords, and lemmatizes text; merges abstract + keywords + subjects into one feature |
| **Cell 4** | Elbow curve (k=2–15) + K-Means (k=10) + PCA scatter plot + top keywords per cluster |
| **Cell 5** | Builds journal profile vectors; prompts for user abstract input; returns top 5 journals |

---

## Using the Recommendation System

At the top of the last code cell, set the `MY_ABSTRACT` variable to your article's abstract, then run the cell:

```python
MY_ABSTRACT = "Your article abstract goes here..."
```

The output will print the top 5 recommended journals:

```
--- Top 5 Recommended Journals ---
1. ACM COMPUTING SURVEYS (Similarity Score: 0.3821)
2. IEEE TRANSACTIONS ON NEURAL NETWORKS (Similarity Score: 0.3104)
...
```

If `MY_ABSTRACT` is left as `""`, the system runs a built-in sample abstract automatically.

> **Note:** `input()` is not used because it blocks indefinitely in VS Code's notebook kernel. Setting `MY_ABSTRACT` directly is the reliable cross-platform approach.

---

## Notes

- **Run cells in order.** Later cells depend on variables created by earlier cells (`df`, `X`, `tfidf`, `clean_text`). Running out of order will cause a `NameError`.
- **Cell 4 takes ~1 minute.** The elbow method runs K-Means 14 times to evaluate different values of k. This is intentional and only runs once.
- **Re-running is safe.** All cells are idempotent — re-running simply overwrites variables with the same values.
- **NLTK download:** The first run of Cell 3 downloads ~3 MB of NLTK data. Subsequent runs skip the download automatically.
