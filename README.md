# Delivery Delay Prediction Pipeline (AWS + Power BI)

End-to-end project predicting late deliveries on the Olist e-commerce dataset. Data is ingested and prepared on AWS (S3, Glue, Athena), modeled with XGBoost, and visualized in Power BI for business storytelling.

---

## Executive Summary

- Processed 5M+ transactions with AWS S3 + Glue + Athena.
- Trained an XGBoost classifier with class-imbalance handling and a decision threshold of **0.25** to prioritize recall.
- **Results:** Base delay rate ≈ **6.6%**, **Recall ≈ 99%**, **Precision ≈ 6.7%**.
- Delivered a compact Power BI dashboard (KPI cards, confusion matrix, probability distribution).

---

## Tech Stack

| Layer | Tools |
|------|------|
| Data | AWS S3, AWS Glue (PySpark), AWS Athena (SQL) |
| ML   | XGBoost (SageMaker/Notebook), threshold tuning, imbalance handling |
| Viz  | Power BI (KPI cards, confusion matrix, histogram) |
| Ops  | (Optional) FastAPI endpoint, AWS Step Functions, QuickSight |

---

## Project Structure

/aws_pipeline
  ├── glue_jobs/            # Glue scripts for raw → curated tables
  ├── athena_queries/       # SQL queries to explore and prepare data
/model
  ├── model_training.ipynb  # Notebook: feature engineering, model training, export
  └── feature_importance.csv
/powerbi
  ├── README.md             # Dashboard walkthrough
  └── visuals/              # Images of Confusion Matrix, Histogram, KPI cards


---

## Visual Highlights & Insights

### KPI Cards
![KPI and Metrics](visuals/KPI_and_metrics.png)

**Interpretation:** Base delay rate is ~6.6%. At threshold 0.25 the model emphasizes **recall (~99%)** to avoid missing delayed orders, with expected low precision (~6.7%).

### Confusion Matrix
![Confusion Matrix](visuals/Confusion_matrix.png)

High recall means we capture almost all delayed orders (few FN) but raise many false positives—appropriate when the cost of a missed delay is high.

### Delay-Probability Histogram
![Distribution of Predicted Delay Probabilities](visuals/Distribution_of_predicted_delay_probabilities.png)

Shows how predicted probabilities cluster (e.g., around 0.45–0.55) and how actual delays distribute across bins.

---

## Results

| Metric        | Value  |
|---------------|--------|
| Base Rate     | ~6.6%  |
| Recall (t=0.25)   | ~99%  |
| Precision (t=0.25)| ~6.7% |
| AUC           | ~0.585 |

**Business take:** Use the model as an *early-warning* system. Investigate high-risk orders and apply operational mitigations (expedite, notify customer, prioritize packing).

---

## Future Work

- Add **Feature Importance** bar chart (export `feature_importance.csv` from notebook).
- Add a **What-If** threshold slider in Power BI to show precision/recall trade-offs.
- Package model behind a **FastAPI** endpoint for batch/real-time scoring.

---

## Author

**Ethan Choo** — Singapore  
Data Science & Business Analytics (SIM–UOL)  
LinkedIn: https://www.linkedin.com/in/ethanchoo5

