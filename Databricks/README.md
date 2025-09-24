Skip to content
Navigation Menu
antoniguedes
Azure_Cloud_Computing_tools_projects_Databricks_DataFactory_Synapse

Type / to search
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
Settings
Azure_Cloud_Computing_tools_projects_Databricks_DataFactory_Synapse/Databricks
/
README.md
in
main

Edit

Preview
Indent mode

Spaces
Indent size

2
Line wrap mode

Soft wrap
Editing README.md file contents
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
102
103
104
105
106
107
108
109
110
111
112
113
114
115
116
117
118
119
120
121
122
123
124
125
126
127
128
129
130
131
132
133
134
135
136
137
138
139
140
141
142
143
144
145
146
147
148
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


Use Control + Shift + m to toggle the tab key moving focus. Alternatively, use esc then tab to move to the next interactive element on the page.
No file chosen
Attach files by dragging & dropping, selecting or pasting them.
Editing Azure_Cloud_Computing_tools_projects_Databricks_DataFactory_Synapse/Databricks/README.md at main · antoniguedes/Azure_Cloud_Computing_tools_projects_Databricks_DataFactory_Synapse 
