# Patent Portfolio Transfers

This repository documents a data construction and exploratory analysis project on **large-scale patent portfolio transfers**. The goal of the project is to assess whether patent portfolio transactions can be systematically identified using public data, and whether economically meaningful information—particularly transaction prices—can be recovered or proxied.

The project was developed during the Hart Fellowship (Summer–Fall 2025) and is primarily a **measurement and feasibility exercise**, rather than a completed valuation or causal study.

---

## Project Overview

Patent ownership transfers are common, but empirical work typically focuses on firm-level mergers or patent grants rather than **portfolio-level patent transactions**. This project investigates whether it is possible to:

1. Identify large patent portfolio transfers at scale.
2. Link these transfers to public firms where possible.
3. Recover or approximate the economic magnitude of such transfers using available data.

The project begins with an attempt to recover **transaction prices** for patent portfolios and documents why this is difficult in practice. It then pivots to constructing a clean dataset of patent portfolio transfers and characterizing their size, timing, and implied value using established patent value proxies.

---

## Data Sources

This project relies exclusively on publicly available data:

### USPTO Patent Assignment Data (Bulk)
Used as the backbone of the analysis to observe legal patent ownership transfers.

Source:  
https://www.uspto.gov/ip-policy/economic-research/research-datasets/patent-assignment-dataset

Files used:
- `assignment.csv`
- `assignee.csv`
- `assignor.csv`
- `assignment_conveyance.csv`
- `documentid.csv`

These files are used to reconstruct reassignment events and cluster them into candidate patent portfolio transfers.

### SEC EDGAR Filings
Used to investigate whether firms disclose patent portfolio transactions and prices in regulatory filings and exhibits (8-K, 10-K, 10-Q).

### KPSS Patent Value Data
Used to proxy for the economic magnitude of transferred patent portfolios when transaction prices are not observable.

Source:  
https://github.com/KPSS2017/Technological-Innovation-Resource-Allocation-and-Growth-Extended-Data/tree/master

---

## Code

### Notebook: USPTO Reassignment Clustering
**`notebooks/hart.html`**

This notebook:
- Loads and merges USPTO reassignment data.
- Cleans and normalizes assignor and assignee names.
- Clusters reassignment events by seller, buyer, and execution-date windows.
- Identifies large clusters of patent transfers interpreted as candidate patent portfolio transactions.
- Links transferred patents to KPSS patent value measures.
- Produces summary statistics and exploratory data analysis of portfolio size, value, and timing.

This notebook produces the core dataset used in the project.

---

### Notebook: SEC and Exhibit Screening
**`notebooks/hart_news.html`**

This notebook:
- Takes candidate patent portfolio transfers identified from USPTO data.
- Matches sellers and buyers to public firms where possible.
- Retrieves nearby SEC filings for those firms.
- Screens filings and exhibits for asset purchase language and price disclosures.
- Attempts to recover explicit patent or IP transaction prices.
- Explores the feasibility of supplementing SEC data with external news sources.

A key outcome of this notebook is a documented limitation: even when patent portfolio transfers are observable, explicit transaction prices are rarely disclosed in public filings or news sources.

---

## Output Files

The notebooks generate several intermediate and final outputs which are under the main branch

## What This Project Does and Does Not Do

**What it does:**
- Constructs a novel dataset of large-scale patent portfolio transfers.
- Demonstrates how USPTO reassignment data can be used to identify portfolio-level transactions.
- Documents the limits of SEC filings and news sources for recovering patent transaction prices.
- Provides exploratory evidence on the size and implied value of patent portfolio transfers.

**What it does not do (yet):**
- Recover reliable transaction prices for most patent portfolios.
- Estimate causal effects or conduct valuation analysis.
- Replace existing patent value measures such as KPSS.

---

## Current Status and Future Directions

At its current stage, the project establishes what can and cannot be measured using standard public data. Future progress would require additional data sources, such as structured news databases or alternative accounting-based measures (e.g., changes in intangible assets), to move beyond descriptive analysis.

---

## Notes on Data Availability

Raw USPTO and KPSS input files are not included in this repository due to size constraints. Users should download the original datasets directly from the sources listed above and adjust file paths accordingly.
