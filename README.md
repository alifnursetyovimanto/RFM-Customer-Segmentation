# Lexon Beauty — Customer Segmentation using RFM & K-Means Clustering

## 📌 Overview
This project performs an end-to-end data analytics solution applying **Unsupervised Machine Learning (K-Means Clustering)** and **RFM (Recency, Frequency, Monetary)** analysis to segment customers of **Lexon Beauty**. The final output integrates a data pipeline built in Python with an executive-level interactive dashboard created in **Power BI Desktop** to provide actionable marketing recommendations for business growth.

## 📊 Executive Dashboard Preview
![Lexon Beauty Dashboard Preview](Power%20BI/dashboard_preview.png)

## 🛠️ Tools & Libraries
- **Data Engineering & Machine Learning (Python 3.x):** 
  - Jupyter Notebook
  - Pandas & NumPy (Data manipulation & cleaning)
  - Scikit-learn (K-Means clustering, PCA, standard preprocessing)
  - Matplotlib & Seaborn (Exploratory statistical charts)
- **Data Modeling & Visualization (Power BI Desktop):**
  - Star Schema Data Architecture (`1-to-Many` Single-Direction Relationship)
  - Custom DAX Engineering (Dynamic currency formatting and aggregated KPI metrics)

## 📊 Dataset & Anonymization Notice
- **Source**: Real retail transaction details from MOKA POS (Lexon Beauty Store).
- **Total Raw Transactions**: 7,439 rows.
- **Data Cleaning Pipelines**:
  - Handled missing Customer IDs and cleaned raw string phone numbers/emails.
  - Excluded anomaly records and unmapped walk-in guest profiles to ensure revenue integrity.
  - Final valid unique customers for ML pipeline & RFM profiling: **1,167** customers.
- **🔒 Corporate Privacy Compliance**: Sensitive Personal Identifiable Information (PII) has been anonymized and masked using unique secure indexing codes (`CUST-00001` to `CUST-01167`) generated via DAX ranking.

## 📈 Project Methodology & Architecture
1. **Data Cleaning & Anonymization:** Handled missing values, formatted chronological locale fields, and mapped raw customer identity values into a unified surrogate key (`CUST-00001`).
2. **RFM Metrics Engineering:** 
   - **Recency:** Days elapsed between the customer's last purchase date and reference cutoff date.
   - **Frequency:** `DISTINCTCOUNT` of receipt numbers.
   - **Monetary:** Sum of net sales spent per individual profile.
3. **K-Means Clustering Evaluation:** Determined optimal clusters using the Elbow Method.
4. **Cluster Validation:** Validated statistical quality using the Silhouette Score algorithm.
5. **Dimensionality Reduction:** Applied PCA for 2D visual projection of customer clusters.
6. **Data Modeling (Star Schema):** Relates dimension and fact tables via a clean `1-to-Many` (`1:*`) single-direction filter context.
7. **Business Strategy Execution:** Formulated targeted operational strategies based on generated segment profiles.

## ⚙️ Key Technical Fix: Unique Customer ID (DAX)
To prevent duplicate IDs per row and ensure every distinct customer maps to a single ID (`CUST-00001` to `CUST-01167`):

```dax
Customer_ID_New = 
"CUST-" & 
FORMAT(
    RANKX(
        ALL('transaction_details_with_segments'[Customer]), 
        'transaction_details_with_segments'[Customer], 
        , 
        ASC, 
        Dense
    ), 
    "00000"
)
```

## 🎯 Results & Business Insights

### Optimal Clusters: **3 Segments**

| Segment | Number of Customers | Key Characteristics | Strategic Business Recommendation |
| --- | --- | --- | --- |
| **Pelanggan Setia (Loyal)** | 208 | High Frequency & High Monetary, Low Recency | Reward with premium tier loyalty programs, early access to new product drops, and exclusive VIP offers. |
| **Pelanggan Potensial (Promising)** | 431 | Moderate transaction frequency, stable monetary contribution. | Encourage increased cross-selling and up-selling spending habits through personalized skincare routine recommendations. |
| **Pelanggan Berisiko (At-Risk)** | 528 | High Recency (Inactive), Low Frequency & low spend. | Run re-engagement win-back campaigns, utilize push notifications, and offer time-limited beauty promo vouchers. |

### Model & Analytics Performance

* **Machine Learning Model Validation:** **Silhouette Score of 0.36** (acceptable for real-world retail point-of-sale data containing commercial noise).
* **Dashboard Integrity:**
* **Total Penjualan Bersih (Net Sales):** `Rp246.23 Juta`
* **Total Transaksi (Total Transactions):** `2,413 Transaksi`
* **Rata-rata Transaksi (AOV):** `Rp102,043`
* **Total Pelanggan (Total Active Customers):** `1,167 Pelanggan`

## 🚀 How to Open the Project

1. Clone this repository to your local computer.
2. Open `RFM_Model_Analysis.ipynb` inside Jupyter Notebook/Google Colab to view the Python workflow.
3. Open `Power BI/Lexon Beauty Dashboard.pbix` using **Power BI Desktop** to explore the interactive report.
