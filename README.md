## Credit Card Fraud Risk Analysis Pipeline
`Tech Stack:` Python, PySpark, Google Cloud Storage (GCS), GCP Dataproc Serverless, GCP BigQuery, GCP Composer (Airflow)

## Project Overview
This project focuses on processing daily credit card transactions to detect potential fraudulent activities. The pipeline is built using Apache Airflow (GCP Composer) to orchestrate data ingestion, transformation, and storage using GCP Dataproc Serverless and BigQuery.

## Architecture Workflow

`1️. Data Ingestion`
A static table of cardholders exists in BigQuery.
Daily transaction files are uploaded to a GCS bucket in a /transactions folder.

`2️. Orchestration with Airflow`
The FileSensor Operator detects new files in the transactions folder.
Once a new file is available, Airflow triggers a Dataproc Serverless job.

`3️. Processing with PySpark`
The PySpark job is executed on the dataproc serverless, which performs data quality and completeness checks, transformations and data enrichment by joining the transformed transactions data with the cardholder data.
Fraud risk is analyzed based on predefined rules.
The processed data is stored in BigQuery.

`4️. Archiving`
Once processed, the transaction file is moved to an archive folder in GCS.
