# 📊 Exploratory Data Analysis (EDA) in Databricks with Spark SQL

This guide shows how to perform EDA in **Databricks** using **Spark SQL** queries.  Part of those steps were done on the JSON  files  loaded in Databricks.
We first register a DataFrame as a SQL temporary view, then run SQL commands.

---

## 1. Load the Data & Register as SQL View
```python
df = spark.read.csv("/mnt/data/myfile.csv", header=True, inferSchema=True)
df.createOrReplaceTempView("mytable")
````
Or use the +New Data interface to upload new JSON files

---

## 2. Inspect Schema & Preview Data

```sql
DESCRIBE TABLE mytable;
```

```sql
SELECT * FROM mytable LIMIT 5;
```

```sql
SELECT COUNT(*) AS total_rows FROM mytable;
```

---

## 3. Check for Missing Values

```sql
SELECT
  COUNT(*) AS total_rows,
  SUM(CASE WHEN col1 IS NULL THEN 1 ELSE 0 END) AS col1_missing,
  SUM(CASE WHEN col2 IS NULL THEN 1 ELSE 0 END) AS col2_missing
FROM mytable;
```

---

## 4. Descriptive Statistics

```sql
SELECT
  MIN(numeric_col) AS min_val,
  MAX(numeric_col) AS max_val,
  AVG(numeric_col) AS mean_val,
  PERCENTILE(numeric_col, 0.25) AS q1,
  PERCENTILE(numeric_col, 0.50) AS median,
  PERCENTILE(numeric_col, 0.75) AS q3
FROM mytable;
```

---

## 5. Categorical Value Distribution

```sql
SELECT category_col, COUNT(*) AS count
FROM mytable
GROUP BY category_col
ORDER BY count DESC;
```

---

## 6. Detect Duplicates

```sql
SELECT *, COUNT(*) AS dup_count
FROM mytable
GROUP BY col1, col2, col3  -- list all columns if needed
HAVING COUNT(*) > 1;
```

---

## 7. Univariate Distributions (with Databricks Visualizations)

```sql
SELECT numeric_col
FROM mytable;
```

➡️ In Databricks: click **Plot Options** → choose **Histogram**.

---

## 8. Correlations & Crosstabs

```sql
-- Crosstab of two categorical variables
SELECT cat_col1, cat_col2, COUNT(*) AS count
FROM mytable
GROUP BY cat_col1, cat_col2;
```

```sql
-- Correlation approximation (requires numeric cols)
SELECT corr(col1, col2) AS correlation
FROM mytable;
```

---

## 9. Outlier Detection (IQR method)

```sql
WITH stats AS (
  SELECT
    PERCENTILE(numeric_col, 0.25) AS q1,
    PERCENTILE(numeric_col, 0.75) AS q3
  FROM mytable
)
SELECT t.*
FROM mytable t, stats s
WHERE t.numeric_col < s.q1 - 1.5*(s.q3 - s.q1)
   OR t.numeric_col > s.q3 + 1.5*(s.q3 - s.q1);
```

---

## 10. Document Insights

Use **Markdown cells** in your Databricks notebook to summarize:

* Data structure & types
* Missing values
* Key distributions
* Outliers
* Correlations and anomalies

---

## ✅ Workflow Recap

1. Load Data & Register SQL View
2. Inspect Schema & Row Counts
3. Null Value Analysis
4. Descriptive Stats & Percentiles
5. Category Distributions
6. Duplicates Check
7. Visualizations (Histograms, Boxplots)
8. Correlations & Crosstabs
9. Outlier Detection
10. Document Insights

---
