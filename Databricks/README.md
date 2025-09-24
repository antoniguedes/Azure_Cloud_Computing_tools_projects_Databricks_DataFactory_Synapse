# 🚀 Exploratory Data Analysis (EDA) in Databricks Spark Notebook

This guide provides a structured process to perform **Exploratory Data Analysis (EDA)** using **PySpark** inside a Databricks notebook. It includes steps, code snippets, and best practices for large-scale data exploration.

---

## 📌 Steps of EDA

### 1. Load the Data
```python
# Load CSV
df = spark.read.csv("/mnt/data/myfile.csv", header=True, inferSchema=True)

# Or load Parquet
df = spark.read.parquet("/mnt/data/myparquet/")
````

---

### 2. Inspect Schema & Basic Info

```python
df.printSchema()
df.show(5)
df.count()
```

---

### 3. Missing Values

```python
from pyspark.sql.functions import col, sum

df.select([sum(col(c).isNull().cast("int")).alias(c) for c in df.columns]).show()
```

---

### 4. Descriptive Statistics

```python
# Summary stats
df.describe().show()

# Quantiles
df.approxQuantile("column_name", [0.25, 0.5, 0.75], 0.05)
```

---

### 5. Categorical Distributions

```python
df.groupBy("category_col").count().orderBy("count", ascending=False).show()
```

---

### 6. Detect Duplicates

```python
df.groupBy(df.columns).count().filter("count > 1").show()
```

---

### 7. Univariate Visualizations

```python
import seaborn as sns
import matplotlib.pyplot as plt

pdf = df.sample(fraction=0.01, seed=42).toPandas()
sns.histplot(pdf["numeric_col"], bins=30)
plt.show()
```

---

### 8. Correlations & Crosstabs

```python
# Correlation matrix
from pyspark.ml.stat import Correlation
from pyspark.ml.feature import VectorAssembler

num_cols = ["col1", "col2", "col3"]
vec_assembler = VectorAssembler(inputCols=num_cols, outputCol="features")
df_vec = vec_assembler.transform(df)
Correlation.corr(df_vec, "features").head()
```

```python
# Crosstab
df.crosstab("cat_col1", "cat_col2").show()
```

---

### 9. Outlier Detection

```python
q1, q3 = df.approxQuantile("numeric_col", [0.25, 0.75], 0.05)
iqr = q3 - q1
lower, upper = q1 - 1.5*iqr, q3 + 1.5*iqr

df.filter((col("numeric_col") < lower) | (col("numeric_col") > upper)).show()
```

---

### 10. Document Insights

Use **Markdown cells** in Databricks to record:

* Summary statistics
* Missing values
* Outliers
* Correlations
* Data quality issues

---

## ✅ Best Practices

* Use **Copy mode** when sampling small subsets for quick visualization.
* Always document anomalies and assumptions in Markdown.
* Start with a **sample fraction (1–5%)** for large datasets before scaling.
* Re-run analysis on full data once EDA logic is validated.

---

## 📂 Output

* Cleaned datasets (ready for feature engineering / ML).
* Markdown documentation of findings.
* Visualizations of key variables and distributions.

---

## 📌 Next Steps

1. Perform **data cleaning** (null handling, outlier removal).
2. Move to **feature engineering**.
3. Build **ML pipelines** in Databricks or MLflow.

