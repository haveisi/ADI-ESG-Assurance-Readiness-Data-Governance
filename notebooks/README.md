# Databricks Notebooks

This folder contains the analytical workflow for the ESG assurance-readiness case study.

## Notebook Sequence

1. `01_bronze_ingestion.ipynb`  
   Loads and preserves the synthetic source data.

2. `02_silver_validation.ipynb`  
   Applies data-quality checks, methodology controls, evidence checks, and exception logic.

3. `03_gold_reporting.ipynb`  
   Creates governed reporting outputs and reconciliation results.

4. `04_assurance_workpaper.ipynb`  
   Builds the structured assurance workpaper connecting records, controls, evidence, exceptions, and conclusions.

5. `05_executive_assurance_dashboard.ipynb`  
   Summarizes reporting eligibility, findings, and overall assurance readiness.

The notebooks are designed as a portfolio demonstration using synthetic data.
