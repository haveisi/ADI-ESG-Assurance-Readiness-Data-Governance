# ADI ESG Assurance Readiness & Data Governance

I built this project to understand a question that comes up often in ESG reporting:

**What has to happen behind the scenes before a Scope 3 number is actually ready to be trusted, reviewed, or assured?**

I used Analog Devices (ADI) as the public case context because its ESG reporting gives enough information to study upstream Scope 3 emissions, supplier data, calculation methods, and assurance.

The transaction-level data in this repository are synthetic. I created them only to test the workflow. They are not ADI internal data.

## What I built

The project follows a Bronze–Silver–Gold structure in Databricks.

```text
Synthetic supplier and procurement data
        ↓
Bronze
        ↓
Silver validation and control checks
        ↓
Exception management and remediation
        ↓
Reporting eligibility
        ↓
Gold reporting output
        ↓
Source-to-disclosure reconciliation
        ↓
Assurance workpapers and findings
```

The idea was to keep the original source data intact, test it, document exceptions, correct problems through a controlled process, and only allow supported records into the reporting layer.

## Scope

I focused on upstream Scope 3, especially:

- Category 1 — Purchased Goods and Services
- Category 2 — Capital Goods

These categories are useful for this type of exercise because the calculations depend on supplier information, spend data, classification, emission factors, and supporting evidence.

## Controls I tested

I built checks for issues such as:

- duplicate transactions
- missing supplier IDs
- supplier country mismatches
- reporting-period cutoff
- incorrect Scope 3 classification
- FX calculation errors
- emissions calculation differences
- expired or unapproved emission factors
- emission-factor unit mismatches
- missing supplier-specific evidence
- manual overrides without approval

When a record failed a control, I did not simply remove it.

I created an exception, reviewed the issue, and either remediated it or placed the record on hold.

One lesson from the project was that a control failure and a confirmed misstatement are not the same thing.

## Reporting eligibility

I added an eligibility step before Gold reporting.

Records with unresolved issues are marked:

`HOLD`

Records without unresolved issues are marked:

`ELIGIBLE`

Only eligible records are included in the Gold reporting output.

In the synthetic dataset, the flow was:

```text
73 source records
72 after duplicate remediation
61 reporting-eligible
11 held for unresolved exceptions
```

The Gold output reconciled back to the eligible Silver population, and the source-to-disclosure reconciliation returned:

**PASS**

That does not mean every record passed every control. It means the final reporting output can be traced back to the records that were approved for reporting.

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

This helped me look at the data differently.

Instead of only asking, “Did the calculation run?”, I started asking:

- Can I reproduce the number?
- Can I trace it back to evidence?
- Was the correct method used?
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

I also left the Skills area unassessed because this project does not provide evidence about staff training or competency.

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
```

## Why this project matters to me

My main interest in ESG data is moving beyond reporting alone.

A sustainability number is more useful when I can explain:

- where it came from
- what rules were applied
- what failed
- what was corrected
- what evidence supports it
- and whether the final number can be reproduced

That is what I wanted to practice with this project.

## Disclaimer

This is an independent portfolio project.

Analog Devices did not sponsor, provide internal data for, or review this work.

All transaction-level data in the repository are synthetic. Public ADI reports are used only as external case context.
