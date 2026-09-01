# Lexon Beauty — Customer Segmentation & Sales Analytics using RFM and K-Means

## 📌 Overview

**Lexon Beauty Sales Analytics Dashboard** is an end-to-end retail data analytics project that transforms point-of-sale transaction data into actionable business insights.

The project combines **data cleaning, RFM (Recency, Frequency, Monetary) analysis, K-Means customer segmentation, product sales analysis, and interactive Power BI visualization** into an executive-level business intelligence solution.

The completed Power BI dashboard provides an overview of sales performance, monthly sales trends, high-value customers, top-selling products, product-category contribution, and customer segmentation insights.

---

## 📊 Executive Dashboard

![Lexon Beauty Sales Dashboard Preview](Power%20BI/dashboard_preview1.png)

### Dashboard Highlights

- **Total Penjualan:** Rp246.23 Juta
- **Total Transaksi:** 2,413
- **Rata-rata Transaksi (AOV):** Rp102,043
- **Total Pelanggan:** 1,167
- **Monthly Sales Trend**
- **Top 5 Customers by Total Spending**
- **Top 5 Products by Sales**
- **Sales by Product Category**
- **Year Filter:** 2025
- Executive navigation for Dashboard, Sales, Products, Customers, Transactions, Report, Marketing, and Settings

---

## 🛠️ Tools & Technologies

### Data Engineering & Machine Learning

- Python 3.x
- Jupyter Notebook / Google Colab
- Pandas
- NumPy
- Scikit-learn
  - K-Means Clustering
  - Standardization
  - PCA
  - Silhouette Score
- Matplotlib
- Seaborn

### Business Intelligence

- Microsoft Power BI Desktop
- Power Query
- DAX
- Star Schema data modeling
- Interactive slicers and cross-filtering
- KPI and Top-N measures

---

## 📂 Dataset

### Source

The project uses retail transaction data originating from the **MOKA POS system of Lexon Beauty**.

### Data Volume

- **Raw transaction-detail records:** 7,439 rows
- **Final unique customer profiles:** 1,167 customers
- **Anonymized customer IDs:** `CUST-00001` – `CUST-01167`

The prepared data contains transaction, customer, product, category, quantity, receipt, date, and net-sales information required for business analysis.

---

## 🔐 Data Cleaning & Anonymization

The data preparation pipeline includes:

1. Handling missing customer identifiers.
2. Cleaning inconsistent phone-number and email formats.
3. Standardizing date and time fields.
4. Removing anomaly records and unmapped walk-in guest profiles where necessary.
5. Creating a unified customer surrogate key.
6. Validating transaction and revenue consistency.
7. Preparing item-level transaction data for product analysis.
8. Mapping transaction records to customer segmentation profiles.

Customer PII is not exposed in the dashboard. Instead, customers are represented using anonymized identifiers such as:

```text
CUST-00001
CUST-00002
CUST-00003
...
CUST-01167
```

---

## 🧮 RFM Analysis

Customer behavior is evaluated using three core RFM metrics.

### Recency

Measures how recently a customer made a purchase.

```text
Recency = Reference Date − Last Purchase Date
```

A lower Recency value indicates more recent activity.

### Frequency

Measures how often a customer purchases.

```text
Frequency = DISTINCTCOUNT(Receipt Number)
```

Using `DISTINCTCOUNT` prevents multiple item rows belonging to the same receipt from being counted as multiple transactions.

### Monetary

Measures the customer's total spending.

```text
Monetary = SUM(Net Sales)
```

---

## 🤖 K-Means Customer Segmentation

RFM variables are standardized before applying K-Means clustering.

The optimal number of clusters was evaluated using the **Elbow Method**, followed by validation using the **Silhouette Score**.

### Final Segments

| Segment | Customers | Characteristics | Recommended Strategy |
|---|---:|---|---|
| **Pelanggan Setia (Loyal)** | 208 | High Frequency and Monetary contribution with relatively recent activity | VIP loyalty, rewards, early product access, exclusive offers |
| **Pelanggan Potensial (Promising)** | 431 | Moderate frequency with stable monetary contribution | Cross-selling, upselling, bundles, personalized recommendations |
| **Pelanggan Berisiko (At-Risk)** | 528 | Higher Recency with lower frequency and spending | Win-back campaigns, personalized vouchers, limited-time promotions |

