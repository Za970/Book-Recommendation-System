# 📚 Book Recommendation System

A book recommender system built in Python that suggests books using both a **Popularity-Based** approach and a **Collaborative Filtering** approach (cosine similarity on user ratings).

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Project Workflow](#-project-workflow)
- [How It Works](#-how-it-works)
- [Example Usage](#-example-usage)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Future Improvements](#-future-improvements)
- [Author](#-author)
- [Acknowledgments](#-acknowledgments)

---

## 🔎 Overview

This project recommends books to users in two ways:

1. **Popularity-Based Recommender** — surfaces the top-rated books overall (great for new users with no rating history).
2. **Collaborative Filtering Recommender** — recommends books similar to a given title based on patterns in how users rated books (great for personalized, title-based recommendations).

## 📊 Dataset

- **Source:** [Book Recommendation Dataset – Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)
- **Files used:**
  - `Books.csv` — book metadata (title, author, ISBN, cover image URL)
  - `Users.csv` — user information
  - `Ratings.csv` — user ratings for books (`User-ID`, `ISBN`, `Book-Rating`)

> ⚠️ The dataset CSVs are **not included** in this repo (they're too large for GitHub). Download them from the Kaggle link above and place `Books.csv`, `Users.csv`, and `Ratings.csv` in the project root before running the notebook.

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3 |
| Data Handling | Pandas, NumPy |
| Similarity / ML | scikit-learn (`cosine_similarity`) |
| Environment | Jupyter Notebook |

## 🔁 Project Workflow

1. **Data Loading** — Read `Books.csv`, `Users.csv`, and `Ratings.csv` into Pandas DataFrames.
2. **Data Cleaning** — Check shapes, missing values, and duplicate rows across all three datasets.
3. **Popularity-Based Model:**
   - Merge `Ratings` with `Books` on `ISBN`.
   - Compute the number of ratings and average rating per book title.
   - Filter to books with **more than 250 ratings**, then sort by average rating to get the top 50 most popular books.
4. **Collaborative Filtering Model:**
   - Keep only users who have rated **more than 200 books** (to ensure reliable signal).
   - Keep only books with **at least 50 ratings** from those users.
   - Build a pivot table (`Book-Title` × `User-ID` → `Book-Rating`), filling missing values with 0.
   - Compute cosine similarity between books based on the rating patterns.
   - `recommend(book_name)` returns the top 5 most similar books.

## ⚙️ How It Works

**Popularity-based:** A book qualifies if it has enough ratings (>250) to be statistically meaningful, then books are ranked by their average rating — similar to a "Top Rated" shelf.

**Collaborative filtering:** Books are represented as vectors of ratings across users. Two books are "similar" if the same users tend to rate them similarly. Cosine similarity measures how close those vectors are, and the model recommends the books closest to the one you searched for.

## 💡 Example Usage

```python
recommend('The Notebook')
```

Returns the top 5 books most similar to *The Notebook* based on collaborative filtering.

## 📂 Project Structure

```
book-recommendation-system/
├── Untitled-1.ipynb          # Main notebook: cleaning, popularity & collaborative models
├── README.md                 # Project documentation (this file)
```

> 💡 Tip: consider renaming `Untitled-1.ipynb` to something more descriptive, like `Book_Recommendation_System.ipynb`, before pushing to GitHub.

## 🚀 Getting Started

**1. Clone the repository**
```bash
git clone https://github.com/<your-username>/book-recommendation-system.git
cd book-recommendation-system
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Download the dataset**

Get `Books.csv`, `Users.csv`, and `Ratings.csv` from [Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset) and place them in the project root folder.

**4. Run the notebook**
```bash
jupyter notebook Untitled-1.ipynb
```

## 🔮 Future Improvements

- Add a content-based filtering model (using book genres/descriptions)
- Combine popularity and collaborative filtering into a hybrid recommender
- Build a simple web app (e.g., Streamlit) for interactive recommendations
- Handle cold-start users with no rating history

## 👤 Author

- **Zaid Qasim**

## 🙏 Acknowledgments

- Dataset provided by [arashnic on Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)