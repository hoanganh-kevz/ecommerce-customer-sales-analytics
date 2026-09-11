# 🛒 E-Commerce Customer & Sales Analytics

A portfolio project analyzing the **UCI Online Retail Dataset** using Python to understand sales performance, product performance, customer behavior, customer value, and retention.

The project follows an end-to-end analytics workflow: data cleaning, exploratory analysis, product and customer analysis, RFM segmentation, cohort retention analysis, and business recommendations.

---

## Project Objectives

This project aims to answer questions such as:

- How does sales performance change over time?
- Which products generate the most revenue and sales volume?
- How concentrated is customer spending and purchase frequency?
- Which customers are the most recent, frequent, and valuable?
- How can customers be grouped into actionable RFM segments?
- How well are customers retained after their first observed purchase?
- What business actions can be recommended from the observed patterns?

---

## Dataset

**Source:** UCI Machine Learning Repository — Online Retail Dataset  
https://archive.ics.uci.edu/dataset/352/online+retail

The dataset contains transactional data for a UK-based online retailer between **December 1, 2010 and December 9, 2011**.

### Raw dataset

- Rows: **541,909**
- Columns: **8**

Main fields:

- `InvoiceNo`
- `StockCode`
- `Description`
- `Quantity`
- `InvoiceDate`
- `UnitPrice`
- `CustomerID`
- `Country`

---

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Google Colab
- Git / GitHub

---

## Analysis Workflow

### 1. Data Loading & Understanding

Reviewed dataset structure, missing values, duplicates, transaction fields, and basic data quality issues.

### 2. Data Cleaning & Preparation

Key cleaning decisions included:

- Separating non-sales inventory adjustments from transaction data
- Separating accounting adjustment records
- Removing exact duplicate rows
- Retaining missing `CustomerID` values for transaction-, product-, and geographic-level analysis
- Excluding missing `CustomerID` values only when customer identity is required
- Retaining valid zero-price free-gift transactions
- Preserving cancellation transactions in the cleaned dataset for analyses where net sales are relevant

Final cleaned dataset:

- Rows: **534,162**
- Unique invoices: **23,799**
- Unique customers: **4,372**
- Unique products: **3,938**
- Total net sales: **£9,748,131.07**

---

### 3. Exploratory Data Analysis

Explored:

- Overall sales and transaction metrics
- Monthly sales trends
- Sales distribution
- Geographic sales concentration
- Customer transaction frequency

Customer and sales distributions were strongly right-skewed, indicating that business activity is concentrated among a relatively small number of transactions and customers.

---

### 4. Sales & Product Analysis

Product analysis was based on successful merchandise transactions and excluded non-merchandise codes such as postage, fees, and internal adjustment codes.

Key findings:

- High sales volume does not always produce the highest revenue.
- Product performance should be evaluated using multiple metrics rather than quantity alone.
- Revenue is concentrated among a relatively small group of products.

Examples:

- **REGENCY CAKESTAND 3 TIER** generated approximately **£174,156.54** from **13,861 units**.
- **PAPER CRAFT, LITTLE BIRDIE** generated approximately **£168,469.60** from **80,995 units**.

This illustrates that **Quantity ≠ Revenue**.

---

### 5. Customer Analysis

Customer-level analysis used transactions with valid `CustomerID` values.

Metrics included:

- Net Sales
- Transaction Frequency
- Net Average Order Value

Key observations:

- Customer spending is highly right-skewed.
- Median customer net sales: **£644.07**
- Median transaction frequency: **3 invoices**
- Median Net AOV: **£235.15**
- A small group of customers generates substantially higher value and activity than the majority.

High-value observations were treated as distributional outliers, not automatically as data errors.

---

## 6. RFM Customer Segmentation

RFM evaluates customers using:

- **Recency:** how recently a customer made a successful purchase
- **Frequency:** how often a customer made successful purchases
- **Monetary:** revenue generated from successful purchase transactions

RFM used:

- Valid `CustomerID`
- Positive quantity
- Non-cancellation invoices

The Recency reference date was derived from the maximum transaction date rather than the current date.

### RFM dataset

- Customers analyzed: **4,339**

Customers were scored from **1 to 4** on Recency, Frequency, and Monetary dimensions and grouped into seven behavioral segments:

- Champions
- Loyal Customers
- Recent Customers
- Promising
- At Risk
- Need Attention
- Hibernating

### Segment highlights

