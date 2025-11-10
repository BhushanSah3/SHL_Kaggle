# SHL_Kaggle

# Grammar Scoring Engine — SHL Internship Assessment (Bhushan Sah)

**Notebook Purpose:**
This notebook represents my **merged and final version** of both development files —
`Untitled1.ipynb` and `Final.ipynb`.
It contains the **complete pipeline** that produces the same final output and score of **0.874 RMSE** on the leaderboard.
The entire end-to-end process — from preprocessing to model training and submission file generation — has been consolidated and verified to work independently on Kaggle.

---

## ⚙️ Notebook Execution Instructions

1. **Run all cells sequentially (top to bottom).**

   * The dataset folder `bhushan-shl-features` (uploaded as a Kaggle Dataset) contains all required intermediate CSVs, precomputed embeddings, and feature files.
   * The notebook automatically detects these files, so heavy preprocessing (e.g., Whisper transcription, LM/GEC feature extraction) is **skipped** by default for fast execution.
   * The final retrain and evaluation cells will reproduce my leaderboard submission results.

2. **If, for any reason, the notebook does not execute completely on Kaggle**,
   please refer to the two original files I have also provided:

   * `Untitled1.ipynb` → performs the complete preprocessing, ASR transcription, LM+GEC feature enrichment, and LightGBM model training.
   * `Final.ipynb` → performs the audit, leakage cleaning, safe retraining, and final submission reconstruction.

   Run them sequentially:
   1️⃣ Untitled1.ipynb
   2️⃣ Final.ipynb

This will produce the same final submission file and RMSE results.

---

## 🧠 Methodology Overview

### 1. Data Preprocessing

* Loaded train/test audio samples and feature metadata.
* Generated ASR transcripts using **OpenAI Whisper (small)** model.
* Extracted **acoustic features** (RMS, ZCR, pauses, etc.) and **textual features** (word count, grammar errors, TTR, etc.).
* Combined both into a unified `features_with_transcripts.csv`.

### 2. Language Model and Grammar Enrichment

* Computed **LM perplexity** and **loss scores** using `distilGPT2`.
* Detected grammar edits using `language_tool_python`.
* Derived normalized metrics such as `lt_edit_ratio_chars` and `ppl_distilgpt2`.

### 3. Feature Cleaning and Leakage Prevention

* Removed label-like or prediction-like columns (`label_x`, `label_y`, `oof_preds`, `split`, etc.).
* Imputed missing numeric values using median.
* Saved a clean reproducible feature list.

### 4. Model Training

* Trained **LightGBM regressors** using 5-fold CV (`n_estimators=2000`, `learning_rate=0.05`, `num_leaves=31`).
* Evaluated model performance using **RMSE** and **Pearson correlation**.
* Achieved **OOF RMSE = 0.7261** and **Leaderboard RMSE = 0.874**.

### 5. Submission Construction

* Retrained final models on all labeled data.
* Neutralized overlapping filenames between train and test (if any).
* Averaged predictions from 5 folds and clipped values to [0, 5].
* Saved as `submission_no_lookup_retrained.csv` (final competition submission).

---

## 📊 Evaluation Summary

|        Metric        | Type        | Description                                             |
| :------------------: | :---------- | :------------------------------------------------------ |
|    **RMSE (OOF)**    | Training    | Root Mean Square Error from 5-fold CV                   |
|      **Pearson**     | Training    | Correlation between true & predicted scores             |
| **Leaderboard RMSE** | Public Test | Final Kaggle score = **0.874**                          |
|  **Visualizations**  | -           | Scatter plots, residual histograms, feature importances |

---

## 📁 Output Files Produced

All generated in `/kaggle/working/bhushan_shl_outputs/audit_outputs`:

* `run_report_final.json` — OOF RMSE and Pearson
* `oof_lgb_final.csv` — OOF predictions
* `feature_importance_top20.png` — interpretability chart
* `submission_no_lookup_retrained.csv` — final competition submission
* `submission_final_for_kaggle.csv` — validated ready-for-upload file

---

### ✅ This notebook contains:

* Clean, documented, and reproducible code
* Required OOF RMSE printed inline
* Interpretability plots and feature importance chart
* Comments explaining all key processing stages
* Final submission verified for correct format and range

---

# ============================================================

# GRAMMAR SCORING ENGINE — FINAL MERGED NOTEBOOK

# ============================================================

# Author: Bhushan Sah

# Competition: SHL Internship Assessment 2025

#

# NOTE TO REVIEWER:

# ------------------------------------------------------------

# This is my *merged* and final version combining both:

# - Untitled1.ipynb  (Main modeling & feature generation)

# - Final.ipynb      (Audit, leakage cleaning & retrain)

#

# It is fully self-contained and executable in Kaggle.

# All required data (preprocessed CSVs, features, models)

# are already included in my uploaded dataset:

# bhushan-shl-features

#

# If, for any reason, the notebook does not execute

# completely, please refer to my original files:

# 1️⃣  Untitled1.ipynb

# 2️⃣  Final.ipynb

# and run them sequentially. They produce the same results

# and final submission file: submission_no_lookup_retrained.csv

#

# Achieved Score on Leaderboard: RMSE = 0.874

# ------------------------------------------------------------

# The notebook also prints OOF RMSE, Pearson correlation,

# and includes required interpretability plots.

# ============================================================

# 🏁 Final Notes and Reproducibility Summary

This notebook successfully reproduces the final submission results of my Grammar Scoring Engine project for SHL’s Research Intern Assessment.

✅ **OOF RMSE and Pearson** are printed in the cell labeled *“A: Print compulsory OOF RMSE & Pearson”*.
✅ **Visual Interpretability** is provided in the *Visualizations* section (scatter plot, residual histogram, top-20 feature importance).
✅ **Final Submission File** is verified in the *Submission Verification* section (`submission_final_for_kaggle.csv`).
✅ All outputs are saved under `/kaggle/working/bhushan_shl_outputs/audit_outputs`.

In case of any execution issues, please refer to the original notebooks included:
1️⃣ Untitled1.ipynb
2️⃣ Final.ipynb

Running them sequentially produces identical final predictions and the same leaderboard score of **0.874 RMSE**.

Thank you for reviewing this submission.

**— Bhushan Sah**
Final Year, B.Tech CSE
Kalinga Institute of Industrial Technology

---

**Score achieved:** ✅ **RMSE = 0.874 (Leaderboard)**
**Author:** Bhushan Sah
**Institution:** Kalinga Institute of Industrial Technology
**Position Applied:** SHL Research Intern
-----------------------------------------
