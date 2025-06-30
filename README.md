# layoffs-since-covid-sql
This project focuses on cleaning and exploring a dataset that tracks global tech layoffs starting from the declaration of COVID-19 as a pandemic. The project transforms raw data into a clean, structured format and performs exploratory data analysis (EDA) to identify key patterns and insights.

**Tools Used:** SQL (MySQL)  
**Status:** Completed  
**Dataset Source:** https://www.kaggle.com/datasets/swaptr/layoffs-2022

## Data Cleaning Steps

The raw dataset was transformed using a series of SQL operations:

1. **Removed duplicates**  
   - Used `ROW_NUMBER()` with `PARTITION BY` to detect repeated rows
2. **Standardized textual fields**  
   - Trimmed extra whitespace  
   - Unified inconsistent industry and country names (e.g., fixing “Cyrpto Currency” to “Crypto”)
3. **Converted dates**  
   - Used `STR_TO_DATE()` to change text to `DATE` type
4. **Handled null and blank values**  
   - Imputed missing values using related rows when possible
   - Removed rows with no usable information
5. **Dropped unnecessary columns**  
   - Removed temporary `row_num` column used for de-duplication

## Exploratory Data Analysis

Several SQL queries were used to extract trends and insights:

- **Layoffs over time**  
  - Monthly and annual totals  
  - Rolling cumulative layoffs using `SUM() OVER`
- **By company and country**  
  - Top companies by total layoffs  
  - Countries with the most impact
- **By industry and funding stage**  
  - Which industries and business stages saw the most layoffs
- **Extreme cases**  
  - Companies that laid off 100% of their workforce

## Key Insights

- Layoffs peaked in specific months and showed waves over the years
- Certain companies like [example: "Meta", "Google", "Airbnb"] consistently appeared in top yearly layoff counts
- Some startups with large funding rounds still laid off their entire workforce
- Country-wise and stage-wise aggregations revealed which geographies and business models were most vulnerable

## Sample SQL Features Used

```sql
-- Ranking duplicate entries
ROW_NUMBER() OVER (PARTITION BY ...)

-- Cumulative trends over time
SUM(total_laid_off) OVER (ORDER BY month)

-- Filtering and standardization
TRIM(), STR_TO_DATE(), LIKE

-- Grouped aggregations
GROUP BY company, year, industry, country