| Segment | Customer Share | Monetary Share |
|---|---:|---:|
| Champions | 12.19% | 49.99% |
| Loyal Customers | 21.20% | 23.67% |
| Hibernating | 21.80% | 5.11% |
| At Risk | 12.93% | 11.14% |
| Need Attention | 14.82% | 4.05% |
| Promising | 10.86% | 2.65% |
| Recent Customers | 6.20% | 3.40% |

The most important result is the concentration of customer value: **Champions represent only 12.19% of customers but generate approximately 49.99% of total RFM Monetary value**.

---

## 7. Cohort & Retention Analysis

Customers were grouped by their **first observed successful purchase month** and tracked across subsequent months.

To avoid bias from incomplete monthly data, **December 2011 was excluded from the retention analysis** because the dataset ends on December 9, 2011.

Key observations:

- Retention generally falls substantially after the first observed purchase.
- For many 2011 cohorts, second-month retention is approximately **15%–24%**.
- The December 2010 cohort shows stronger long-term retention, with many observed months around the **30%–40%** range and approximately **50% retention in Month 12**.

The earliest cohort should be interpreted carefully because the dataset begins in December 2010. Its first observed purchase may not represent the customer's true first-ever purchase.

---

## 8. Key Business Insights

### Customer value is highly concentrated

A relatively small group of customers contributes a disproportionately large share of purchase value.

### Retention is an important opportunity

Many cohorts show a substantial drop after the first observed purchase, suggesting that increasing repeat purchase behavior could be valuable.

### At Risk customers deserve attention

The At Risk segment has meaningful historical purchasing activity and Monetary value but lower recent engagement.

### Hibernating customers are numerous but low-value on average

This segment is large but contributes a relatively small share of Monetary value, suggesting that lower-cost re-engagement approaches may be more appropriate.

### Product decisions should use multiple metrics

High-volume products are not always the highest-revenue products. Quantity, revenue, and average selling price should be considered together.

---

## Business Recommendations

Based on the observed patterns:

- Prioritize retention of **Champions** and **Loyal Customers**
- Develop targeted reactivation strategies for **At Risk** customers
- Use lower-cost automated re-engagement for **Hibernating** customers
- Improve the customer journey after the first observed purchase to encourage repeat orders
- Evaluate product performance using both revenue and quantity metrics
- Reduce excessive dependence on a small number of high-value customers by developing mid-value segments
- Recalculate RFM periodically to monitor customer movement between segments

These recommendations are analytical suggestions based on transaction patterns and should be tested with additional business and campaign data before large-scale implementation.

---

## Analysis Limitations

- The dataset covers approximately one year, limiting long-term trend analysis.
- December 2011 contains only partial-month data.
- Missing `CustomerID` values mean customer-level analysis does not represent every transaction.
- Cohort membership represents the **first observed purchase**, not necessarily true acquisition.
- RFM segmentation uses rule-based quartile thresholds rather than externally validated customer categories.
- RFM Monetary represents successful purchase revenue, while other customer metrics may use net sales including cancellations.
- The dataset does not include customer demographics, acquisition channels, marketing campaigns, product costs, or profit margins.
- Observed relationships should not automatically be interpreted as causal explanations.

---

## Repository Structure

```text
E-Commerce-Analytics/
│
├── ecommerce_analysis.ipynb
├── README.md
└── data/
    └── Online Retail.xlsx
```

> If the dataset is not stored in the repository, download it from the UCI source above and place it in the `data/` directory.

---

## How to Run

1. Clone this repository.
2. Download the UCI Online Retail dataset.
3. Place `Online Retail.xlsx` inside the `data/` folder.
4. Open `ecommerce_analysis.ipynb` in Jupyter Notebook or Google Colab.
5. Update the dataset path if necessary.
6. Run the notebook from top to bottom.

Example:

```python
import pandas as pd

df = pd.read_excel("data/Online Retail.xlsx")
```

---

## Skills Demonstrated

This project demonstrates practical experience with:

- Data cleaning and data quality investigation
- Exploratory Data Analysis
- Business metric design
- Sales and product analytics
- Customer behavior analysis
- RFM customer segmentation
- Cohort and retention analysis
- Data visualization
- Translating analytical findings into business recommendations
- Communicating assumptions and limitations

---

## Project Status

**Completed**

The analysis covers the full workflow from raw transactional data to customer segmentation, retention analysis, and business recommendations.
