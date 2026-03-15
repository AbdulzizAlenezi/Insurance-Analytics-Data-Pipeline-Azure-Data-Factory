# Insurance-Analytics-Data-Pipeline-Azure-Data-Factory

This repository showcases an enterprise‑ready data engineering solution built on Azure Data Factory (ADF) for processing insurance claims and policy data. The project demonstrates how cloud‑native orchestration, scalable transformations, and structured data modeling can be used to deliver KPI‑ready datasets for analytics and reporting.

1. Business Overview
Insurance companies depend on accurate, timely insights to evaluate portfolio performance, understand risk exposure, and support operational decision‑making. This solution transforms raw operational data into curated KPI outputs that support:

Claims cost monitoring

Premium distribution analysis

Product‑level performance insights

Downstream dashboarding (e.g., Power BI)

The project reflects real‑world data engineering patterns used in modern insurance analytics platforms.

2. Solution Architecture
High‑Level Architecture Diagram
Code


                ┌──────────────────────────┐
                │   Source CSV Files       │
                │ (Claims, Policies, etc.) │
                └─────────────┬────────────┘
                              │
                              ▼

                ┌──────────────────────────┐
                │ Azure Data Lake Storage  │
                │        RAW Layer         │
                └─────────────┬────────────┘
                              │
                              ▼

                ┌──────────────────────────┐
                │  ADF Ingestion Pipelines │
                │ (001_insurance_data_*)   │
                └─────────────┬────────────┘
                              │
                              ▼

                ┌──────────────────────────┐
                │ Azure Data Lake Storage  │
                │      STAGING Layer       │
                └─────────────┬────────────┘
                              │
                              ▼

                ┌──────────────────────────┐
                │   ADF Data Flows         │
                │ (KPI Transformations)    │
                └─────────────┬────────────┘
                              │
                              ▼
                ┌──────────────────────────┐
                │ Azure Data Lake Storage  │
                │      CURATED Layer       │
                └─────────────┬────────────┘
                              │
                              ▼

                ┌──────────────────────────┐
                │  Analytics & Reporting   │
                │     (Power BI, etc.)     │
                └──────────────────────────┘


Key Azure Components
Azure Data Factory – Orchestration, ingestion, and transformation

Azure Data Lake Storage (ADLS) – Raw, staging, and curated data layers

ADF Data Flows – Scalable transformations for KPI computation

ARM Templates – CI/CD‑ready deployment artifacts

3. Pipelines

001_insurance_data_pipeline
Ingests raw claims and policy data from ADLS input into the staging layer. Ensures schema consistency and prepares data for downstream transformations.

002_insurance_kpi_dashboarding
Executes KPI‑oriented dataflows to compute curated outputs such as claim amounts and premium amounts by policy type.

Insurance_Master_Data_Pipeline
Coordinates the full end‑to‑end workflow, combining ingestion and KPI computation into a single orchestrated process.

4. Datasets

Raw Layer
adls_input – Raw CSV input files

Staging Layer
adls_stg_claims – Standardized claims data

adls_stg_policies – Standardized policy data

adls_stg – General staging dataset

Curated Layer
adls_claim_amount_kpi_parquet – KPI output for claim amounts

kpi_2_policytype_premium_amount_kpi_csv – KPI output for premium amounts by policy type

5. Data Flows


kpi_1_claim_amount
Computes aggregated claim KPIs, including:

Total claim amount

Average claim amount

Claim count

Claim amount by date or category

kpi_2_policy_type_premium_amount1
Calculates premium KPIs grouped by policy type:

Total premium amount

Average premium per policy

Premium distribution across product lines

These transformations follow best practices for partitioning, schema drift handling, and scalable transformation design.

6. KPI Definitions
Claim Amount KPIs
Total Claim Amount – Sum of all claim payouts

Average Claim Amount – Mean payout per claim

Claim Frequency – Number of claims in a period

Loss Ratio (optional) – Claims / Premiums

Premium KPIs
Total Premium Amount – Sum of all premiums written

Premium by Policy Type – Product‑level revenue

Average Premium – Mean premium per policy

Premium Growth (optional) – Period‑over‑period change

These KPIs support underwriting, pricing, and portfolio management.

7. Repository Structure
Code
azure-datafactory-insurance-kpi/


- README.md

- architecture/
      - architecture-diagram.png
      - dataflow-diagram.png



- pipelines/
  - 001_insurance_data_pipeline.json
  - 002_insurance_kpi_dashboarding.json
  - Insurance_Master_Data_Pipeline.json



- datasets/
  - adls_input.json
  - adls_stg_claims.json
  - adls_stg_policies.json
  - adls_claim_amount_kpi_parquet.json
  - kpi_2_policytype_premium_amount_kpi_csv.json



- dataflows/
  - kpi_1_claim_amount.json
  - kpi_2_policy_type_premium_amount1.json


-  sample-data/
  -  claims.csv
  -  policies.csv
  -  pi_output_example.csv

    
8. Governance & Operational Design
Clear separation of raw, staging, and curated layers

Parameterized pipelines for reusability

Modular datasets for consistent schema management

ARM‑template export support for CI/CD

Lineage from ingestion to KPI outputs

Scalable transformations using ADF Data Flows

This structure supports maintainability, auditability, and enterprise‑level scalability.

9. Business Value
This project demonstrates capabilities that matter to enterprise data teams:

Cloud‑native data engineering on Azure

End‑to‑end orchestration and transformation

KPI‑driven business logic

Scalable and maintainable architecture

Realistic insurance analytics scenario
