# Methodology

I built this project around one simple idea:

**A Scope 3 number should be traceable from the source data all the way to the final reporting output.**

To test that, I used a Bronze–Silver–Gold structure in Databricks.

## Bronze

Bronze keeps the original synthetic source data.

I added basic ingestion metadata, but I did not change the source values.

The purpose of this layer is to preserve the original record and make the lineage clear.

## Silver

Silver is where I tested the data.

The checks included:

- duplicate transactions
- missing supplier IDs
- supplier-country mismatch
- reporting-period cutoff
- Scope 3 category mapping
- FX recalculation
- emissions recalculation
- emission-factor status
- factor-unit consistency
- supplier-specific evidence
- manual override approval

If a record failed a check, I flagged it. I did not automatically delete it.

## Exception and remediation

Failed controls were written into an exception log.

I treated a failed control as something that needs review, not automatically as a confirmed error.

For the duplicate case, I:

1. identified the duplicate,
2. compared the two physical records,
3. selected the record to exclude,
4. kept the original Bronze data unchanged,
5. created a remediated Silver population,
6. retested the control.

That gave me a clear audit trail of what changed and why.

## Reporting eligibility

Before data moves to Gold, I check whether a transaction still has an open exception.

Each record is classified as:

- `ELIGIBLE`
- `HOLD`

Only ELIGIBLE records are used in the Gold reporting output.

The HOLD records stay visible until the issue is resolved.

## Gold

Gold contains the reporting-ready results for:

- Scope 3 Category 1 — Purchased Goods and Services
- Scope 3 Category 2 — Capital Goods

The output includes transaction count, supplier count, spend, and emissions.

## Reconciliation

The final control is a reconciliation between eligible Silver and Gold.

```text
Eligible Silver emissions = Gold emissions
```

For this synthetic case, the reconciliation returned:

**PASS**

## Assurance review

After the data pipeline was complete, I created assurance workpapers for the main controls.

Each workpaper connects:

```text
Risk
→ Control
→ Test
→ Evidence
→ Result
→ Conclusion
```

This helped me review the project from an assurance perspective rather than only as a data pipeline.

## Readiness view

I also grouped selected controls under the five areas used in the KPMG ESG Assurance Maturity Index:

- Governance
- Skills
- Data Management
- Digital Technology
- Value Chain

I use these only as a reference structure. I do not calculate a KPMG maturity score.

## Limitation

All transaction-level data in this project are synthetic.

The project is designed to demonstrate the process and controls, not to reproduce Analog Devices' internal Scope 3 inventory.
