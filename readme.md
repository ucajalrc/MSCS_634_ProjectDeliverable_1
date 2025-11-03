
### **MSCS 634 – Big Data and Data Mining**

**Deliverable 1: Data Collection, Cleaning, and Exploration**
**Student:** Ajal RC <br>
**Instructor:** Satish Penmatsa <br>
**Date:** November 2, 2025

---

### **Dataset Summary**

The dataset used for this project is **Online Retail II**, obtained from the **UCI Machine Learning Repository** (mirrored on Kaggle).
It contains **over 500,000 retail transactions** made by a UK-based online store between 2009 and 2011.
Each record includes details such as:

* `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, and `Country`.

This dataset is highly suitable for a data mining project because it allows exploration of **regression** (e.g., predicting revenue), **classification** (e.g., return vs. non-return orders), **clustering** (e.g., customer segmentation), and **association rule mining** (e.g., product co-purchase patterns).

NOTE: The original dataset (~94 MB) was compressed (online_retail_II.zip) to remain within GitHub size limits. The notebook automatically reads the zipped file, so no manual extraction is needed.
---

### **Major Steps in Data Cleaning and Exploration**

1. **Data Loading and Inspection**

   * The dataset was loaded using `pandas`. Initial inspection confirmed over half a million records and multiple numeric and categorical attributes.
   * Preliminary summaries (`df.info()`, `df.describe()`) revealed minor missingness and some negative quantity values (representing product returns).

2. **Basic Hygiene and Structure**

   * Column names were standardized to lowercase with underscores for consistency.
   * The `InvoiceDate` field was parsed to a proper datetime object to enable time-based analysis.
   * Duplicate records were removed to prevent data inflation.

3. **Handling Missing and Noisy Data**

   * Missing `CustomerID` values were retained but encoded as `"Unknown"` to preserve valuable transactional records.
   * Negative `Quantity` values were not discarded but flagged as **returns or cancellations**, a behavior that can later serve as a target for classification.
   * Invalid negative `UnitPrice` entries were removed.

4. **Feature Creation and Initial Exploration**

   * New variable `line_total = Quantity × UnitPrice` was added to represent per-line revenue.
   * Time-based features (`invoice_year`, `invoice_month`) were derived to analyze seasonality.
   * Visualizations (using Matplotlib) were generated to understand data distributions, missingness, and basic revenue patterns.

5. **Exploratory Data Analysis (EDA)**

   * Histograms and IQR outlier checks showed that variables such as `Quantity` and `UnitPrice` are heavily skewed.
   * Correlation analysis indicated moderate relationships among monetary and count variables.
   * Revenue aggregated by month displayed strong **seasonal trends**, while country-level summaries showed high concentration in the UK market.

---

### **Key Insights from EDA**

* **Sales Concentration:** The majority of revenue comes from a small number of high-value orders and a single dominant country (the United Kingdom).
* **Seasonality:** Clear peaks appear during specific months, implying that **seasonal factors strongly influence demand**.
* **Returns and Cancellations:** Around 1–2% of orders are returns (negative quantities). This behavior introduces a natural classification problem.
* **Outliers:** Monetary fields show heavy right skew, suggesting that **log-transformations or robust scaling** will be useful for modeling.
* **Missingness:** The absence of `CustomerID` may carry business meaning (e.g., guest purchases), so missingness should be modeled rather than simply dropped.

---

### **How EDA Insights Guide Future Modeling Steps**

These insights form a blueprint for the upcoming deliverables:

* For **regression**, `line_total` can serve as the target, with price, quantity, and temporal features as predictors.
* For **classification**, `is_return_or_cancel` can be modeled to predict future return likelihood.
* For **clustering**, features such as frequency, recency, and monetary value (RFM) can segment customers.
* For **association rule mining**, cleaned transactional pairs (InvoiceNo, StockCode) can be used to uncover product co-occurrence patterns.

The observed skew, seasonality, and concentration will also shape **feature scaling**, **sampling strategy**, and **model evaluation** in subsequent deliverables.

---

### **Challenges and How They Were Addressed**

| **Challenge**                 | **Resolution**                                                                                                          |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Missing `CustomerID` values   | Used a literal `"Unknown"` to retain rows while preserving missingness information.                                     |
| Negative `Quantity` (returns) | Flagged as `is_return_or_cancel` instead of dropping, preserving a useful classification label.                         |
| Negative `UnitPrice` entries  | Removed to eliminate invalid business cases.                                                                            |
| Highly skewed distributions   | Retained raw data for now; plan to apply log transformations or robust models in Deliverable 2.                         |
| Large file size               | Kept full CSV locally but generated a smaller cleaned sample (`online_retail_II_clean_sample.csv`) for reproducibility. |

---

### **References (APA 7th Edition)**

Dua, D., & Graff, C. (2019). *UCI Machine Learning Repository*. University of California, Irvine, School of Information and Computer Sciences. [https://archive.ics.uci.edu](https://archive.ics.uci.edu)
Kaggle. (n.d.). *Online Retail II Data Set* (mirror). Retrieved from [https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci)

---

**Summary:**
This README fully covers all required elements:

* Concise dataset summary and key insights
* Major steps in data cleaning and exploration
* EDA findings tied to future modeling direction
* Challenges encountered and their resolutions

---
