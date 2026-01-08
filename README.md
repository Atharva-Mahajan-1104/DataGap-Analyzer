

# 🩺 DataGap Analyzer

*A practical diagnostic and treatment toolkit for handling missing values in tabular machine-learning datasets.*

---

## 🚑 Why DataGap Analyzer?

Missing values are one of the most common—and dangerous—problems in real-world datasets. Ignoring them or blindly imputing can quietly degrade model performance or introduce bias.

**Missing Data Doctor** is built to answer four critical questions:

1. **How bad is the missing data problem?**
2. **Where exactly is data missing—and in what patterns?**
3. **Which imputation strategy works best for this dataset?**
4. **How does each choice affect downstream ML performance?**

Instead of guessing, this tool **measures, visualizes, compares, and reports** everything in a clean, reproducible way.

---

## ✨ What This Tool Does

Missing Data Doctor provides an end-to-end pipeline that:

* Quantifies missing values (counts & percentages)
* Visualizes missingness across rows and columns
* Applies multiple imputation strategies
* Trains downstream ML models on each imputed dataset
* Compares performance metrics side-by-side
* Generates a **self-contained HTML report** you can share or archive

It’s designed to be:

* 🔧 Drop-in for real ML workflows
* 📊 Interpretable for analysis & learning
* 🧪 Portfolio-ready for GitHub

---


## ⚡ Quick Start

### 1️⃣ Set up a virtual environment (Windows)

```bash
cd C:\Users\YourName\missing-data-doctor
python -m venv .venv
.\.venv\Scripts\activate
```

### 2️⃣ Install dependencies

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn jinja2
```

---

### 3️⃣ Run the demo pipeline

```bash
python src\cli.py ^
  --data data\example_with_missing.csv ^
  --target target ^
  --task classification ^
  --out_dir outputs\runs\demo
```

This single command will:

* Load the dataset
* Profile missing values
* Generate visualizations
* Apply **3 imputation strategies**
* Train & evaluate ML models
* Write all results to a single run folder

---

### 4️⃣ Open the report

```bash
start "" outputs\runs\demo\missing_data_doctor.html
```

No server required—just open the file.

---

## 📁 What Gets Generated

After execution, your run directory will look like:

```
outputs/runs/demo/
├── missing_summary.csv
├── summary.json
├── impact.json
├── plots/
│   ├── missing_bar.png
│   └── missing_heatmap.png
└── missing_data_doctor.html
```

Each run is **self-contained** and portable.

---

## 🧪 Example Dataset Explained

The demo dataset is intentionally small so patterns are easy to see:

| age | income | visits | score | target |
| --: | -----: | -----: | ----: | -----: |
|  25 |  30000 |      5 |   620 |      0 |
|  40 |        |     10 |   680 |      1 |
|  35 |  45000 |        |   640 |      0 |
|     |  70000 |     12 |   720 |      1 |
|  28 |  34000 |      6 |       |      0 |
|   … |      … |      … |     … |      … |

**Key characteristics**

* 10 rows × 5 columns
* Multiple features with partial missingness
* Binary classification target
* No missing labels (ideal supervised setup)

---

## 📊 Understanding the Visualizations

### Missingness per Feature (Bar Chart)

This plot answers:

> *“Which columns are hurting the most?”*

* Tall bars → higher risk features
* Low bars → simpler imputation may suffice
* Zero bars → safe features

This is your **first triage step**.

---

### Missingness Matrix (Heatmap)

This view answers:

> *“Is missingness random or structured?”*

It helps distinguish between:

* **MCAR** – scattered, random gaps
* **MAR** – missingness related to other features
* **MNAR** – missingness tied to the missing value itself

Understanding this directly informs which imputation strategy is safe.

---

## 🧠 Imputation + Model Impact

Missing Data Doctor doesn’t stop at filling values.

It evaluates how imputation choices affect **real ML performance**.

### Strategies evaluated:

* **Simple** (mean / median / mode)
* **KNN Imputation**
* **Iterative Imputation (MICE-style)**

Each strategy:

* Produces a complete dataset
* Trains a Random Forest model
* Reports metrics (AUC, Accuracy, etc.)

Example (`impact.json` schema):

```json
{
  "simple": { "AUC": 0.85, "Accuracy": 0.80 },
  "knn": { "AUC": 0.87, "Accuracy": 0.82 },
  "iterative": { "AUC": 0.86, "Accuracy": 0.81 }
}
```

📌 **Insight:**
The “best” imputer is dataset-dependent—and this tool proves it quantitatively.

---

## 🧾 The HTML Report

Each run generates a **standalone HTML report** that includes:

* Missing-value tables
* Embedded plots
* Model comparison metrics
* Clear sectioned layout

Because plots live alongside the report:

```
plots/missing_bar.png
plots/missing_heatmap.png
```

…the report works anywhere:

* Zip it
* Email it
* Archive it
* Share it

---




---

## 🔍 Design Philosophy

**DataGap Analyzer** is intentionally built to be:

* **Explicit** – missing data is treated as a measurable risk, not a silent preprocessing step
* **Comparative** – multiple imputations are evaluated side-by-side
* **Reproducible** – every run produces a self-contained artifact
* **Practical** – usable on real datasets, not just toy examples

The goal is not just to *fill gaps*, but to **understand their impact**.

---

## 🚀 Ideas for Extension

You can extend DataGap Analyzer in several directions:

* **Additional imputation strategies**

  * Mean vs median comparison
  * Domain-aware defaults (e.g., 0 for count features)
* **Missingness analysis**

  * Correlation between `is_missing(feature)` and other variables
  * Predicting missingness using logistic models
* **Fairness checks**

  * Does missing data disproportionately affect certain subgroups?
* **Time-series support**

  * Gap length analysis
  * Location of missing segments over time
* **MLOps integration**

  * Dataset monitoring
  * Regression tests for data quality drift

---

## 📌 When to Use DataGap Analyzer

* During **EDA** to understand dataset health
* Before **model training** to choose safe imputation strategies
* In **academic projects** to justify preprocessing decisions
* In **production workflows** to compare data repair choices
* As a **portfolio project** demonstrating applied ML thinking


---

## ⭐ Final Note

Missing data is rarely random—and rarely harmless.
**DataGap Analyzer** helps you treat it as a first-class problem, not an afterthought.

---

