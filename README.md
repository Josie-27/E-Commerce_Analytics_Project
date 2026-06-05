# Olist E-Commerce: Retention Strategy Analysis
### A Data Analytics & Business Consulting Portfolio Project

A end-to-end analytics project analysing customer retention 
patterns on the Olist Brazilian e-commerce platform (2016–2018). 
The project spans data cleaning, exploratory analysis, RFM 
segmentation, and a McKinsey SCR-structured consulting 
presentation — translating raw transaction data into actionable 
business strategy.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Data Source](#data-source)
- [Analysis Process](#analysis-process)
- [Key Findings](#key-findings)
- [Consulting Deliverable](#consulting-deliverable)
- [Tools Used](#tools-used)
- [Limitations & Future Work](#limitations--future-work)
- [Getting Started](#getting-started)

---

## Project Overview

Olist achieved strong growth between 2016 and 2018 — $14.27M 
in revenue across 99K orders and 27 states. However, beneath 
the top-line performance lies a structural problem: **96.95% 
of customers purchased only once**, despite returning buyers 
generating 2× the per-customer revenue of first-time buyers.

This project investigates why retention is so low, identifies 
which customer segments and product categories offer the highest 
retention potential, and proposes three data-backed strategic 
initiatives to double the returning-buyer share.

---

## Business Problem

**Central question:**
> *"How can Olist convert its acquisition engine into a 
> retention engine — and what is the revenue impact of doing so?"*

The analysis is structured around the McKinsey 
**SCR (Situation–Complication–Resolution)** framework:

| Layer | Question |
|---|---|
| **Situation** | Olist grew 117% in revenue but plateaued in 2018 |
| **Complication** | 96.95% single-purchase rate with no engagement mechanism |
| **Resolution** | 3 targeted initiatives to unlock ~$1.4M additional GMV |

---

## Data Source

**Dataset:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
**Platform:** Kaggle  
**Period:** September 2016 – August 2018  
**Size:** ~100K orders, 9 relational tables

> **Data model note:** The dataset contains two customer 
> identifier fields. `customer_id` is order-level (99K), 
> generating a new ID per transaction. `customer_unique_id` 
> is person-level (92K), tracking the same buyer across 
> multiple orders. All retention analysis uses 
> `customer_unique_id` as the true identifier. The 7K delta 
> between the two figures confirms ~7K orders came from 
> returning buyers — consistent with the 96.95% 
> single-purchase rate.

---

## Analysis Process

### 1. Data Cleaning & Preparation
- Joined 9 relational tables across orders, customers, 
  payments, products, and reviews
- Standardised date fields and resolved null values in 
  delivery timestamps
- Created derived fields: `frequency_group`, 
  `delivery_status`, `installment_tier`

### 2. Exploratory Data Analysis (Descriptive)
- Monthly revenue trend analysis (2016–2018)
- Geographic revenue distribution by Brazilian state
- Purchase frequency distribution using `customer_unique_id`
- New vs. returning customer revenue split

### 3. Diagnostic Analysis — Hypothesis Testing
Three leading hypotheses for low retention were tested 
and ruled out using descriptive evidence:

| Hypothesis | Evidence | Verdict |
|---|---|---|
| Delivery delays cause churn | 73.54% of 1× buyers received on-time delivery yet never returned | ✕ Ruled out |
| Low product value discourages return | AOV of $144.66 is healthy by e-commerce standards | ✕ Ruled out |
| Geographic gaps limit retention | Single-purchase rate is uniformly high across all 27 states | ✕ Ruled out |

> *Note: These are descriptive rejections. Formal 
> statistical testing (chi-square, logistic regression) 
> would be recommended before production deployment 
> of retention initiatives.*

### 4. Predictive Analysis — RFM Segmentation
- Built RFM (Recency, Frequency, Monetary) customer 
  lifecycle segments
- Identified conversion gap: 11,700 New Customers → 
  only 5,900 Champions
- Quantified at-risk pool: ~35K customers across 
  Cannot Lose Them, At Risk, and About-to-Sleep segments

### 5. Category Portfolio — BCG Matrix
- Mapped all product categories against repeat potential 
  and revenue contribution
- Stars (Computers Accessories, Furniture Decor): 
  high revenue + high repeat → prioritise
- Cash Cows (Bed Bath Table, Health Beauty): 
  high revenue + low repeat → harvest
- Question Marks (Telephony, Pet Shop): test and learn
- Dogs (Stationery, Construction): de-prioritise

---

## Key Findings

- **96.95%** of customers bought only once — vs. 
  20–30% industry benchmark for repeat rate
- **$19M** from new customers vs. **$1M** from 
  returning customers — the $18M gap is the 
  loyalty opportunity
- **10× installment plan buyers** represent only 5% 
  of orders but generate **14.85% of revenue** — 
  the strongest LTV signal in the dataset
- Revenue is concentrated in **São Paulo and Rio de 
  Janeiro**; 25 of 27 states contribute marginally — 
  Olist is a Southeast corridor platform, not 
  a national one
- Growth **plateaued from January 2018**, confirming 
  limits of the acquisition-only model

---

## Consulting Deliverable

The final output is a **9-slide McKinsey SCR-structured 
consulting presentation** covering:

| Slide | Content |
|---|---|
| 01 | Cover |
| 02 | Executive Summary (SCR + Key Take-aways) |
| 03 | Situation — Growth at a Glance |
| 04 | Complication — The Retention Problem |
| 05 | Diagnostic — Myth-Busting Root Causes |
| 06 | Diagnostic — Predictors of Repeat Purchase |
| 07 | Resolution — Customer Portfolio (RFM + BCG) |
| 08 | Resolution — Strategic Recommendations |
| 09 | Resolution — Phased Roadmap & Impact |

**Each slide follows the McKinsey anatomy:**  
Action Title → Subheadline → Slide Body → Source/Footer

**Strategic recommendations (prescriptive layer):**
1. **Activate post-purchase lifecycle program** — 
   RFM-triggered re-engagement for 35K at-risk 
   customers within 30–60 days *(Quick Win)*
2. **Reward 10× installment-plan commitment** — 
   loyalty perks tied to the highest-LTV buyer 
   segment *(Medium-term)*
3. **Deploy category-specific retention plays** — 
   subscription model for Health Beauty; 
   cross-sell/upgrade path for Stars 
   (Computers + Furniture) *(Strategic)*

**Projected impact:** If returning-buyer share doubles 
from 3% → 6%, estimated GMV uplift is **~$1.4M** at 
current AOV.

---

## Tools Used

| Tool | Purpose |
|---|---|
| **Power BI** | Interactive dashboard — 3 pages: Overview, Driver Analysis, Portfolio & Customer Analysis |
| **DAX** | Custom measures: RFM scoring, frequency grouping, revenue segmentation |
| **Excel / CSV** | Data inspection and initial profiling |
| **McKinsey SCR Framework** | Consulting presentation structure |

---

## Limitations & Future Work

**Current limitations:**
- Hypothesis rejections are descriptive, not inferential — 
  formal statistical testing (chi-square, logistic 
  regression, ANOVA by state) would strengthen the 
  diagnostic claims
- No customer contact or campaign data available — 
  retention initiatives cannot be A/B tested 
  within this dataset
- Geographic analysis is limited by data concentration; 
  Nordeste representation is minimal

**Future extensions:**
- Add NPS or satisfaction survey data to enrich 
  churn analysis
- Build a predictive churn model using logistic 
  regression or gradient boosting on RFM features
- Automate RFM segmentation refresh via scheduled 
  Power BI dataflows
- Expand geographic analysis once platform reaches 
  broader state coverage

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/yourusername/olist-retention-analysis

# Repository structure
├── data/               # Raw and cleaned CSV files
├── powerbi/            # .pbix dashboard file
├── presentation/       # 9-slide consulting deck (PDF)
├── docs/               # Supporting analysis notes
└── README.md
```

**To view the dashboard:** Open `powerbi/olist_dashboard.pbix` 
in Power BI Desktop (free).  
**To view the presentation:** Open `presentation/olist_consulting_deck.pdf`.

---

*Source: Olist public dataset via Kaggle · 
Team analysis · Portfolio Project 2025*
