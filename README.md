# ADI ESG Assurance Readiness & Data Governance

I built this project around a question I kept coming back to in ESG reporting:

**What has to happen behind the scenes before a Scope 3 number is ready to be trusted, reviewed, or assured?**

I used Analog Devices (ADI) as the public case context because its ESG reporting provides enough information to study upstream Scope 3 emissions, supplier data, calculation methods, and assurance.

The transaction-level data in this repository are synthetic. I created them only to test the workflow. They are not ADI internal data.

## Project at a glance

**Focus:** Scope 3 Category 1 and Category 2

**Tools:** Databricks, SQL, Delta tables, synthetic supplier and procurement data

**Main control areas:** supplier traceability, duplicates, cutoff, classification, FX, emission factors, evidence, manual overrides, and reconciliation

**Result:**

```text
73 source records
→ 72 after duplicate remediation
→ 61 ELIGIBLE
→ 11 HOLD
→ Gold reconciliation: PASS
```

![Reporting eligibility](assets/reporting-eligibility.png)

## What I built

The project follows a Bronze–Silver–Gold structure in Databricks.

```text
Synthetic supplier and procurement data
        ↓
Bronze
        ↓
Silver validation and control checks
        ↓
Exception review and remediation
        ↓
Reporting eligibility
        ↓
Gold reporting output
        ↓
Source-to-disclosure reconciliation
        ↓
Assurance workpapers and findings
```

The idea was simple: keep the original source data intact, test it, document exceptions, correct issues through a controlled process, and only allow supported records into the reporting layer.

## Scope

I focused on two upstream Scope 3 categories:

- Category 1 — Purchased Goods and Services
- Category 2 — Capital Goods

These categories are useful for this exercise because the calculation depends on several things working together: supplier information, spend data, classification, emission factors, calculation logic, and supporting evidence.

## Controls I tested

I built checks for:

- duplicate transactions
- missing supplier IDs
- supplier country mismatches
- reporting-period cutoff
- incorrect Scope 3 classification
- FX calculation errors
- emissions calculation differences
- retired or unapproved emission factors
- emission-factor unit mismatches
- missing supplier-specific evidence
- manual overrides without approval

When a record failed a control, I did not simply remove it.

I created an exception, reviewed the issue, and either remediated it or kept the record on hold.

One of the main lessons for me was that a control failure and a confirmed misstatement are not the same thing.

## Reporting eligibility

Before data could move into Gold, I added a reporting eligibility check.

```text
Open exception → HOLD
No open exception → ELIGIBLE
```

In the synthetic dataset:

```text
73 source records
72 after duplicate remediation
61 ELIGIBLE
11 HOLD
```

Only ELIGIBLE records were included in the Gold reporting output.

![Reporting eligibility](assets/reporting-eligibility.png)

The HOLD records remained visible for further review rather than disappearing from the process.

## Gold reconciliation

The final reporting control compared the eligible Silver population with the Gold output.

```text
Eligible Silver emissions = Gold emissions
```

For this case, the reconciliation returned:

**PASS**

![Gold reconciliation](assets/gold-reconciliation.png)

The PASS result means the final Gold output agrees with the records approved for reporting.

It does not mean every source record passed every control.

## Assurance workpapers

I also built a simple assurance workpaper structure around:

```text
Assertion
→ Risk
→ Control
→ Test
→ Evidence
→ Result
→ Conclusion
```

This changed how I looked at the data.

Instead of only asking, "Did the calculation run?", I started asking:

- Can I reproduce the number?
- Can I trace it back to the source?
- Was the correct method used?
- Is there evidence behind it?
- Were exceptions reviewed?
- Is there an approval trail?
- Can someone else understand what changed and why?

## Assurance-readiness view

For the final summary, I mapped selected controls to the five areas used in the KPMG ESG Assurance Maturity Index:

- Governance
- Skills
- Data Management
- Digital Technology
- Value Chain

I use those areas only as a reference structure.

This project is not a KPMG assessment and does not calculate a KPMG maturity score.

I also left the Skills area unassessed because the project does not provide evidence about staff training or competency.

![Assurance readiness summary](assets/assurance-readiness-summary.png)

## Repository contents

```text
notebooks/
    01_bronze_ingestion.ipynb
    02_silver_validation.ipynb
    03_gold_reporting.ipynb
    04_assurance_workpaper.ipynb
    05_executive_assurance_dashboard.ipynb

data/
    synthetic/
        raw_supplier_procurement.csv
        supplier_master.csv
        category_mapping.csv
        emission_factor_master.csv
        evidence_register.csv

docs/
    methodology.md
    control-framework.md
    assurance-findings.md
    sources.md

assets/
    reporting-eligibility.png
    gold-reconciliation.png
    assurance-readiness-summary.png
```

## Why this project matters to me

My main interest in ESG data is moving beyond reporting alone.

A sustainability number becomes much more useful when I can explain:

- where it came from
- what rules were applied
- what failed
- what was corrected
- what evidence supports it
- and whether the final number can be reproduced

That is what I wanted to practice with this project.

The part I found most useful was moving from a reporting mindset to an assurance-readiness mindset: not just producing the number, but being able to defend the process behind it.

## Disclaimer
This is an independent portfolio project.
Analog Devices did not sponsor, provide internal data for, or review this work.
All transaction-level data in the repository are synthetic. Public ADI reports are used only as external case context.
