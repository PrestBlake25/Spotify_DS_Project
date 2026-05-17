# 🎵 Spotify Top Streamed Songs — Data Science Project

**Author:** Preston Blake  
**Dataset Source:** [Rakkesh Aravind G — Kaggle](https://www.kaggle.com/)  
**Project Website:** [Google Sites](https://sites.google.com/view/spotify-ds-proj-prestblake25/home)

---

## 📖 Overview

This project analyzes the **Spotify Top 10,000 Streamed Songs** dataset to uncover patterns in song popularity and build predictive models for total stream counts. The analysis spans exploratory data analysis (EDA), multiple linear regression, K-Nearest Neighbors (KNN) regression, and decision tree modeling.

---

## 📂 Repository Structure

```
Spotify_DS_Project/
│
├── Images/                                          # Visualizations and charts
├── Spotify_Project_Part_1.ipynb                     # EDA & data exploration
├── Spotify_Project_Part_2_(Linear_Regression).ipynb # Linear regression models
├── Spotify_Project_Part_2_K_Nearest_Neighbors.ipynb # KNN models
└── Spotify_final_dataset.csv                        # Cleaned dataset
```

---

## 📊 Dataset

The dataset contains **11,084 rows × 9 columns**, where each row represents a unique song.

| Column | Description |
|---|---|
| `Position` | Spotify ranking |
| `Artist Name` | Name of the artist |
| `Song Name` | Name of the song |
| `Days` | Days since the song's release (updated) |
| `Top 10 (xTimes)` | Number of times the song appeared in the Top 10 |
| `Peak Position` | Highest chart position attained |
| `Peak Streams` | Total streams during peak position |
| `Peak Position (xTimes)` | Number of times peak position was reached |
| `Total Streams` | Cumulative stream count |

**Notes:** Data is Spotify-only (no other platforms). The dataset contains 4 rows with missing song titles and no duplicate rows.

---

## 🔍 Part 1: Exploratory Data Analysis

Key visualizations and findings:

- **Distribution of Peak Positions** — Most songs cluster near positions #0–#25; fewer songs reached lower-ranked peak positions.
- **Distribution of Songs in Top 10** — Right-skewed: most songs barely cracked the Top 10, while a small number of dominant hits appeared there repeatedly.
- **Distribution of Days Since Release** — Also right-skewed, indicating that the most-streamed songs were relatively recent at the time of dataset creation.
- **Distribution of Total Streams** — Heavily skewed: over 9,000 songs have fewer than 100M streams, while only a tiny fraction surpass 800M.
- **Top 10 Times vs. Total Streams** — Strong positive correlation; songs that appear in the Top 10 more often accumulate significantly more streams.
- **Days Since Release vs. Total Streams** — Positive correlation: older popular songs accumulate more streams over time.
- **Position vs. Peak Streams** — Weak negative correlation; chart position alone is not a reliable predictor of peak streaming performance.

---

## 📈 Part 2: Predictive Modeling

### Linear Regression

Two multiple linear regression models were built to predict **Total Streams**:

| Model | Predictors | Train R² | Test R² | Test MSE |
|---|---|---|---|---|
| Model 1: Popularity & Longevity | Peak Streams, Days Since Release | 0.887 | 0.898 | 3.41 × 10¹⁴ |
| Model 2: Popularity & Viral Consistency | Peak Streams, Top 10 (xTimes) | 0.571 | 0.583 | 1.40 × 10¹⁵ |

**Takeaway:** Model 1 significantly outperforms Model 2. Peak streams combined with days since release explains ~90% of variance in total streams, making longevity a strong predictor of streaming success.

---

### K-Nearest Neighbors (KNN)

| Model | Predictors | K | Train MSE | Test MSE |
|---|---|---|---|---|
| Model 1: Popularity & Longevity | Peak Streams, Days Since Release | 3 | 1.40 × 10¹⁵ | 3.11 × 10¹⁵ |
| Model 2: Popularity & Viral Consistency | Peak Streams, Top 10 (xTimes) | 24 | 1.94 × 10¹⁵ | 2.68 × 10¹⁵ |

Model 1 has stronger raw predictive power but shows more overfitting. Model 2 (K=24) generalizes better, though with a higher overall MSE. The number of Top 10 appearances adds minimal predictive value beyond peak streams alone.

---

### Decision Tree

A decision tree was explored to predict **Peak Streams** without using Total Streams, Position, or Peak Position as inputs. Testing revealed that models with a max depth beyond 4 overfit significantly.

- **Optimal depth: 3**
  - Training MSE: 181,682,022,159
  - Testing MSE: 169,624,377,145

---

## ✅ Final Recommendation

The **Linear Regression Model 1** (Peak Streams + Days Since Release) is the best model overall, achieving ~90% explained variance (R² ≈ 0.898 on test data) with closely matched training and testing scores — indicating low overfitting. Peak streams and song longevity are the strongest indicators of a song's cumulative streaming success.

---

## 🛠️ Technologies Used

- Python
- Jupyter Notebook
- pandas, numpy
- matplotlib, seaborn
- scikit-learn

---

## 🔗 Links

- 📊 [Full Project Website (Google Sites)](https://sites.google.com/view/spotify-ds-proj-prestblake25/home)
- 📁 [Dataset on Kaggle — Spotify Top 10000 Streamed Songs](https://www.kaggle.com/)
