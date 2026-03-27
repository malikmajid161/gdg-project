# 🎓 Student Performance Analysis & Prediction
### GDGoC COMSATS WAH — DECODE: Data Science Bootcamp 2026

---

## 📌 Project Overview

This project applies a complete Data Science pipeline on a messy student dataset to analyze and predict final exam scores using Linear Regression. The dataset contains **205 rows and 14 columns** with real-world data quality issues that were cleaned and processed before modeling.

---

## 📁 Dataset

| Column | Type | Description |
|--------|------|-------------|
| Student_ID | Numerical | Unique ID — dropped before modeling |
| Name | Text | Student name — casing issues fixed |
| Age | Numerical | Student age — wrong dtype fixed |
| Gender | Categorical | Male/Female — casing standardized |
| City | Categorical | Student city |
| Department | Categorical | CS / EE / ME / BBA / SE |
| Education_Level | Categorical | Intermediate / Bachelors / Masters |
| Attendance_% | Numerical | Attendance percentage |
| Study_Hours_Daily | Numerical | Daily study hours |
| Assignments | Numerical | Assignment score out of 10 |
| Quizzes | Numerical | Quiz score out of 20 |
| Midterm | Numerical | Midterm score |
| Internet_Access | Categorical | Yes / No |
| Final_Score | Numerical | **TARGET — what we predict** |

---

## 🔧 Pipeline Steps

### Step 1 — Data Loading
- Loaded dataset using `pd.read_excel()`
- Checked shape, dtypes, missing values, head/tail, describe

### Step 2 — Data Cleaning
Fixed all 7 problems in the dataset:
- ✅ Gender casing → `.str.title()`
- ✅ Name casing → `.str.title()`
- ✅ Department inconsistencies → `.str.upper().str.strip()`
- ✅ Age wrong dtype → `pd.to_numeric(errors='coerce')` + median fill
- ✅ Impossible Attendance values → replaced with NaN
- ✅ Impossible Final_Score values → replaced with NaN
- ✅ Missing values → filled with **median** (robust to outliers)
- ✅ Duplicate rows → removed with `drop_duplicates()`

### Step 3 — EDA + Visualization
7 charts with written interpretations:
1. Distribution of Final_Score (histplot)
2. Attendance % vs Final_Score (scatter)
3. Study Hours vs Final_Score (scatter)
4. Midterm vs Final_Score (scatter)
5. Correlation Heatmap
6. Final_Score by Department (boxplot)
7. Students per Department (countplot)

### Step 4 — Feature Engineering + Pipeline
New features created:
- `Total_Academic` = Midterm + Assignments×5 + Quizzes×2
- `Attendance_Category` = Low / Medium / High (binned)
- `Study_Efficiency` = Study_Hours × (Attendance / 100)

Encoding decisions:
- **OneHot** → Gender, Internet_Access, City, Department (no order)
- **Ordinal** → Education_Level, Attendance_Category (order exists)
- **StandardScaler** → all numerical columns

### Step 5 — Model + Evaluation
- Model: **Linear Regression** via sklearn Pipeline
- Train/Test Split: 80/20, random_state=42

---

## 📊 Results

| Metric | Value |
|--------|-------|
| MAE | ~2.45 |
| RMSE | ~3.27 |
| R² | ~0.59 |

> The model explains **59% of the variation** in Final_Score. The strongest predictor was **Midterm score**, followed by the engineered **Total_Academic** feature.

---

## 🚀 What I Would Improve

1. Try **Random Forest / XGBoost** to capture non-linear patterns
2. Collect more data — 200 rows is small for ML
3. Add stronger features like previous GPA or assignment submission rate

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.0-green)
![Sklearn](https://img.shields.io/badge/Scikit--Learn-1.3-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-0.12-red)

- Python 3.10
- Pandas, NumPy
- Scikit-learn (Pipeline, ColumnTransformer, LinearRegression)
- Matplotlib, Seaborn
- Google Colab

---

## 📂 How to Run

1. Clone this repo
```bash
git clone https://github.com/your-username/student-performance-prediction
```

2. Upload notebook to Google Colab

3. Upload dataset to Google Drive at:
```
/content/drive/MyDrive/gdg project/student_performance_dataset.xlsx
```

4. Run all cells top to bottom

---

## 👤 Author

**Muhammad MAjid Ali**
COMSATS University Islamabad, Wah Campus
GDGoC DECODE Data Science Bootcamp 2026
