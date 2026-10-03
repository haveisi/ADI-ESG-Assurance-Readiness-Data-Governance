# Assurance Findings
This page summarizes the main issues I found while testing the synthetic Scope 3 dataset.

The goal was not to produce a perfect dataset. I intentionally kept selected issues in the population so I could test whether the workflow could detect them, document them, and prevent unresolved records from moving into the reporting layer.

## Summary

The main findings fell into four areas:

1. source-data quality
2. calculation and emission-factor controls
3. supporting evidence
4. approval and governance

Some findings affected only one transaction. Others affected several records.

I treated each finding as something to investigate rather than assuming every control failure was a confirmed misstatement.

## Findings

| Finding | What I found | Why it matters | Status |
|---|---|---|---|
| Missing supplier ID | One transaction could not be linked to a supplier record | Breaks supplier traceability | Open |
| Supplier country mismatch | Transaction country did not agree with supplier master data | Could affect data quality and factor selection | Open |
| Reporting-period cutoff | One transaction was assigned to FY2025 even though the invoice date fell outside the period | Could place activity in the wrong reporting year | Open |
| Scope 3 classification | One record did not agree with the expected category mapping | Can distort Category 1 or Category 2 totals | Open |
| FX recalculation | One converted spend amount could not be reproduced from source amount and FX rate | Spend-based emissions depend on the converted spend | Open |
| Emissions recalculation | Several records did not reproduce using the stated inputs and factor | Directly affects reported emissions | Open |
| Retired emission factor | One record used a factor that was no longer approved for use | Can create methodology inconsistency | Open |
| Factor-unit mismatch | One transaction used an emission-factor unit that did not match the expected calculation basis | Can create a material calculation error | Open |
| Missing supplier evidence | Supplier-specific calculations were not always supported by an evidence record | Weakens traceability and reviewability | Open |
| Manual override | One adjusted value did not have completed approval evidence | Manual changes need clear authorization | Open |
| Duplicate transaction | The same transaction ID appeared twice in the source population | Could overstate spend and emissions | Remediated |

## Duplicate finding

The duplicate transaction was the only issue I fully remediated in the exercise.

Both source records remained unchanged in Bronze.

In Silver, I:

- identified the duplicate,
- documented the issue,
- selected the duplicate physical record for exclusion,
- created a remediated population,
- reran the duplicate test.

The retest returned no remaining duplicate transaction IDs.

This reduced the population from:

```text
73 source records
to
72 remediated records
```

I kept the original source records so the correction remained visible.

## Open findings and reporting eligibility

I did not force unresolved records into the reporting output.

The reporting rule was:

```text
Open assurance exception → HOLD
No open assurance exception → ELIGIBLE
```

After applying that rule:

```text
72 remediated records
61 ELIGIBLE
11 HOLD
```

Only the 61 eligible records were used in the Gold reporting output.

## What I would investigate next

If this were a live reporting process, my next priority would be the findings that can directly change the emissions result.

I would first review:

- emissions recalculation differences,
- emission-factor unit mismatch,
- retired factor usage,
- FX differences,
- unsupported supplier-specific calculations.

After that, I would work through the classification, cutoff, master-data, and approval issues.

The sequence matters because not every exception has the same reporting impact.

## A useful lesson from the exercise

One thing that became clearer to me while building the findings register is that data quality is not only about whether a field is populated.

For assurance purposes, I also need to know:

- where the value came from,
- whether the method is appropriate,
- whether the calculation can be reproduced,
- whether evidence exists,
- whether someone reviewed an exception,
- and whether the final output can be traced back to the source.

That is why I kept the exception log separate from the final reporting table.

## Assurance perspective

Research on ESG assurance and internal audit emphasizes the importance of internal controls, data validation, governance, and review before information reaches external assurance.

That idea shaped this part of the project.

I wanted the findings register to show not only what failed, but also whether the issue was:

- still open,
- remediated,
- retested,
- or safe to include in reporting.

## Limitation

These findings come from a synthetic training dataset.

They do not describe Analog Devices' actual data quality, controls, suppliers, or assurance findings.
```

Use this commit message:

```text
Document assurance findings and remediation status
