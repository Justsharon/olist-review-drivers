# Olist Review Drivers

**What predicts a 1-star review on Brazilian e-commerce — and which factor matters most?**

 **[Live dashboard →](https://olist-review-drivers.vercel.app/)**
 **[Full analysis notebook →](./notebooks/04_analysis.ipynb)**

---

## The Question

Olist is Brazil's largest e-commerce marketplace. Across 95,809 delivered orders with reviews, ~10% receive 1-star scores. The product team wants to know: **which factors drive customer dissatisfaction — and where should engineering invest to reduce 1-star rates?**

## The Headline Findings

Three statistically significant drivers, ranked by impact:

| Driver | Effect Size | Strength |
|---|---|---|
| **Late delivery** | OR = 16.35 | Very strong — primary intervention target |
| **Multi-seller orders** | OR = 5.40 | Strong — independent of delivery performance |
| **Product category** | Cramér's V = 0.062 | Weak — segmentation lens, not lever |

### The Counterintuitive Finding

The dataset's biggest surprise: **multi-seller orders aren't a logistics problem.** They arrive *faster* and *more on-time* than single-seller orders — yet have 4× higher 1-star rates. This suggests the friction is psychological (fragmented arrivals, expectation mismatch) rather than operational.

### The Strongest Finding

The single largest effect in the dataset: **on-time delivery has a 6.6% 1-star rate. One-week-late delivery has a 70% 1-star rate.** A 10× jump from a single missed estimate. Customers anchor on the promised date — once it's broken, sentiment collapses.

## How This Analysis Was Done

Followed an 8-step analytical framework:

1. **Problem definition** — narrowed "what causes bad reviews?" to specific, testable factor categories
2. **Data understanding** — mapped 9 source CSVs, selected 5 relevant tables, defined join strategy
3. **Cleaning** — applied cohort filters (delivered orders with reviews), resolved type issues, dropped 23 rows with missing dates
4. **Exploration** — generated 7 candidate findings, with effect sizes and confounder checks
5. **Hypothesis formulation** — pre-registered H₀ and H₁ before running any formal tests (anti-p-hacking discipline)
6. **Method selection** — chose chi-square tests with appropriate effect-size measures per setup
7. **Analysis** — ran the tests; computed odds ratios and Cramér's V
8. **Interpretation** — translated statistical findings into business recommendations with explicit caveats

Each decision is documented in the notebooks with reasoning, not just code.

## What This Analysis Cannot Tell You

- **Observational, not causal.** Late delivery *predicts* 1-star reviews; whether it *causes* them needs a randomized intervention to confirm.
- **Selection bias.** The dataset is customers who chose to leave reviews. Non-reviewers may behave differently.
- **Geographic context.** Effects likely generalize qualitatively to other e-commerce markets but not quantitatively.

## Repo Structure

olist-review-drivers/
├── notebooks/
│   ├── 01_exploration.ipynb     # Schema mapping, table loading
│   ├── 02_cleaning.ipynb        # Cohort filters, type conversions, joins
│   ├── 03_exploration.ipynb     # 7 candidate findings with confounders
│   └── 04_analysis.ipynb        # Formal hypotheses + chi-square tests
├── sql/
│   ├── analysis_queries.sql     # Analysis-equivalent SQL
│   └── practice/                # Daily SQL drills (CTEs, window functions)
├── dashboard/                   # SvelteKit + Tailwind dashboard
└── data/
└── README.md                # Download instructions (data not committed)

## Tech Stack

- **Python / Pandas** — data manipulation and joins
- **scipy.stats** — chi-square tests and effect sizes
- **SQL (SQLite)** — analytical queries replicating key findings
- **SvelteKit + Tailwind CSS** — dashboard frontend
- **Vercel** — dashboard deployment

## About

Built by **Sharon Odiwa** — a frontend engineer transitioning into data analytics. This is a portfolio piece demonstrating end-to-end analytical work: from messy public data to a deployable dashboard with defensible findings and articulated caveats.

[Live dashboard](https://olist-review-drivers.vercel.app/) 
[Full notebook](./notebooks/04_analysis.ipynb) 