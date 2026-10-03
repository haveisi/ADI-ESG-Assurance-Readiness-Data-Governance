# Project Visuals

This folder contains the screenshots I use to show the main results of the project without opening the Databricks notebooks.

## Gold reconciliation

This screenshot shows the final comparison between the reporting-eligible Silver population and the Gold reporting output.

The reconciliation returned **PASS**, which means the Gold result agrees with the records approved for reporting.

![Gold reconciliation](gold-reconciliation.png)

## Reporting eligibility

This screenshot shows the reporting gate used before data moves into Gold.

```text
Open exception → HOLD
No open exception → ELIGIBLE
```

In this synthetic case:

```text
72 remediated records
61 ELIGIBLE
11 HOLD
```

Only the ELIGIBLE records were included in the Gold reporting output.

![Reporting eligibility](reporting-eligibility.png)

## Assurance-readiness summary

This screenshot shows the final control summary grouped under the assurance-readiness areas used in the project.

I use this view to see where controls passed, where findings remain open, and where there was not enough evidence to assess an area.

![Assurance readiness summary](assurance-readiness-summary.png)

## Note

These screenshots come from the synthetic Databricks case study I built for this project.

They are not Analog Devices internal dashboards, systems, controls, or assurance results.
```

Your `assets` folder should now look like:

```text
assets/
├── README.md
├── gold-reconciliation.png
├── reporting-eligibility.png
└── assurance-readiness-summary.png
