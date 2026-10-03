# Synthetic Data
The files in this folder are synthetic and were created for this ESG assurance-readiness case study.

They do not represent Analog Devices' actual suppliers, procurement transactions, internal controls, emission factors, or assurance evidence.

The purpose of the dataset is to demonstrate how Scope 3 supplier and procurement data can be validated, controlled, remediated, and reconciled before reaching a reporting-ready output.

## Files
### `raw_supplier_procurement.csv`
Synthetic transaction-level procurement data used as the starting population for the Bronze layer.

It includes fields such as supplier, spend, currency, Scope 3 category, calculation method, emission factor, and calculated emissions.

### `supplier_master.csv`
Synthetic supplier reference data used to test supplier traceability, country consistency, and master-data controls.

### `category_mapping.csv`
Controlled mapping used to test whether procurement records are assigned to the appropriate Scope 3 category.

### `emission_factor_master.csv`
Synthetic emission-factor reference table used to test factor status, version, unit consistency, and calculation logic.

### `evidence_register.csv`
Synthetic evidence register used to test whether supplier-specific calculations are supported by traceable documentation.

## Data Quality Testing
The dataset intentionally contains selected control exceptions so that the assurance workflow can test:

- duplicate transactions
- missing supplier identifiers
- supplier master-data inconsistencies
- reporting-period cutoff
- Scope 3 classification
- FX recalculation
- emissions reperformance
- retired or unapproved emission factors
- factor-unit mismatches
- missing supplier-specific evidence
- manual override approval

These exceptions are used only for training and demonstration.

## Important Note
A separate planted-error key was used during development and is not included in this public repository.

This project is intended to demonstrate ESG data governance and assurance-readiness methods, not to reproduce ADI's reported Scope 3 inventory.
