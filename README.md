# Systamatic_Solvers---Bike-Rental-Insights

Bike Rental Data Insights (Snowflake Project)
📌 Overview

This project implements an end-to-end data pipeline for a bike rental system using Snowflake. It processes raw data from AWS S3, performs data validation, applies transformations, maintains historical data using SCD Type 2, and generates KPIs for analytics and visualization.

🎯 Project Objectives

Build a scalable ETL pipeline in Snowflake

Clean and validate raw data

Implement SCD Type 2 for historical tracking

Generate business KPIs

Prepare data for dashboards

🏗️ Architecture
AWS S3 → RAW → VALIDATED → CURATED → KPI → DASHBOARD
📂 Dataset

The project uses the following datasets:

stations_master.csv / stations_inc.csv

bikes_master.csv / bikes_inc.csv

users_master.csv / users_inc.csv

rentals_master.csv / rentals_inc.csv

⚙️ Implementation Details
🔹 1. Data Ingestion

Created Stage to connect with AWS S3

Loaded data using COPY INTO

Used custom CSV file format

🔹 2. RAW Layer

Stores raw data without transformations

Includes metadata:

source_file_name

load_ts

🔹 3. Data Quality Checks

Invalid records stored in DQ_EXCEPTIONS

Validation rules:

Negative duration or distance

Missing user_id

Invalid battery levels

Incorrect timestamps

🔹 4. VALIDATED Layer

Deduplication using ROW_NUMBER()

Standardization (LOWER, UPPER)

Removes invalid records

🔹 5. CURATED Layer
📌 Dimension Tables (SCD Type 2)

DIM_USERS_SCD2

DIM_BIKES_SCD2

DIM_STATIONS_SCD2

Features:

Maintains historical records

Uses:

effective_from

effective_to

is_current

📌 Fact Table

FACT_RENTALS

Stores:

Rental transactions

Time attributes

Anomaly flags

Revenue metrics

🔥 Anomaly Detection

Anomalies are detected using:

Short trip detection

GPS mismatch

Zero battery rides

Device reuse fraud

Geofence violations

👉 Combined into anomaly_score

🔹 6. Automation

Stream → Tracks changes

Procedure → Refresh validated layer

Task → Runs automatically

🔹 7. Data Governance

Applied Dynamic Masking for:

Email

Phone

📊 KPIs Implemented
1️⃣ Anomalous Rental Probability

% of rentals with anomalies

2️⃣ Station Availability Score

% of successful rides per station

3️⃣ Active Rider Engagement Ratio

Active users (last 30 days) / total users

4️⃣ Fleet Maintenance Health Index

% of healthy bikes

5️⃣ Average Rental Revenue by Channel

Average revenue grouped by channel

📈 Visualization Tables

ALL_RIDES → Ride-level dataset

BIKE_INFO → Bike-level insights

KPI Views → Dashboard ready

🛠️ Tech Stack

Snowflake

SQL

AWS S3

🚀 Key Highlights

End-to-end ETL pipeline

SCD Type 2 implementation

Real-time automation

Data quality handling

Fraud detection using anomaly logic

Dashboard-ready outputs
