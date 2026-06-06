# Olist E-Commerce: Retention Strategy Analysis
### A Data Analytics & Business Consulting Portfolio Project

An end-to-end analytics project investigating the structural 
retention failure of Olist, a Brazilian e-commerce platform, 
across 2016–2018. The project combines Power BI dashboard 
development with a McKinsey SCR-structured consulting 
presentation, translating 99K transactions across 9 
relational tables into a boardroom-ready strategic recommendation.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Data Source](#data-source)
- [Analysis Process](#analysis-process)
- [Key Findings](#key-findings)
- [Consulting Deliverable](#consulting-deliverable)
- [Tools & Stack](#tools--stack)
- [Limitations & Future Work](#limitations--future-work)
- [Getting Started](#getting-started)

---

## Project Overview

Olist scaled to **$14.27M in revenue** and **99K orders** 
across 27 Brazilian states between 2016 and 2018, with 
total revenue growing 119.4% YoY. However, beneath the 
top-line performance lies a structural problem that 
acquisition growth cannot solve:

> **96.95% of customers purchased only once.**

Returning buyers represent just 3.05% of the customer base 
yet generate **6.93% of total GMV**, more than twice 
the revenue per customer compared to first-time buyers. 
The $18M gap between new-customer revenue ($19M) and 
returning-customer revenue ($1M) is not a product problem 
or a delivery problem. It is the absence of any 
post-purchase engagement infrastructure.

This project identifies the root cause, segments the 
customer base to surface high-value at-risk cohorts, and 
proposes three data-backed initiatives projected to double 
the returning-buyer share and unlock **~$1.4M in 
additional GMV** within 12 months.

---

## Business Problem

**Central question:**
> *"How can Olist convert its acquisition engine into a 
> retention engine, and what is the quantified revenue 
> impact of doing so?"*

Structured using the McKinsey **SCR framework**:

| Layer | Statement |
|---|---|
| **Situation** | Olist achieved exponential growth *$14.27M revenue, 99K orders, $206.93 AOV) driven by an aggressive acquisition engine across 27 states |
| **Complication** | Revenue plateaued from early 2018; 96.95% single-purchase rate and 65%+ revenue concentration in SP + RJ expose a high-CAC "leaky bucket" with no retention mechanism |
| **Resolution** | Three targeted initiatives (RFM lifecycle program, installment loyalty rewards, category-specific retention plays) to reach 6% returning-buyer share within 12 months |

---

## Data Source

**Dataset:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
**Platform:** Kaggle  
**Period:** September 2016 – August 2018  
**Volume:** ~100K orders across 9 relational tables

> **Important data model note:** The dataset contains two 
> customer identifiers. `customer_id` is **order-level** 
> , a new ID is generated per transaction regardless of 
> buyer identity (99K). `customer_unique_id` is 
> **person-level**, it tracks the same buyer across 
> multiple orders (92K unique buyers). All retention 
> analysis in this project uses `customer_unique_id` 
> as the true identifier. The 7K delta between the two 
> figures confirms approximately 7K orders came from 
> returning buyers, consistent with the 96.95% 
> single-purchase rate.

---

## Analysis Process

### 1. Data Preparation
- Joined 9 relational tables: orders, customers, payments, 
  products, reviews, sellers, geolocation
- Resolved null values in delivery timestamps and 
  product category fields
- Built derived measures in DAX: `frequency_group`, 
  `delivery_status`, `installment_tier`, 
  `rfm_segment`, `returning_customer_flag`
- Validated customer identifier logic: confirmed 
  `customer_id` ≠ `customer_unique_id` and adjusted 
  all retention metrics accordingly

### 2. Descriptive Analysis (Situation)
- Monthly revenue trend 2016–2018: growth trajectory, 
  2018 plateau, November 2017 Black Friday spike
- Geographic revenue distribution: SP (~42%), RJ (~13%), 
  MG, RS, PR. 65%+ concentration in two states
- KPI scorecard: Total Revenue $14.27M (+117.1%), 
  Orders 99K (+119.8%), AOV $144.66, 27 states reached

### 3. Diagnostic Analysis, Hypothesis Testing (Complication)

Three leading hypotheses were tested and falsified:

| Hypothesis | Evidence | Verdict |
|---|---|---|
| Delivery delays drive churn | 73.54% of 1× buyers received on-time delivery; mean delay for churned (−11.73 days) ≈ mean delay for returned (−12.82 days) = no meaningful difference | ✕ Ruled out |
| Product longevity explains single-purchase | Single-purchase rate equally high in both short-lifecycle (Health Beauty, Stationery) and long-lifecycle (Furniture, Computers) categories | ✕ Ruled out |
| Geographic gaps limit retention | Single-purchase rate uniformly high across all 27 states; no state deviates more than 2 standard deviations from national average | ✕ Ruled out |

**Actual root cause:** Complete absence of post-purchase 
engagement — no re-engagement emails, no loyalty 
programme, no personalised cross-sell trigger exists 
on the platform.

> *Note: Hypothesis rejections are based on descriptive 
> evidence. Formal statistical testing (chi-square, 
> logistic regression, ANOVA by state) would be 
> recommended before production deployment of 
> retention initiatives.*

### 4. Predictive Analysis — RFM Segmentation (Resolution)

Built RFM (Recency · Frequency · Monetary) customer 
lifecycle segmentation across 8 segments:

| Segment | Count |
|---|---|
| Champions | 5,900 |
| Loyal Customers | 17,600 |
| New Customers | 11,700 |
| Promising | 11,700 |
| About-to-Sleep | 11,500 |
| At Risk | 11,700 |
| Cannot Lose Them | 11,500 |
| Hibernating | 11,800 |

Key finding: **58,200 customers** across non-retention 
segments have never returned. The at-risk pool 
(Cannot Lose Them + At Risk + About-to-Sleep = ~35K) 
represents customers with **proven spend history** 
who are at risk of permanent churn.

### 5. Category Portfolio — BCG Matrix

Mapped all product categories by repeat purchase 
potential (x-axis) vs. total revenue (y-axis):

| Quadrant | Categories | Action |
|---|---|---|
| **Stars** | Computer Accessories, Furniture Decor, Sports Leisure | Prioritise = highest LTV compounding |
| **Cash Cows** | Bed Bath Table, Health Beauty | Harvest = introduce replenishment model |
| **Question Marks** | Furniture Bedroom, Drinks | Test and learn |
| **Dogs** | Book Technical, Marketplace | De-prioritise |

### 6. Installment Signal Analysis

| Plan | % Orders | % Revenue | Revenue:Order Ratio |
|---|---|---|---|
| 1× | 58.09% | 44.49% | 0.77× |
| 2× | 13.61% | 11.14% | 0.82× |
| 3× | 11.85% | 11.44% | 0.97× |
| **10×** | **7.85%** | **15.90%** | **2.03×** |

10× installment buyers generate **2.03× more revenue 
per order** than 1× buyers, the strongest single 
LTV signal available at point of sale.

---

## Key Findings

**Growth:**
- Total revenue $14.27M across 2016–2018; 119.4% YoY 
  growth rate, but plateau visible from January 2018 
  onward for 8 consecutive months
- November 2017 revenue spike (+35% above trend) driven 
  by Black Friday, meaning seasonal dependency, not 
  organic demand

**Retention problem:**
- 96.95% single-purchase rate vs. 20–30% e-commerce 
  industry benchmark
- $19M from new buyers vs. $1M from returning buyers; 
  the $18M gap is the quantified loyalty opportunity
- Returning buyers = 3.05% of base, 6.93% of GMV — 
  2× per-customer revenue value

**Predictors of repeat purchase:**
- 10× installment plan: 7.85% of orders, 15.90% of 
  revenue — 2.03× revenue:order ratio vs. 1× buyers
- Repeat buyers concentrate in Computers Accessories 
  and Furniture Decor — high-ticket lifestyle 
  categories, not replenishment goods

**Customer portfolio:**
- Only 5,900 of 11,700 new customers ever reach 
  Champion status
- ~35K at-risk customers with proven spend history 
  require immediate re-engagement intervention
- 58,200 customers across non-retention lifecycle 
  segments have zero post-purchase engagement

**Geography:**
- SP + RJ account for 65%+ of total revenue; 
  Olist operates as a Southeast corridor platform 
  with isolated high-value pockets in interior states
- Retention failure is platform-wide, not regionally 
  concentrated — geography is not a factor

---

## Consulting Deliverable

**Output:** 9-slide McKinsey SCR-structured consulting 
presentation + 3-page interactive Power BI dashboard

### Power BI Dashboard (3 pages)

| Page | Content |
|---|---|
| **Overview** | Revenue trend, KPI scorecards, new vs. returning revenue split, purchase frequency distribution, geographic map |
| **Driver Analysis** | Delivery performance vs. frequency group, installment tier table, category revenue by frequency |
| **Portfolio & Customer Analysis** | RFM lifecycle distribution, BCG category matrix, revenue by segment × category table |

### Consulting Presentation (9 slides)

| Slide | Section | Content |
|---|---|---|
| 01 | Frontpage | Cover |
| 02 | Executive Summary | SCR summary + Key Take-aways |
| 03 | Body — Situation | Revenue trend + geographic concentration |
| 04 | Body — Complication | 96.95% single-purchase rate + $18M loyalty gap |
| 05 | Body — Diagnostic | Myth-busting: delivery, longevity, geography all ruled out |
| 06 | Body — Diagnostic | 10× installment signal + category migration pattern |
| 07 | Body — Resolution | RFM funnel (11.7K → 5.9K) + BCG matrix |
| 08 | Recommendations | 3 initiatives + impact model (~$1.4M GMV) |
| 09 | Recommendations | Phased roadmap: 0–30 / 30–90 / 6–12 months |

**Each body slide follows McKinsey anatomy:**  
`Action Title` → `Subheadline` → `Slide Body` → 
`Source / Footer`

### Strategic Recommendations

**Initiative 1 — Activate post-purchase lifecycle program** 
*(Phase 1: Quick Win, 0–30 days)*
- Deploy personalised email and push re-engagement 
  for ~35K at-risk customers within 30–60 days of 
  first order
- Message sequence: order confirmation → category 
  cross-sell at day 14 → loyalty incentive at day 30
- Target: +0.5% returning-buyer rate

**Initiative 2 — Build repeat behavior in Star 
categories first** *(Phase 2: Build, 30–90 days)*
- Concentrate retention investment in Computers 
  Accessories and Bed Bath Table (BCG Stars)
- Introduce upgrade and cross-sell paths; category-
  specific triggers outperform generic re-engagement
- Target: +1.5% returning-buyer rate

**Initiative 3 — Deploy category-specific 
retention plays** *(Phase 3: Scale, 6–12 months)*
- Health & Beauty: introduce replenishment reminders 
  and subscription framing for the natural 60–90 day 
  repurchase cycle
- Full loyalty programme infrastructure + NPS 
  data collection pipeline
- Target: 6% returning-buyer rate

**Projected impact:** Doubling returning-buyer share 
from 3% → 6% at current AOV unlocks **~$1.4M 
additional GMV** within 12 months.

---

## Tools & Stack

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | 3-page interactive dashboard with cross-filtering |
| **DAX** | Custom measures: RFM scoring, frequency grouping, returning customer flag, installment tier, revenue segmentation |
| **Power Query** | Data joins across 9 relational tables, null handling, type standardisation |
| **McKinsey SCR Framework** | Consulting presentation narrative structure |
| **BCG Matrix** | Category portfolio prioritisation |

---

## Limitations & Future Work

**Current limitations:**
- Hypothesis rejections are descriptive, not 
  inferential. Formal statistical testing 
  (chi-square on delivery vs. return rate; 
  logistic regression on churn predictors; 
  ANOVA across states) would strengthen 
  diagnostic claims before production use
- No customer contact data, campaign history, 
  or NPS scores available. Retention initiatives 
  cannot be A/B tested within this dataset

**Future extensions:**
- Build a churn prediction model using logistic 
  regression or gradient boosting on RFM features
  and purchase signals
- Integrate NPS or satisfaction survey data to 
  enrich root-cause analysis
- Automate RFM segmentation refresh via scheduled 
  Power BI dataflows
- Expand geographic analysis as platform reaches 
  broader state coverage beyond Southeast corridor

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/yourusername/olist-retention-analysis

# Repository structure
├── data/
│   ├── raw/               # Original Kaggle CSV files
│   └── processed/         # Cleaned and joined tables
├── powerbi/
│   └── olist_dashboard.pbix
├── presentation/
│   └── olist_consulting_deck.pdf
├── docs/
│   └── analysis_notes.md  # Methodology and DAX measures
└── README.md
```

**To view the dashboard:** Open 
`powerbi/olist_dashboard.pbix` in Power BI Desktop 
(free to download).

**To view the presentation:** Open 
`presentation/olist_consulting_deck.pdf`.

---

*Source: Olist public dataset · Kaggle ·  
Portfolio Project · June 2026*
