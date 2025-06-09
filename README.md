# 📊 Exploratory Data Analysis (EDA) of Tech Layoffs using SQL

This repository contains a structured exploratory data analysis (EDA) of the **tech layoffs dataset** using **SQL queries**. The dataset is sourced from the `world_layoffs.layoffs_staging2` table and provides insights into global layoffs in the technology sector over the past few years.

---

## 🗂️ Project Structure

The SQL file provided in this repository explores the dataset in stages, progressing from basic descriptive statistics to more advanced analytical queries using aggregate functions and window functions.

---

## 🔍 Objectives

- Understand the magnitude and distribution of tech layoffs across companies, industries, countries, and years.
- Identify significant events and patterns (e.g., companies that shut down completely, high layoff percentages, peaks over time).
- Build foundations for potential dashboards or predictive modeling.

---

## 🛠️ Tools Used

- SQL (MySQL or PostgreSQL compatible syntax)
- Structured Query Language features such as:
  - Aggregation (`SUM`, `MAX`, `MIN`)
  - Filtering (`WHERE`)
  - Sorting and limiting (`ORDER BY`, `LIMIT`)
  - Grouping (`GROUP BY`)
  - Window functions (`DENSE_RANK`, `OVER()`)
  - Common Table Expressions (CTEs)

---

## 📌 Key Analyses Performed

### 1. 🧹 Initial Exploration
- Viewing the entire dataset
- Identifying companies with 100% layoffs (indicative of closure)
- Sorting companies by the amount of funds raised

### 2. 📈 Descriptive Statistics
- Maximum and minimum values of `percentage_laid_off` and `total_laid_off`
- Companies with the highest single-day layoffs
- Top companies with cumulative layoffs

### 3. 🗺️ Aggregated Insights
- Total layoffs by:
  - **Company**
  - **Location**
  - **Country**
  - **Year**
  - **Industry**
  - **Funding stage**

### 4. 🏆 Advanced Queries
- **Yearly Top 3 Companies** with the highest layoffs using `DENSE_RANK`
- **Rolling Monthly Layoffs** using window functions to compute cumulative trends

---

## 📊 Sample Query Snippet

```sql
WITH DATE_CTE AS 
(
  SELECT SUBSTRING(date, 1, 7) AS dates, SUM(total_laid_off) AS total_laid_off
  FROM layoffs_staging2
  GROUP BY dates
)
SELECT dates, SUM(total_laid_off) OVER (ORDER BY dates ASC) AS rolling_total_layoffs
FROM DATE_CTE;
