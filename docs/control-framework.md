# Control Framework

I built these controls by asking a practical question:

**What could make a Scope 3 number difficult to trust, reproduce, or assure?**

That led me to focus on the points where errors can enter the process: source data, supplier information, classification, emission factors, calculations, evidence, manual adjustments, and the final reporting output.

The controls are simple by design. Each one should answer a clear question and leave enough evidence for someone else to review the result.

## Controls used in this project

| Control area | Question I tested | Why I care about it |
|---|---|---|
| Duplicate transactions | Has the same transaction entered the population more than once? | A duplicate can overstate both spend and emissions. |
| Supplier ID | Can the transaction be linked to a known supplier? | Without a supplier ID, traceability breaks. |
| Supplier country | Does the transaction agree with the supplier master record? | Country differences can point to a master-data problem or incorrect factor selection. |
| Reporting cutoff | Does the transaction belong in the reporting year? | A valid transaction can still be reported in the wrong period. |
| Scope 3 category | Is the transaction mapped to the right Scope 3 category? | Misclassification can distort both the category total and the explanation behind it. |
| FX conversion | Can the reported USD spend be reproduced from the original amount and FX rate? | Spend-based emissions depend directly on the converted spend value. |
| Emissions recalculation | Can I reproduce the emissions result using the stated method and factor? | If I cannot rerun the calculation, I cannot rely on the output. |
| Emission factor status | Is the factor approved and current? | Old or retired factors can introduce avoidable calculation risk. |
| Factor unit | Does the factor unit match the transaction calculation? | A correct factor used with the wrong unit can still produce a wrong result. |
| Supplier evidence | Is supplier-specific data supported by evidence? | Primary data is more useful when I can trace where it came from and what period it covers. |
| Manual override | Was the adjustment explained and approved? | Manual changes need a clear reason and review trail. |
| Reconciliation | Does Gold agree with the reporting-eligible Silver population? | This is my final check that the reporting layer is complete and consistent. |

## How I treated a failed control

I did not treat every failed control as a confirmed misstatement.

A failure means:

**something needs to be reviewed.**

My workflow was:

```text
Control fails
        ↓
Exception created
        ↓
Issue investigated
        ↓
Evidence reviewed
        ↓
Remediation documented
        ↓
Control retested
        ↓
ELIGIBLE or HOLD
```

This distinction matters because a missing field, a duplicate, and a true emissions error are not the same problem.

The exception log keeps that difference visible.

## Example: duplicate transaction

The synthetic dataset contained two physical records with the same transaction ID.

The first reaction could have been to delete one row.

I did not do that.

Instead, I:

1. preserved both original records in Bronze,
2. identified the duplicate in Silver,
3. logged the issue as an exception,
4. compared the two records,
5. documented which record should be excluded,
6. created the remediated Silver population,
7. reran the duplicate test.

The original evidence stayed unchanged, while the reporting population showed the remediation.

That is the behavior I wanted from the pipeline.

## Example: supplier-specific emissions

Supplier-specific data can look stronger than spend-based estimates, but I did not want to accept it only because the method field said "supplier-specific."

I also checked whether supporting evidence existed.

If the method was supplier-specific but the evidence was missing, the record failed the control and was held for review.

For me, this is an important assurance lesson:

**better data is not just a more precise number; it also needs a traceable basis.**

## Example: recalculation

I also reperformed the emissions calculation rather than accepting the reported value.

The basic test was:

```text
Reported emissions
versus
Recalculated emissions from source inputs
```

A difference does not automatically tell me why the number is wrong.

It tells me where to investigate next:

- spend,
- FX,
- factor,
- unit,
- method,
- or manual adjustment.

## Why these controls matter for assurance

The controls are not only data-cleaning rules.

They help answer questions an assurer or internal reviewer would ask:

- Where did this number come from?
- Can I reproduce it?
- Was the right method used?
- Is there evidence behind it?
- Were exceptions reviewed?
- Were manual changes approved?
- Can the final disclosure be traced back to the source population?

Research on ESG assurance makes a similar point: stronger reporting depends on robust systems, controls, risk assessment, and data validation, and internal audit can play a useful role in testing those areas before external assurance. 

## Metric-level thinking

One idea I found especially useful from the assurance literature is that ESG assurance is often metric-specific.

Gipper, Ross, and Shi (2025) examined ESG assurance among S&P 500 firms and found substantial variation in which ESG metrics were assured, the level of assurance obtained, the assurance standards used, and the type of assurance provider.

That helped shape how I approached this project.

I did not treat "ESG assurance" as one broad yes/no condition.

Instead, I tested specific Scope 3 records, calculations, evidence, controls, and reporting outputs.

This is especially relevant for environmental metrics because the study found that firms increasingly assured individual environmental measures, including greenhouse-gas metrics.

Source: Gipper, Ross, and Shi (2025), *ESG assurance in the United States*, Review of Accounting Studies.

## Limited assurance mindset

For this project, I also tried to think in a limited-assurance mindset.

That does not mean proving that every transaction is perfect.

It means building enough traceability, testing, evidence, and control documentation to identify material problems and support a defensible conclusion.

The assurance literature distinguishes limited assurance from reasonable assurance partly by the extent of testing and evidence gathered. I use that distinction as context, not as a claim that this portfolio project itself provides external assurance.

## Final reporting gate

The final control is simple:

```text
Open exception → HOLD
No open exception → ELIGIBLE
```

Only ELIGIBLE records move into Gold.

This gives me a clear line between:

**data available for reporting**

and

**data still requiring investigation.**

That separation is one of the most useful things I built in this project.

## Important limitation

These controls were created by me for a synthetic portfolio case.

They are not Analog Devices' internal controls and should not be interpreted as a reconstruction of ADI's control environment.
