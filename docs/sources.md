# Sources

I used public materials from Analog Devices and KPMG to define the real-world context for this project.

The transaction-level data, controls, exceptions, and remediation workflow were created by me for the case study.

## Analog Devices

Main source library:

https://www.analog.com/en/corporate-responsibility/reports-library.html

The main documents I reviewed were:

- 2025 ESG Report
- FY2025 Assurance Statement
- ESG Disclosure Controls
- GHG Methodology
- Scope 3 Calculation Methodology
- Supplier Ethics Commitment
- Product Carbon Footprint Methodology
- Historical GHG data
- 2025 Annual Report

I used these materials to understand how ADI publicly describes its Scope 3 reporting, supplier data, emission factors, methodology, and assurance.

I did not use them to make claims about internal systems or controls that are not publicly disclosed.

## KPMG

I used the KPMG ESG Assurance Maturity Index 2025 as a reference for the assurance-readiness part of the project.

The five areas I used were:

- Governance
- Skills
- Data Management
- Digital Technology
- Value Chain

Source:

https://assets.kpmg.com/content/dam/kpmgsites/xx/pdf/2025/07/esg-assurance-maturity-index.pdf

I used these areas only to organize my own findings. I did not calculate a KPMG maturity score.

## What I created

The following parts of the project are my own case-study design:

- synthetic supplier and procurement data
- category and supplier master tables
- synthetic emission factors
- evidence register
- planted data-quality issues
- Bronze–Silver–Gold pipeline
- validation controls
- exception log
- remediation workflow
- reporting eligibility logic
- Gold reporting tables
- source-to-disclosure reconciliation
- assurance workpapers
- findings summary

These are not ADI internal data or processes.

## Important distinction

I kept the project separated into two parts:

**Public evidence**
- company reports
- methodologies
- assurance statements
- external assurance-readiness references

**Synthetic case design**
- transaction data
- controls
- exceptions
- remediation
- workpapers
- reporting outputs

That distinction is important because public reports can show what a company discloses, but they do not provide access to the underlying transaction data or complete internal control environment.

## ESG Assurance Research

Gipper, Brandon, Samantha Ross, and Shawn X. Shi.  
**“ESG assurance in the United States.”**  
*Review of Accounting Studies*, Volume 30, pages 1753–1803, 2025.  
Published online October 7, 2024.

DOI: 10.1007/s11142-024-09856-2

The study examines ESG assurance practices among S&P 500 firms from 2010–2020. It documents substantial variation in:

- which ESG metrics are assured,
- the level of assurance,
- assurance standards,
- and the type of assurance provider.

The paper is used in this project as background for treating ESG assurance as metric-specific rather than as a single company-wide yes/no condition.

## Disclaimer

This is an independent portfolio project.

Analog Devices and KPMG did not sponsor, review, or provide internal data for this work.

All transaction-level data in the repository are synthetic.
