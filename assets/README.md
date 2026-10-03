# Project Visuals

I use this folder for a few visuals that help explain the project without having to open every notebook.

The visuals are meant to show the flow of the work, the main control points, and the final reporting results.

## Files I plan to keep here

### `architecture.png`

A simple view of how the data moves through the project:

```text
Synthetic source data
        ↓
Bronze
        ↓
Silver validation
        ↓
Exception review and remediation
        ↓
ELIGIBLE / HOLD
        ↓
Gold reporting
        ↓
Reconciliation
        ↓
Assurance workpapers
```

This is the main visual for the project.

### `gold-reconciliation.png`

A screenshot showing that the Gold reporting output reconciles to the eligible Silver population.

For this case:

```text
61 eligible records
→ Gold reporting output
→ reconciliation PASS
```

### `assurance-readiness-summary.png`

A screenshot of the final control summary, grouped into the assurance-readiness areas I used from the KPMG framework.

The purpose of this image is to show where controls passed, where findings remain open, and which areas were not assessed.

## Note

These visuals are based on the synthetic case study I created.

They are not ADI internal dashboards, systems, or assurance results.
