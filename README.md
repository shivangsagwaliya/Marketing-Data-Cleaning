# Marketing Campaign Data Cleaning 🧹

## Overview
This project demonstrates a rigorous data cleaning pipeline designed to transform a raw, "messy" marketing campaign dataset into a clean, analysis-ready format. Using **Python** and **Pandas**, the notebook tackles common real-world data quality issues including inconsistent formatting, typos, logical fallacies, and outliers.

## 📂 The Dataset
The dataset contains 2020 rows of marketing campaign data with the following initial issues:
* **Inconsistent Headers:** Mixed case and spacing.
* **Dirty Currency Data:** 'Spend' column contained symbols ('$') and text, preventing numerical analysis.
* **Categorical Typos:** Channel names like "Facebok", "Gogle", and "Tik_Tok".
* **Mixed Data Types:** Boolean columns containing 'Y', '1', 'True', and 'Yes'.
* **Logical Errors:** Campaign end dates occurring before start dates ("Time Travel").
* **Outliers:** Extreme values in the spending data.

## 🛠️ Technologies Used
* **Python**
* **Pandas** (Data manipulation)
* **NumPy** (Numerical operations)

## ⚙️ Cleaning Pipeline Steps

### 1. Header Standardization
Converted all column headers to snake_case (lowercase with underscores) to ensure consistent programmatic access.

### 2. Currency Conversion & Regex
The `spend` column was stored as strings due to the '$' symbol.
* **Technique:** Used Regex (`[^\\d.-]`) to strip non-numeric characters.
* **Result:** Converted column to `float` for statistical analysis.

### 3. Categorical Standardization (Fuzzy Logic)
The `channel` column contained various misspellings.
* **Technique:** Mapped inconsistent values (e.g., 'Facebok', 'Insta_gram') to standard categories using a dictionary map.

### 4. Boolean Logic Repair
The `active` column contained mixed data types.
* **Technique:** Standardized 'Y', 'Yes', '1' to `True` and 'N', 'No', '0' to `False`.

### 5. Date Parsing & Logical Integrity
* **Parsing:** Converted `start_date` and `end_date` columns to Datetime objects.
* **Logic Check:** Identified rows where `start_date` > `end_date` (Logical Time Travel).
* **Fix:** For invalid rows, calculated a new `end_date` by adding a standard 30-day duration to the `start_date`.

### 6. Outlier Handling (IQR)
Detected anomalies in the `spend` column using the Interquartile Range method.
* **Calculation:** `IQR = Q3 - Q1`.
* **Threshold:** `Upper Bound = Q3 + 1.5 * IQR`.
* **Action:** Capped outliers at the upper bound limit to prevent skewing of downstream analysis.

## 🚀 How to Run
1. Clone the repository.
2. Ensure the `marketing_campaign_data_messy.csv` file is in the root directory.
3. Open `Data Cleaning.ipynb` in Jupyter Notebook or Google Colab.
4. Run all cells to generate the cleaned dataframe.

---
*This project highlights the importance of Data Quality Assurance (QA) prior to exploratory data analysis (EDA).*
