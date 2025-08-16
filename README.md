# 🚚 E-Commerce Delay Prediction Pipeline (AWS) 

This project builds an **end-to-end data pipeline and predictive model** for late delivery detection using the **Olist e-commerce dataset**. It demonstrates large-scale data handling on AWS, machine learning with XGBoost, and business-focused storytelling with Power BI.

---

## 💼 Problem Context

E-commerce companies face rising **customer dissatisfaction** due to late deliveries. The challenge is to **predict high-risk orders early** and trigger mitigation steps (e.g., expedited shipping, proactive customer notifications).

This project shows how cloud-scale data + ML can solve operational pain points.

---

## 📂 Dataset

This project uses the real **Olist E-Commerce Dataset** from Kaggle, containing ~1.5M records across multiple tables.

Source: Kaggle — Olist Brazilian E-Commerce Public Dataset.

---

## 📌 Executive Summary

- **Data Scale**: Processed ~1.5M Olist records on AWS (S3 + Glue + Athena).  
- **Model**: Trained XGBoost with imbalance handling, tuned for **recall priority**.  
- **Results**: Base delay ≈ **6.6%**, **Recall ≈ 99%**, **Precision ≈ 6.7%**, **AUC ≈ 0.585**.  
- **Visualization**: Delivered an interactive Power BI dashboard (KPIs, confusion matrix, distribution analysis).  

> **Business takeaway**: Use as an *early-warning system* to flag risky orders, reducing missed delays.

---

## 🛠️ Tech Stack

- **Cloud & Data**: S3 (raw/curated zones), Glue Jobs & Crawlers, Glue Data Catalog, Athena (CTAS, Parquet)
- **ML/Compute**: PySpark, Python (Pandas, scikit-learn), XGBoost (threshold tuning, class imbalance)
- **Security/Access**: IAM roles & policies
- **Visualization**: Power BI (KPI cards, confusion matrix, histograms)

---

## 📁 Project Structure

- `aws_pipeline/` — Glue scripts & Athena SQL for ETL  
- `model/` — XGBoost training, feature engineering, export  
- `powerbi/` — Dashboard walkthrough  
- `visuals/` — Power BI screenshots (KPI, confusion matrix, probability distribution)
  
--- 

## 🧠 Modeling  
- Trained an XGBoost model on processed features to predict delivery delays.  
- **Feature Engineering**: Derived variables such as shipping times, review scores, lag features (e.g., lag7), and rolling averages (e.g., ma7) to improve predictive power.  
- The pipeline can be easily extended to include **feature importance visualization**, offering interpretable insights into key drivers of delays.

--- 

## 🗄️ Data Engineering (ETL)

- Ingested raw Olist tables into **S3** (raw zone).  
- Built Glue ETL jobs to join and transform multi-table data.  
- Produced **dimension tables** (customers, products, sellers) and **fact tables** (orders, order items) in curated Parquet format, partitioned by purchase date/state for efficiency.  
- Registered all tables in the **Glue Data Catalog** for querying via Athena.

---

## 🌟 Key Results Summary

| Metric                  | Value   |
|--------------------------|---------|
| Base Delay Rate          | ~6.6%   |
| Recall (t=0.25)          | ~99%    |
| Precision (t=0.25)       | ~6.7%   |
| AUC                      | ~0.585  |

---

## 📊 Visual Highlights & Insights

### KPI Cards
![KPI and Metrics](visuals/KPI_and_metrics.png) 
> Shows overall base delay rate (~6.6%). Recall-focused threshold ensures nearly all late orders are flagged.

### Confusion Matrix
![Confusion Matrix](visuals/Confusion_matrix.png)
> Captures almost all delayed orders (low FN) at the cost of more false positives — appropriate in logistics risk contexts.

### Delay Probability Distribution
![Distribution of Predicted Delay Probabilities](visuals/Distribution_of_predicted_delay_probabilities.png)
> Visualizes how predictions cluster, highlighting mid-range uncertainty where business rules can intervene.

---

## ⚠️ Limitations & Future Work

- Precision is low due to extreme recall bias — future work will explore **threshold tuning dashboards** in Power BI.  
- Feature importance (e.g., shipping distance, product type) to be visualized for transparency.  
- Deployment as **FastAPI service** for real-time integration with e-commerce systems.  

---

## 🔗 Author

**Ethan Choo**  
📍 Singapore | 🎓 Data Science & Business Analytics Graduate (SIM-UOL)  
🔗 [LinkedIn](https://www.linkedin.com/in/ethanchoo5/) | 🔗 [GitHub](https://github.com/ethan-analytics)
