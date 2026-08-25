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
  - Custom DAX Measures (Dynamic currency formatting, RFM metrics, and aggregated KPI cards)

## 📊 Dataset & Anonymization Notice
- **Source**: Real retail transaction details from MOKA POS (Lexon Beauty Store).
- **Total Raw Transactions**: 7,439 rows.
- **Data Cleaning Pipelines**:
  - Handled missing Customer IDs and cleaned raw string phone numbers/emails.
  - Excluded anomaly records and unmapped walk-in guest profiles to ensure revenue integrity.
  - Final valid unique customers for ML pipeline & RFM profiling: **1,167** customers.
- **🔒 Corporate Privacy Compliance**: Raw data containing sensitive Personal Identifiable Information (PII) such as real customer names and phone numbers has been anonymized and masked using unique secure indexing codes (`CUST-00001` to `CUST-01167`) generated via DAX/Power Query ETL processing.

## 📈 Project Methodology & Architecture
1. **Data Cleaning & Anonymization:** Handled missing values, formatted chronological locale fields, and removed transaction anomalies.
2. **RFM Metrics Engineering:** Calculated exact Recency (days since last purchase), Frequency (`DISTINCTCOUNT` of transaction receipt numbers), and Monetary (total net sales spend) for each individual member profile.
3. **K-Means Clustering Evaluation:** Determined the optimal number of customer clusters using the Elbow Method.
4. **Cluster Validation:** Validated statistical quality using the Silhouette Score algorithm.
5. **Dimensionality Reduction:** Applied PCA (Principal Component Analysis) for 2D visual projection of customer clusters.
6. **Data Modeling (Star Schema):** Modeled the Python-segmented customer dimension table (`transaction_details_with_segments`) with a clean `1-to-Many` (`*:1`) single-direction relationship to the transactional fact table (`Report Item Details`) to ensure filter context accuracy.
7. **Business Strategy Execution:** Formulated targeted operational strategies based on generated segment profiles.

## 🎯 Results & Business Insights

### Optimal Clusters: **3 Segments**

| Segment | Number of Customers | Key Characteristics | Strategic Business Recommendation |
|---------|--------------------|---------------------|-----------------------------------|
| **Pelanggan Setia (Loyal)** | 208 | High Frequency & High Monetary, Low Recency (Highly Active) | Reward with premium tier loyalty programs, early access to new cosmetic product drops, and exclusive VIP offers. |
| **Pelanggan Potensial (Promising)** | 431 | Moderate transaction frequency, stable monetary contribution. | Encourage increased cross-selling and up-selling spending habits through personalized skincare routine recommendations. |
| **Pelanggan Berisiko (At-Risk)** | 528 | High Recency (Inactive for a long time), Low Frequency & low spend. | Run re-engagement win-back campaigns, utilize push notifications, and offer time-limited beauty promo vouchers. |

### Model & Analytics Performance
- **Machine Learning Model Validation:** **Silhouette Score of 0.36** (highly acceptable for real-world retail point-of-sale data containing commercial noise).
- **Dashboard Integrity & Financial Audit:** Fully verified custom DAX measures ensuring complete alignment between top KPI cards and detail table totals without circular dependency or ambiguity:
  - **Total Penjualan Bersih (Net Sales):** `Rp246.2 Juta` (`Rp246,229,208`)
  - **Total Transaksi (Total Transactions):** `2,413 Transaksi`
  - **Rata-rata Transaksi (AOV):** `Rp102,043`
  - **Total Pelanggan (Total Active Customers):** `1,167 Pelanggan`

## 🚀 How to Open the Project
1. Clone this repository to your local computer.
2. Open `RFM_Model_Analysis.ipynb` inside Jupyter Notebook/Google Colab to view the complete Python data science workflow.
3. Open `Power BI/Lexon Beauty Dashboard.pbix` using **Power BI Desktop** to explore the fully functional interactive report, modify time ranges using the date slicer, or drill down into individual customer segmentation profiles.
