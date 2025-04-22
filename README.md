# 🧹 Data Cleaning Pipeline - Loan Dataset

This project showcases a simple yet powerful **data cleaning pipeline** built using **Pandas**. It processes a raw loan dataset to handle missing values, fix categorical inconsistencies, and cap outliers — making the data ready for analysis or machine learning tasks.

---

## 📁 Files Included

- `loan_cleaning_pipeline.ipynb`: Main notebook with cleaning logic
- `EDA.ipynb`: Exploratory Data Analysis
- `loan_prediction.csv`: Raw data
- `loan_data_pipeline.csv`: Cleaned output CSV

---

## 🚀 Features

- Handles missing values (mode for categorical, median for numerical)
- Converts `object` types to `category` for optimization
- Strips whitespaces & standardizes text
- Caps outliers at 99th percentile (for income & loan columns)
- Saves cleaned dataset as a new CSV

---

## 🧠 Sample Code

```python
def clean_loan_data(df):
    for col in df.select_dtypes(include="object"):
        df[col] = df[col].fillna(df[col].mode()[0])
        df[col] = df[col].astype('category')
        df[col] = df[col].str.strip().str.lower()

    for col in df.select_dtypes(include=['int', 'float']):
        df[col] = df[col].fillna(df[col].median())

    for col in ['ApplicantIncome', 'CoapplicantIncome', 'LoanAmount']:
        if col in df.columns:
            upper = df[col].quantile(0.99)
            df[col] = df[col].apply(lambda x: upper if x > upper else x)
    
    return df
🔍 Exploratory Data Analysis (EDA)
Check the EDA.ipynb notebook for:

Null value visualization

Distribution plots for numerical features

Count plots for categorical features

Outlier visualizations (before & after cleaning)

📌 Libraries Used
pandas

matplotlib

seaborn

✍️ Author
AshokKumar
25 y/o | Python & Data Enthusiast | On a journey to become a Machine Learning Engineer
