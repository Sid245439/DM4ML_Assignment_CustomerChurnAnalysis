# PROJECT OVERVIEW – Customer‑Churn Prediction Pipeline
**Group:** 34  
**Course:** Data Management for Machine Learning – Assignment I  
**Date:** 23 Aug 2025  

## 1. Business Problem
Customer churn is the loss of a paying subscriber before the end of the contract.  
Our startup must **predict addressable churn** (customers who could be retained with an intervention) so that the marketing team can target retention offers proactively.

## 2. Business Objectives
| Objective | KPI | Target |
|----------|-----|--------|
| Reduce addressable churn | % churn reduction (offline test) | **≥ 12 %** in 6 months |
| Increase revenue retention | Net‑revenue‑retention (NRR) | **≥ 95 %** |
| Provide reusable pipeline | Time‑to‑model (from data arrival to model) | **≤ 30 min** |

## 3. Data Sources
| Source | Storage type | Key attributes |
|--------|--------------|----------------|
| Web logs (clickstream) | CSV / JSON in S3 (`raw/web_logs/`) | `customer_id`, `timestamp`, `page_id`, `event_type` |
| Transactional DB | PostgreSQL (`transactions` table) | `transaction_id`, `customer_id`, `amount`, `transaction_ts` |
| CRM third‑party API | REST endpoint (`/customers`) | `customer_id`, `gender`, `tenure`, `contract`, `payment_method`, `Churn` |

## 4. Pipeline Outputs
- **Clean datasets** (CSV/Parquet) for EDA – stored in `data/clean/`.
- **Feature table** (`churn_features`) stored in a feature store (Feast) and also in a relational DB.
- **Deployable model** (`churn_model.pkl`) versioned with MLflow.

## 5. Evaluation Metrics
- Primary: **Recall** & **F1‑score** for the churn = 1 class (addressable churn is the minority).
- Secondary: **AUC‑ROC**, **Precision**, **Lift@10 %** (business impact).
- Operational: **Pipeline runtime** < 30 min, **Data‑quality failure rate** < 5 %.

## 6. Success Criteria
- End‑to‑end run (Ingestion → Model) completes without manual intervention.
- Model meets **F1 ≥ 0.75** on a held‑out test set.
- All artefacts (raw, clean, feature, model) are versioned in DVC/MLflow.

---

*All the subsequent sections of the repository implement the design described above.*