**Total customers: 1,167**

### Model Evaluation

- **Silhouette Score:** 0.36
- **Optimal clusters:** 3

PCA was also used to project the customer clusters into two dimensions for visual inspection.

---

# 📈 Sales Analytics in Power BI

The completed dashboard adds an executive sales-performance layer on top of the customer segmentation analysis.

## 1. Monthly Sales Trend

The line chart displays monthly sales performance and makes it easier to identify:

- Sales peaks and declines
- Monthly seasonality
- Changes in business performance
- Periods requiring further investigation

---

## 2. Top 5 Customers by Total Spending

Customers are ranked according to accumulated net sales contribution.

Customer IDs are anonymized to protect customer privacy while still allowing customer-level analysis.

The ranking dynamically responds to the selected reporting period.

---

## 3. Top 5 Products by Sales

Product performance is analyzed at the **item/product level**, rather than treating a receipt number as a product.

A single receipt can contain multiple products.

For example:

```text
Receipt 3BOGHN
├── Wardah Glasting Liquid Lip 01 Caramel Coat
├── Wardah Glasting Liquid Lip 04 Rosewood Radiance
├── Wardah Perfect Bright Creamy Foam Bright + Oil Control 100 ml
└── Wardah Colorfit Perfect Glow Cushion 21W Linen
```

Therefore:

```text
Receipt Number = Transaction
SKU / Variant  = Product
```

The product-detail preparation uses the **Receipt Number** to determine which products belong to each transaction, while product-level identifiers such as **SKU** and **Variant** are used to identify the products themselves.

This approach allows product sales to be aggregated correctly at the product level and used for Top-N product analysis.

### Product Analysis Logic

The product analysis follows this structure:

```text
Receipt Number
      ↓
Identify all items purchased in the receipt
      ↓
Match Product / Variant / SKU
      ↓
Create item-level product records
      ↓
Aggregate product sales
      ↓
Rank products
      ↓
Top 5 Products by Sales
```

This prevents the analysis from incorrectly treating one receipt as one product.

---

## 4. Sales by Product Category

The dashboard summarizes net sales contribution by product category.

The category-level analysis supports business decisions related to:

- Product assortment
- Inventory planning
- Promotional campaigns
- Category-level marketing
- Cross-selling opportunities

---

# 💡 Business Insights

## 1. Loyal Customers — 208

The **208 Loyal customers** represent the highest-value relationship group and should receive retention-focused treatment.

### Recommended Actions

- VIP / loyalty tiers
- Exclusive promotions
- Early access to new products
- Personalized recommendations
- Customer rewards

---

## 2. Promising Customers — 431

The **431 Promising customers** represent a significant growth opportunity.

### Recommended Actions

- Cross-selling
- Upselling
- Product bundles
- Personalized skincare recommendations
- Product education campaigns

---

## 3. At-Risk Customers — 528

The **528 At-Risk customers** represent the largest customer segment and a major reactivation opportunity.

### Recommended Actions

- Win-back campaigns
- Personalized discount vouchers
- Limited-time offers
- Targeted messaging
- Recommendations based on previous purchases

> **Key Insight: 528 At-Risk customers require a targeted re-engagement campaign to recover inactive customer relationships and create opportunities for repeat purchases.**

---

# 🏗️ Data Architecture

The Power BI model follows a structured analytical approach using a **Star Schema** where appropriate.

```text
                    ┌─────────────────┐
                    │   Date Table    │
                    └────────┬────────┘
                             │
                             ▼
┌────────────────┐     ┌──────────────────────────┐
│ Customer / RFM │ ──► │ Transaction / Detail    │
│ Dimension      │     │ Fact Data               │
└────────────────┘     └────────────┬─────────────┘
                                    │
                                    ▼
                           ┌─────────────────┐
                           │ Product Detail  │
                           └─────────────────┘
```

