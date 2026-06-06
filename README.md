# E-Commerce Customer Segmentation (RFM) & Market Basket Analysis

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.2.2-150458?logo=pandas)
![mlxtend](https://img.shields.io/badge/mlxtend-0.23.1-orange)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

An end-to-end data science portfolio project that transforms raw e-commerce transaction data into actionable business insights using **RFM Segmentation** and **Market Basket Analysis**.

---

## Project Structure
```
├── data/
│   ├── raw/                    # Raw dataset (not tracked by git)
│   │   └── ecommerce.csv
│   └── processed/              # Cleaned & output data (not tracked by git)
│       ├── ecommerce_cleaned.csv
│       └── rfm_segments.csv
│
├── notebooks/
│   ├── 01_data_cleaning_eda.ipynb          # Data cleaning & exploratory analysis
│   ├── 02_rfm_segmentation.ipynb           # RFM scoring & customer segmentation
│   └── 03_market_basket_analysis.ipynb     # Apriori & association rules
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Business Objectives

### 1. RFM Customer Segmentation
Segment customers based on three behavioral dimensions:

| Dimension | Description |
|-----------|-------------|
| **Recency** | How recently did the customer make a purchase? |
| **Frequency** | How often do they purchase? |
| **Monetary** | How much do they spend in total? |

Each customer receives an RFM score (1–5 per dimension) and is mapped to one of **7 segments**: Champions, Loyal Customers, Potential Loyalist, Promising, At Risk, Hibernating, or Lost. This enables the marketing team to design targeted retention and re-engagement campaigns.

### 2. Market Basket Analysis
Using the **Apriori algorithm**, we identify product association rules of the form:

> *"Customers who buy Product A tend to also buy Product B."*

These rules are ranked by **Lift** and **Confidence** to surface the strongest, non-trivial product relationships — directly usable for cross-selling features and bundle promotions.

---

## Dataset

- **Source:** [Kaggle — E-Commerce Data by carrie1](https://www.kaggle.com/datasets/carrie1/ecommerce-data)
- **Records:** ~540,000 transactions (pre-cleaning)
- **Period:** December 2010 – December 2011
- **Market:** Primarily United Kingdom-based online retail

| Column | Description |
|--------|-------------|
| `InvoiceNo` | Unique invoice number (prefix 'C' = cancellation) |
| `StockCode` | Product code |
| `Description` | Product name |
| `Quantity` | Units purchased per transaction |
| `InvoiceDate` | Date and time of invoice |
| `UnitPrice` | Price per unit (GBP) |
| `CustomerID` | Unique customer identifier |
| `Country` | Customer's country of residence |

---

## Methodology

### Notebook 01 — Data Cleaning & EDA
- Remove rows with missing `CustomerID`
- Drop cancelled invoices (prefix `'C'`) and invalid `Quantity`/`UnitPrice` values
- Feature engineering: `TotalSpend`, temporal features (`Year`, `Month`, `Hour`)
- Exploratory visualizations: revenue by country, monthly trend, top products, hourly traffic

### Notebook 02 — RFM Segmentation
- Compute **Recency**, **Frequency**, **Monetary** per customer using `groupby`
- Score each dimension into quintiles (1–5) using `pd.qcut`
  - Recency scoring is **inverted** (lower recency = more recent = higher score)
- Map RFM score combinations to 7 customer segments via rule-based function
- Visualize segment distribution, average monetary value, and Recency vs Frequency scatter

### Notebook 03 — Market Basket Analysis
- Filter to UK transactions (~90% of data) for memory efficiency and market specificity
- Build a **binary basket matrix**: rows = invoices, columns = products
- Run **Apriori** with `min_support=0.02`
- Generate **association rules** filtered by `lift ≥ 1.0`, sorted by lift and confidence
- Business recommendations dynamically generated from top-ranked rules

---

## Key Results

### RFM Segmentation
| Segment | Strategy |
|---------|----------|
| **Champions** | Reward program, brand advocacy |
| **Loyal Customers** | Upsell, loyalty points |
| **Potential Loyalist** | Onboarding, nurturing campaigns |
| **Promising** | Early engagement offers |
| **At Risk** | Win-back campaigns |
| **Hibernating** | Low-cost re-engagement |
| **Lost** | Sunset / unsubscribe |

### Market Basket Analysis
- Rules with **Lift > 2** indicate strong, non-coincidental product associations
- Top rules are used to drive cross-selling recommendations and bundle promotions directly at checkout

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/rdityaza/ecommerce-customer-segmentation-rfm.git
cd ecommerce-customer-segmentation-rfm
```

**2. Create and activate virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Download the dataset**

Download `data.csv` from [Kaggle](https://www.kaggle.com/datasets/carrie1/ecommerce-data) and place it at:
```bash
data/raw/ecommerce.csv
```

**5. Run notebooks in order**
```bash
jupyter notebook
```
Open and run sequentially:
1. `notebooks/01_data_cleaning_eda.ipynb`
2. `notebooks/02_rfm_segmentation.ipynb`
3. `notebooks/03_market_basket_analysis.ipynb`

---

## Tech Stack

| Library | Version | Purpose |
|---------|---------|---------|
| `pandas` | 2.2.2 | Data manipulation |
| `numpy` | 1.26.4 | Numerical operations |
| `matplotlib` | 3.9.0 | Base plotting |
| `seaborn` | 0.13.2 | Statistical visualization |
| `mlxtend` | 0.23.1 | Apriori & association rules |
| `jupyter` | 1.0.0 | Notebook environment |

---

## Author

**Raditya Zaki Athaya**  
Sistem dan Teknologi Informasi — Institut Teknologi Bandung (ITB)  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/raditya-zaki-athaya)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?logo=github)](https://github.com/rdityaza)