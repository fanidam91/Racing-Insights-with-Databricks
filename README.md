🏎️ Formula 1 Racing Analytics Using Azure Databricks
📌 Project Overview

The goal of this project is to build an end-to-end data engineering and analytics solution for Formula 1 race results using Azure Databricks. The solution ingests race data from the Ergast Developer API
, processes it in a Lakehouse architecture, and delivers insights such as driver standings, constructor standings, and team dominance trends.

This project demonstrates how to design an ETL pipeline with Azure Data Factory (ADF), transform data using Azure Databricks (PySpark + SQL), store data in Azure Data Lake Gen2, and create interactive reports in Power BI.

🏁 Formula 1 Context

Formula 1 (F1) is the world’s premier single-seater racing competition governed by the FIA. Each season:

Consists of 20–23 races (“Grands Prix”) hosted worldwide.

Each of the 10 teams fields 2 drivers.

Races are typically 50–70 laps, depending on the circuit.

Qualifying sets the starting grid.

Driver Standings and Constructor Standings are updated after each race.

🏗️ Solution Architecture
Azure Resources Used
<img width="1416" height="727" alt="image" src="https://github.com/user-attachments/assets/2982505a-f4d2-4b29-a076-77fbb83c1a28" />


<img width="4284" height="2684" alt="image" src="https://github.com/user-attachments/assets/bad13b43-ddb5-4ebe-bfcf-27e018e41311" />

Azure Data Lake Gen2 → Raw (Bronze), Standardized (Silver), and Analytical (Gold) storage layers.

Azure Databricks → Data transformation with PySpark & SQL.

Delta Lake → Incremental loads, ACID transactions, history & time travel.

Azure Data Factory → Orchestration and scheduling of pipelines.

Azure Key Vault → Secure storage for secrets.

Power BI → Visualization and reporting.

Architecture Flow:

Data ingested from Ergast API into Bronze (raw).

Databricks transforms data into Delta tables with schema enforcement and audit columns → stored in Silver.

Aggregations, joins, and fact/dimension modeling → stored in Gold.

Power BI dashboards visualize standings, team dominance, and race analytics.

🔄 ETL Pipeline
1. Ingestion (Bronze → Silver)

Reads JSON & CSV from Ergast API (Drivers, Constructors, Races, Circuits, Results, PitStops, LapTimes, Qualifying).

Applies schema, renames headers, drops unused columns.

Adds audit columns: ingestion_date, file_source, file_date.

Stores in Delta tables for incremental processing.

2. Transformation (Silver → Gold)

Deduplicates records and enforces data quality rules.

Joins datasets (drivers, constructors, results, circuits).

Creates fact tables (race results, lap times, pit stops) and dimension tables (drivers, constructors, circuits).

Uses window functions for driver/constructor standings.

Saves final analytical tables in Parquet/Delta format.

📊 Reporting & Analytics

Delivered via Databricks SQL + Power BI:

Driver Standings per season.

Constructor Standings per season.

Dominant Drivers and Teams across decades.

Interactive dashboards showing race performance, pit stop efficiency, and historical comparisons.

📅 Scheduling & Monitoring

ADF pipelines scheduled every Sunday at 10 PM.

Pipelines skip automatically if no race occurred that week.

Triggers use file_date as a parameter (tumbling window).

Alerts and monitoring configured for failures.

✅ Project Requirements Met
Data Ingestion

Ingested 8 datasets into Azure Data Lake Gen2.

Schema applied uniformly across all files.

Audit columns added.

Stored in columnar format (Parquet/Delta).

Incremental ingestion logic implemented.

Data Transformation

Created fact & dimension models.

Joins and aggregations implemented.

Audit columns retained.

Stored in Delta format.

Incremental load patterns implemented.

Reporting

Driver and Constructor Standings created.

Analysis of dominant drivers/teams.

Power BI dashboards for interactive reporting.

Analysis

Used PySpark & Spark SQL for queries.

Window functions (ranking, aggregations).

Dashboards in Databricks and Power BI.

Scheduling

Automated weekly ADF pipelines.

Monitoring, re-run capability, and alerting enabled.

Non-Functional

Delete individual records (Delta DELETE).

History & Time Travel supported (Delta).

Rollback to previous versions possible.

🔧 Tasks Performed

Built solution architecture using ADF, Databricks, ADLS, Delta Lake, and Power BI.

Created Databricks notebooks for ingestion & transformation.

Managed Databricks clusters, pools, and jobs.

Implemented secrets-based storage mounts via Key Vault.

Used PySpark for ingesting CSV/JSON → Delta tables.

Used Spark SQL for aggregations, joins, and modeling.

Implemented incremental load and time travel with Delta Lake.

Created Power BI dashboards connected to Gold layer.

🛠️ Tech Stack
Languages: PySpark, SQL

Databricks: Clusters, Notebooks, DBFS, Delta Lake

Azure: ADLS Gen2, ADF, Key Vault, Databricks

Visualization: Power BI
🚀 Future Enhancements

Add streaming ingestion with Kafka + Structured Streaming.

Deploy ML models in Databricks for race outcome prediction.

Automate dashboard publishing in Power BI Service.
\
Visualization: Power BI
