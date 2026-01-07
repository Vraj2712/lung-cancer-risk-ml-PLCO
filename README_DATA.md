
# 📊 PLCO Lung Cancer Dataset — Data Documentation

This project uses data derived from the **Prostate, Lung, Colorectal, and Ovarian (PLCO) Cancer Screening Trial** lung cohort.

⚠️ **Important**
- Original PLCO data **cannot legally be shared**
- This repository contains **only synthetic / sample data**
- All modeling was performed on the officially licensed dataset

---

The dataset used in this project is an **older official PLCO dataset release**. 
A newer PLCO version exists, but it is not used here.


## 📦 Dataset Summary

| Property | Value |
|--------|-------|
| Source | PLCO Cancer Screening Trial (Lung Cohort) |
| File used | `lung_data_nov18_d070819.csv` |
| Participants | **154,887** |
| Positive lung cancer cases | **3,723** |
| Negative cases | **151,164** |
| Positive rate | **2.40%** |
| Total raw variables | **219** |

The dataset contains demographic, smoking history, family history, and clinical questionnaire responses collected at baseline.

---

## 🔐 Data Privacy & Ethics

- Original PLCO data is **restricted-access**
- Not included in this repo
- Only **fake sample CSV** is provided:
  - `data/fake_plco_sample.csv`
- All figures and models were created using the licensed dataset
- No personally identifiable information is used

---

## 🧹 Data Cleaning Pipeline

The cleaning was performed using the notebook:

```

data_cleaning.ipynb

```

### ✔ Steps Performed

1. **Load raw PLCO dataset**
2. **Select final 15 variables** used in the model
3. Convert PLCO missing codes:
   - `.M`, `.N`, `.U`, `.NA`, `NA`, blanks → NaN
4. Convert numeric columns safely
5. Set categorical variables to `category` type
6. Handle missing values:
   - numeric → **median imputation**
   - categorical → **mode imputation**
7. One-hot encode categorical variables
8. Save cleaned dataset:

```

lung_15_variable_cleaned.csv

````

---

## 🧩 Final 15 Variables Used

| Category | Variable | Meaning |
|---------|---------|--------|
| Demographic | age | Participant age |
| Demographic | sex | Male/Female |
| Demographic | race7 | Race category |
| Education | educat | Education level |
| Smoking | cig_stat | Smoking status |
| Smoking | pack_years | Lifetime cigarette exposure |
| Smoking | cig_years | Years smoked |
| Smoking | cigpd_f | Cigarettes per day |
| Smoking | cig_stop | Years since quitting |
| Second-hand | rsmoker_f | Lives with smoker |
| Medical | emphys_f | Emphysema history |
| Medical | bronchit_f | Chronic bronchitis history |
| Medical | bmi_curr | Current BMI |
| Family history | lung_fh | Lung cancer in family |
| Target | lung_cancer | Cancer outcome |

The final prediction model intentionally uses **only 15 easy-to-collect variables**:

age
sex
race7
educat
cig_stat
pack_years
cig_years
cigpd_f
cig_stop
rsmoker_f
emphys_f
bronchit_f
bmi_curr
lung_fh
lung_cancer (target)

After one-hot encoding:

- total columns increase
- all models operate on numeric matrix

---

## ⚖️ Class Imbalance

Lung cancer is rare in screening populations.

- positive rate = **2.40%**
- models would otherwise learn “always predict 0”

### We handled imbalance using:

- `class_weight="balanced"`
- `scale_pos_weight` (XGBoost & LGBM)
- controlled oversampling in some models
- threshold tuning to maximize **F1/Recall**

---

## 🔄 Reproducibility

To regenerate the cleaned file:

```bash
python data_cleaning.ipynb
````

or in Jupyter:

1. Open `data_cleaning.ipynb`
2. Run all cells
3. Output will be:

```
lung_15_variable_cleaned.csv
```

---

## 📌 Notes for Researchers

* PLCO access is available via CDAS approval
* Use of data must follow NIH policy
* This repository is intended for **academic demonstration only**

---

## ✅ Conclusion

This document explains:

* what the dataset is
* how it was processed
* ethical data protection steps
* variables used in modeling

The cleaned dataset enables development of:

👉 interpretable
👉 clinically relevant
👉 high-recall lung cancer risk prediction models

```

---


