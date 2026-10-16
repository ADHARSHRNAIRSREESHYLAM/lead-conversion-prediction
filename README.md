# Lead Conversion Predictive Modeling & Prioritization

An end-to-end Machine Learning pipeline to predict customer lead conversions, rank active prospects, and optimize sales outreach using historical CRM data.

---

## 🚀 Project Overview

Sales teams often waste time pursuing cold leads while high-intent prospects experience delayed follow-ups. Using a **Random Forest Classifier** on **27,375 lead records**, this project computes continuous conversion probabilities ($P \in [0, 1]$) to prioritize 14,832 active prospects automatically.

---

## 🎯 Project Objectives

- **Conversion Prediction:** Train a machine learning model to evaluate historical patterns and predict the probability ($P \in [0, 1]$) of a lead successfully converting.
- **Automated Lead Triaging:** Generate an automated, ranked priority list for active leads in the `Prospect` and `Follow Up Required` stages.
- **Resource Optimization:** Reallocate executive bandwidth and marketing budgets toward high-performing acquisition channels and campaigns.

---

## 🛠️ Data Pipeline & Preprocessing

1. **Leakage Prevention:** Removed post-call timestamps (`creation_date`, `first_call_attempt`, `last_call_date`, `last_call_time`) and identifiers (`Name`, `contact_number`, `Contact_email`, `references`).
2. **Missing Values:** Imputed 11,416 missing entries in `lead_tag` with `'Do Not Know'`[cite: 1].
3. **Encoding & Scaling:** Applied `LabelEncoder` on categorical fields and standardized inputs with `StandardScaler`.
4. **Data Split:** 70% Training ($19,162$ rows) / 30% Testing ($8,213$ rows).

---

## 🤖 Model Architecture

- **Random Forest Classifier:** Uses an ensemble of 100 decision trees to capture complex, non-linear interactions across marketing channels and lead metadata without overfitting.
- **Probabilistic Scoring:** Outputs continuous probabilities rather than hard binary outputs, allowing dynamic lead sorting and customizable priority thresholds.
- **Handling Class Imbalance:** Maintains a solid **76% recall rate** on the converted minority class, minimizing the loss of viable business opportunities.

---

## 📊 Performance Summary

| Metric | Value |
| :--- | :--- |
| **Overall Accuracy** | **98.49%** |
| **ROC-AUC Score** | **84.73%** |
| **Macro Average F1-Score** | **0.86** |
| **Converted Lead Recall (Class 1)** | **76%** |

### Confusion Matrix

- **True Negatives:** 7,920 | **False Positives:** 52
- **False Negatives:** 72 | **True Positives:** 169

---

## 📈 Lead Triaging & Action Plan

- **Tier 1 (P ≥ 0.50):** High-priority immediate calls by top closers (probabilities up to 83.8%)[cite: 1].
- **Tier 2 (0.20 ≤ P < 0.50):** Follow-ups via email/WhatsApp within 24 hours.
- **Tier 3 (P < 0.20):** Automated drip campaigns and ad retargeting.

---

## 🎯 Conclusion

The Random Forest model effectively replaces manual guesswork with data-driven prioritization, enabling sales teams to focus resources on top-tier prospects and maximize conversion rates.

### Future Scope
- Test gradient boosting algorithms (XGBoost, LightGBM).
- Address class imbalance using SMOTE or custom loss weights.
- Integrate directly with CRM webhooks for real-time lead scoring.

---

## ⚙️ Quick Start

```bash
# Clone repository
git clone [https://github.com/your-username/lead-conversion-prediction.git](https://github.com/your-username/lead-conversion-prediction.git)
cd lead-conversion-prediction

# Install dependencies & run pipeline
pip install -r requirements.txt
python src/train_model.py
