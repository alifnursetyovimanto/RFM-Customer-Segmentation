# Customer Segmentation using RFM & K-Means Clustering

## 📌 Overview

This project performs **customer segmentation** using **RFM (Recency, Frequency, Monetary)** analysis and **K-Means clustering** on real retail transaction data.

The goal is to identify customer segments and provide actionable marketing recommendations to improve customer retention and business growth.

## 📊 Dataset

- **Source**: Real transaction data from MOKA POS (retail business)
- **Total raw transactions**: 1,722 rows
- **Data cleaning**:
  - Handled 35.4% missing Customer IDs
  - Removed 272 anomaly/refund transactions
  - Final valid unique customers: **1,167**
- **Note**: Raw data is confidential and not included in this repository. Only aggregated results and code are shared.

## 🛠️ Tools & Libraries

- Python 3.x
- Pandas & NumPy (data manipulation)
- Scikit-learn (K-Means clustering, PCA, preprocessing)
- Matplotlib & Seaborn (visualization)
- Jupyter Notebook

## 📈 Methodology

1. **Data Cleaning** – Handle missing values, remove anomalies
2. **RFM Score Calculation** – Calculate Recency, Frequency, Monetary for each customer
3. **K-Means Clustering** – Determine optimal clusters using Elbow Method
4. **Cluster Validation** – Silhouette Score evaluation
5. **PCA Visualization** – 2D projection of clusters
6. **Segment Profiling** – Snake Plot to understand cluster characteristics
7. **Business Recommendations** – Actionable insights per segment

## 🎯 Results

### Optimal Clusters: **3 Segments**

| Segment | Number of Customers | Characteristics | Recommendation |
|---------|--------------------|-----------------|----------------|
| **Loyal / Champion** | 208 | High Frequency & Monetary, Low Recency | Reward with loyalty programs, exclusive offers |
| **Promising** | 431 | Average interaction, stable | Encourage increased spending with targeted campaigns |
| **At-Risk / Lost** | 528 | High Recency (inactive), Low Frequency | Run re-engagement campaigns, win-back offers |

### Model Performance

- **Silhouette Score**: 0.36 (acceptable for real-world retail data with noise)
