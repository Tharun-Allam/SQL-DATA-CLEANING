# SQL Data Cleaning Project – Layoffs Dataset

This project demonstrates a complete end-to-end **SQL data cleaning workflow** using a real-world dataset containing global tech layoffs from 2020–2023.

The goal of this project is to transform the raw dataset into a clean, analysis-ready table by applying SQL data-cleaning techniques including:
- Removing duplicates  
- Standardizing inconsistent values  
- Handling NULLs and blank fields  
- Date formatting and conversion  
- Removing unusable rows  

---

##  Project Overview

The project uses MySQL to clean the `layoffs` dataset.  
The cleaning process is divided into the following steps:

### **Remove Duplicates**
- Created a staging table (`layoffs_staging`)  
- Used `ROW_NUMBER()` + PARTITION to identify duplicates  
- Deleted all rows with `row_num > 1`  

### **Standardize Data**
Applied consistent formatting for:
- Company names (using `TRIM()`)  
- Industry values (mapping variations like “Crypto & Web3” → “Crypto”)  
- Country names (e.g., removing trailing periods in “United States.”)  
- Converted date strings (`mm/dd/yyyy`) into valid `DATE` format  

### **Handle NULL Values & Empty Fields**
- Replaced blank fields with NULL  
- Filled missing industries by matching companies with known industry values  
- Removed rows where *both* total_laid_off and percentage_laid_off were NULL  

### **final Cleanup**
- Dropped helper columns  
- Produced a clean final dataset in `layoffs_staging2`

---

## Project Files

| File | Description |
|------|-------------|
| **sql-data-cleaning-project.sql** | Full SQL script containing all data-cleaning steps |
| **layoffs.csv** | Raw dataset used in the project |

---

## Technologies Used
- **MySQL 8+**
- SQL Window Functions  
- CTE (Common Table Expressions)  
- Data Standardization  
- Data Transformation & Cleaning  

---

## Example SQL Used

```sql
WITH duplicate_cte AS (
    SELECT *,
    ROW_NUMBER() OVER(
        PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised_millions
    ) AS row_num
    FROM layoffs_staging
)
DELETE FROM duplicate_cte
WHERE row_num > 1;
```

---

## Key Learnings
- How to design a full SQL cleaning pipeline  
- Removing duplicates using window functions  
- Fixing formatting issues with string functions  
- Correcting NULL values and filling missing data  
- Converting inconsistent date formats  
- Preparing data for further analytics  

---

##  Author
**Your Name**  
SQL Enthusiast | Data Analyst | Python & SQL Learner  

---

##  Contribute
Feel free to fork this repository and contribute improvements or more cleaning techniques!

