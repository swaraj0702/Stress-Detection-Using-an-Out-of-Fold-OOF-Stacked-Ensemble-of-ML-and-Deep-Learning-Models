# Stress Detection Using OOF-Stacked Ensemble of ML and Deep Learning

## Overview
This project presents a robust **stress detection system** using an **Out-of-Fold (OOF) stacked ensemble** that combines traditional machine learning and deep learning models.  
The approach is designed to eliminate data leakage, improve generalization, and provide confidence-aware stress predictions.

The system classifies stress into:
- **Non-Stress**
- **Moderate Stress**
- **High Stress**

---

## Key Contributions (Novelty)
- ✔ Out-of-Fold (OOF) stacking to prevent data leakage
- ✔ Hybrid ensemble of **ML + DL models**
- ✔ LightGBM used as an **interpretable meta-learner**
- ✔ Confidence-based **risk level assessment**
- ✔ Model agreement analysis for explainability

This design makes the project suitable for **M.Tech dissertation and conference publication**.

---

## Models Used

### Base Models
- **LightGBM** – Tabular physiological feature learning  
- **CNN** – Temporal pattern extraction  
- **LSTM** – Sequential dependency modeling  
- **BiLSTM** – Bidirectional temporal learning  

### Meta-Learner
- **LightGBM (shallow & interpretable)** trained on OOF predictions

---

## OOF Stacking Strategy
1. Stratified K-Fold cross-validation is applied.
2. Each base model is trained on `(k-1)` folds.
3. Predictions are generated on the unseen fold (**Out-of-Fold**).
4. OOF predictions from all models are concatenated.
5. A LightGBM meta-learner is trained on these OOF features.
6. Final predictions are generated without data leakage.

---

## Dataset Description
The dataset consists of **physiological features** derived from:
- Heart Rate (HR)
- Electrodermal Activity (EDA)
- Temperature (TEMP)

Features include statistical summaries such as mean, standard deviation, RMS, min, and max.

> ⚠ Raw sensor data is not shared for privacy reasons. Only processed features are used.

---

## Final Output (Cell 11)
For each input sample, the system produces:

- **Final Stress Label**
- **Prediction Confidence**
- **Risk Level** (Low / Elevated / Critical)
- **Model Agreement Report**
- **Decision Source** (OOF Stacked Meta-Learner)

Example output:
```json
{
  "Final_Stress_Label": "High Stress",
  "Confidence": 0.969,
  "Risk_Level": "Critical",
  "Model_Agreement": {
    "LightGBM": "High Stress",
    "CNN": "High Stress",
    "LSTM": "Moderate Stress",
    "BiLSTM": "High Stress"
  },
  "Decision_Source": "OOF Stacked Meta-Learner"
}