Relationships are designed around appropriate business keys using **1-to-Many (`1:*`) single-direction filtering** where applicable.

---

# 🧠 Key DAX Engineering

## Anonymized Customer ID

```DAX
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

## Frequency

```DAX
Frequency =
DISTINCTCOUNT(
    'transaction_details_with_segments'[Receipt Number]
)
```

## Monetary

```DAX
Monetary =
SUM(
    'transaction_details_with_segments'[Net Sales]
)
```

These calculations support customer profiling and dashboard KPI calculations while avoiding incorrect transaction counts caused by multiple item rows within a receipt.

---

# 🎨 Dashboard Design

The completed dashboard follows an executive BI design system:

| Design Element | Specification |
|---|---|
| Primary Color | `#2E86AB` |
| Secondary Color | `#A23B72` |
| Accent Color | `#F18F01` |
| Background | White / Very Light Gray |
| Typography | Modern Sans-Serif |
| Layout | Grid-Based Executive Dashboard |
| Visuals | KPI Cards, Line Chart, Bar Charts, Donut Chart |
| Filter | Year / Date Filter |

The dashboard emphasizes:

- Clean visual hierarchy
- Business readability
- Consistent spacing
- Minimal visual clutter
- Executive-level presentation
- Actionable data storytelling

---

# 📁 Project Structure

```text
Lexon-Beauty/
│
├── RFM_Model_Analysis.ipynb
│
├── Power BI/
│   ├── Lexon Beauty Dashboard.pbix
│   └── dashboard_preview1.png
│
└── README.md
```

---

# 🚀 How to Open the Project

## 1. Python / RFM Analysis

Open:

```text
RFM_Model_Analysis.ipynb
```

using **Jupyter Notebook** or **Google Colab**.

The notebook contains:

- Data preparation
- Data cleaning
- RFM calculation
- Customer profiling
- K-Means clustering
- Elbow Method evaluation
- Silhouette Score evaluation
- PCA visualization
- Customer segmentation analysis

---

## 2. Power BI Dashboard

Open:

```text
Power BI/Lexon Beauty Dashboard.pbix
```

using **Power BI Desktop**.

The PBIX file contains:

- Executive dashboard
- KPI cards
- Sales trend analysis
- Top customer analysis
- Top product analysis
- Product category analysis
- Customer segmentation
- DAX calculations
- Interactive filters
- Data model

---

# 🎯 Project Objective

The primary objective of this project is to demonstrate how raw retail transaction data can be transformed into a practical decision-support system.

The complete analytical workflow is:

```text
Raw POS Data
      ↓
Data Cleaning
      ↓
Customer & Product Preparation
      ↓
RFM Analysis
      ↓
K-Means Clustering
      ↓
Customer Segmentation
      ↓
Sales Analytics
      ↓
Power BI Executive Dashboard
      ↓
Actionable Business Strategy
```

The final solution helps Lexon Beauty understand:

- **Who are the customers?**
- **How frequently do they purchase?**
- **How much do they spend?**
- **Which products generate the most sales?**
- **Which product categories contribute the most revenue?**
- **Which customers are loyal, promising, or at risk?**
- **What marketing actions should be prioritized?**

---

# 📌 Key Project Results

| Metric | Result |
|---|---:|
| Raw Transaction Details | 7,439 rows |
| Unique Customers | 1,167 |
| Total Net Sales | Rp246.23 Juta |
| Total Transactions | 2,413 |
| Average Transaction | Rp102,043 |
| Customer Segments | 3 |
| Loyal Customers | 208 |
| Promising Customers | 431 |
| At-Risk Customers | 528 |
| Silhouette Score | 0.36 |

---

# 👤 Author

**Alif Nursetyo Vimanto**

Data Analytics / Data Science Project

---

# 📌 Disclaimer

This project is intended for analytical and portfolio purposes.

Customer information shown in the project has been anonymized using surrogate customer identifiers. No personally identifiable customer information is intentionally exposed in the final dashboard.

The dashboard and analytical results are based on the prepared dataset and business rules defined throughout the project.
