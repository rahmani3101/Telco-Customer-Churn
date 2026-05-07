# 📡 Telco Customer Churn Analysis — Power BI Dashboard

> **Advanced business intelligence report** analyzing customer churn patterns across 7,000+ telecom customers — built with Power Query transformations, DAX measures, and a 3-page executive dashboard in Power BI.

---

## 📌 Project Overview

Customer churn is one of the most critical business metrics in the telecom industry. This project dives deep into **why customers leave**, **which segments are at highest risk**, and **how much revenue is at stake** — presenting actionable insights through an interactive Power BI dashboard.

| Metric | Value |
|---|---|
| 📊 Dataset Size | 7,043 customers · 21 features |
| 📉 Overall Churn Rate | **26.5%** |
| 💸 Revenue at Risk (Monthly) | High-value churners on Fiber Optic + M2M contracts |
| 🛠️ Tools Used | Power BI Desktop, Power Query (M), DAX |

---

## 📁 Repository Structure

```
📦 Telco-Customer-Churn/
├── 📄 Telco-Customer-Churn.csv       # Raw source dataset (Raw dataset from kaggle)
├── 📄 Churn Fact.csv                 # Cleaned fact table (post Power Query)
├── 📄 Service Flags.csv              # Service-level reference table (DAX derived)
└── 📊 TELCO Churn Analysis.pbix      # Power BI report file (open in Power BI Desktop)
```

---

## 🔧 Power Query Transformations

All data preparation was done inside **Power Query Editor** before loading into the model:

- **Data Type Correction** — Fixed `TotalCharges` and `MonthlyCharges` to Decimal; `tenure` to Whole Number
- **SeniorCitizen Encoding** — Replaced binary `0/1` with `No/Yes` for readability
- **Tenure Bucketing** — Custom column grouping tenure into `0–1 Year`, `1–2 Years`, `2–4 Years`, `4+ Years`
- **Charges Tier** — Segmented `MonthlyCharges` into `Low (<$35)`, `Medium ($35–$65)`, `High (>$65)`
- **Text Cleaning** — Trim + Clean applied to all string columns to eliminate hidden whitespace

---

## 📐 Data Model

```
Telco_Churn_Raw (source)
        │
        ▼
  Churn_Fact (working table)
        │
        ▼
  ServiceFlags (DAX-derived reference table)
        │
        ▼
  _Measures (dedicated measures table)
```

---

## 📊 DAX Measures

Key measures powering the dashboard:

```dax
-- Churn Rate %
Churn Rate % = DIVIDE([Total Churned], [Total Customers], 0)

-- Revenue at Risk
Revenue at Risk =
CALCULATE(
    SUMX(Churn_Fact, Churn_Fact[MonthlyCharges]),
    Churn_Fact[Churn] = "Yes"
)

-- Month-to-Month Churn Rate
M2M Churn Rate =
CALCULATE(
    [Churn Rate %],
    Churn_Fact[Contract] = "Month-to-month"
)

-- Avg Tenure of Churned Customers
Avg Tenure Churned =
CALCULATE(AVERAGE(Churn_Fact[tenure]), Churn_Fact[Churn] = "Yes")
```

---

## 📋 Dashboard Pages

### Page 1 — Executive Summary
KPI cards (Total Customers, Churn Rate %, Revenue at Risk, Avg Tenure Churned) · Donut chart (Churn vs Retained) · Bar chart (Churn Rate by Contract Type) · Stacked bar (Tenure Group distribution)

### Page 2 — Customer Segmentation
Matrix with conditional formatting (Internet Service × Contract × Churn Rate) · Scatter plot (MonthlyCharges vs Tenure, colored by Churn) · Churn Rate by Payment Method · Gender / Senior / Partner slicers

### Page 3 — Services & Revenue Deep Dive
Revenue at Risk vs Retained by Internet Service · Charges Tier waterfall · Service adoption heatmap (Security, TechSupport, Streaming) · M2M Churn Rate KP

---

## 💡 Key Insights

- 🔴 **Month-to-month contract customers churn at ~3× the rate** of customers on annual or two-year plans
- 🔴 **Fiber Optic internet users** show ~41% churn vs ~19% for DSL users — despite being the premium tier
- 🔴 **Electronic check payment** is the highest-churn payment method — likely correlating with lower engagement
- 🟢 Customers with **2+ years tenure** have significantly lower churn probability regardless of contract type
- 🟡 The **highest-risk segment** is: Month-to-month + Fiber Optic + Electronic Check + No TechSupport

---

## 🚀 How to Use

1. Clone or download this repository
2. Open `TELCO Churn Analysis.pbix` in **Power BI Desktop** (free download from Microsoft)
3. All data is embedded — no external connection needed
4. Use the slicers on each page to filter by demographics, contract type, or service

---

## 🗂️ Dataset Source

**IBM Watson Analytics Sample Data — Telco Customer Churn**
> A widely used public dataset for churn modeling and business analytics practice. Contains customer demographics, subscribed services, account information, and churn labels.

---

## 👤 Author

**Mohammad Asad Rahmani**
Final Year B.Tech — Computer Science (AI & ML), Techno India University, Kolkata

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/rahmani3101)
[![GitHub](https://img.shields.io/badge/GitHub-rahmani3101-181717?style=flat&logo=github)](https://github.com/rahmani3101)

> 2× Google Cloud Arcade Facilitator · Teaching Assistant — Data Science @ GeeksforGeeks · GCP · BigQuery · Power BI · Apache Spark

---

*This project is part of my data analytics portfolio, showcasing end-to-end BI development from raw data ingestion through Power Query to executive-level dashboard delivery.*
