# data-screening-exercise
Data cleaning and analysis for ICE detention centers.


# 🧊 ICE Detention Data Cleaning and Visualization Project

## 📁 Project Overview

This project involves cleaning and analyzing a messy ICE detention center dataset. The primary goals were:

- Clean and standardize facility names and columns.
- Correct typos and inconsistencies.
- Convert Excel-style dates to readable format.
- Handle missing values transparently.
- Visualize the top 10 facilities by total population.
- Document manual corrections and AI usage.

---

## 📂 Files Included

| File Name | Description |
|-----------|-------------|
| `messy_ice_detention.csv` | Raw dataset (initial state, uncleaned) |
| `ice_cleaning_script.R` | R script used for data cleaning, transformation, and visualization |
| `cleaned_ice_detention_data.csv` | Final cleaned version of the dataset |
| `top_10_detention_facilities.png` | Bar chart showing top 10 facilities by total population |
| `README.md` | Project documentation |
| `Prompt_Details.txt` | AI prompt and explanation of how LLM was used |
| `manual_corrections_log.txt` | Explanation of manual corrections made using online sources |

---

## 📊 Data Cleaning and Transformation Summary

### ✅ Cleaned Elements:

- Standardized column names using `janitor::make_clean_names()`.
- Removed unwanted characters from `name` column using `stringr`.
- Fixed common typos such as:
  - `ALEXASNDRIA` → `ALEXANDRIA`
  - `ALLLEN` → `ALLEN`
- Converted population fields to numeric and created a `Total_Population` column.
- Converted Excel serial numbers in `last_inspection_end_date` into readable `Date` format using `as.Date()`.

### 📉 Missing Values:
- Missing `last_inspection_end_date` values were **preserved as NA** for data integrity and to support descriptive statistics or quality control analysis.

---

## 🛠️ Manual Data Correction

Some entries lacked names despite having valid city information. These were looked up manually due to a lack of reliable pattern-matching.

| City | Corrected Name | Source |
|------|----------------|--------|
| DOVER | DOVER ICE FIELD OFFICE | Google Search / ICE Office Directory |
| ELK RIVER | SHERBURNE COUNTY JAIL | ICE Detention Center List |

**Code Used**:
```r
data$name[is.na(data$name) & data$city == "DOVER"] <- "DOVER ICE FIELD OFFICE"
data$name[is.na(data$name) & data$city == "ELK RIVER"] <- "SHERBURNE COUNTY JAIL"
