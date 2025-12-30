# Piedmont Hospital Patient Satisfaction Dashboard

![alt text](https://github.com/wii-nguyen/hospital_dashboard/blob/main/3.%20Dashboard%20visualization/hospital_dashboard.png "Hospital dashboard")

## 1. Business objective:
Piedmont Healthcare executives want to evaluate and improve patient experience across Piedmont hospitals in Georgia. They want to:
  1. Identify key drivers of patient satisfaction.
  2. Highlight hospital-level strengths and weaknesses that directly influence overall patient reception.
  3. Benchmark hospital-level performance against national and state standards.

This gives leadership a way to:
  * Monitor patient satisfaction performance across all Piedmont hospitals.
  * Identify where experience improvements will have the greatest ROI.
  * Track progress over time toward system-wide quality goals.
  * Support data-driven operational and strategic decisions.

## 2. Project objective:
To design and develop an interactive Power BI dashboard that consolidates Hospital Consumer Assessment of Healthcare Providers and Systems (HCAHPS) survey results, benchmarks, and YoY trends into a clear, actionable visualization suite. The dashboard allows executives to understand key drivers of patient satisfaction, compare performance across all Piedmont hospitals, and quickly identify areas requiring operational focus.

The dashboard will:
  * Display hospital-level scores for overall satisfaction and all major HCAHPS measures.
  * Highlight performance above/below national and state benchmarks.
  * Visualize year-over-year satisfaction improvement or decline.
  * Highlight key improvement areas for each hospital.

## 3. Datasets used:
Survey data for this dashboard is sourced from the Centers for Medicare & Medicaid Services (CMS) website. Every quarter, CMS releases HCAHPS public reporting files. These datasets capture standardized patient experience survey results for hospitals across the United States, including overall satisfaction ratings and domain-level metrics such as nurse communication, doctor communication, cleanliness, and care transitions. For project demonstration purposes, the dataset only includes Q2 results of each year from 2022-2024 and has been filtered exclusively to Piedmont Healthcare hospitals to support executive decision-making.

Data on hospital type and number of beds are taken from each Piedmont hospital website and manually entered into "bed_info" Excel file.

## 4. Questions (KPIs):
  * How do these KPIs perform year-over-year?
     * Overall satisfaction – star rating.
     * Likelihood to recommend hospital - star rating.
     * Summary star rating across all domains.
  *	In terms of overall satisfaction, where does the hospital rank compared to other Piedmont hospitals?
  *	How does each hospital perform across all domains against the national average and state average?
  *	What are the key areas of improvement for each hospital to drive patient satisfaction?

## 5. Process:
The project followed a rigorous methodology encompassing data quality assurance, relational modeling, advanced statistical analysis, and interactive visualization.

### 5.1) Data Acquisition & Quality Assurance (QA)
* **Raw data audit:** Verified the original HCAHPS flat-file dataset from CMS website for data integrity, identifying missing values and anomalies (e.g., inconsistent formatting, outliers).
* **Data cleaning:** Performed comprehensive data type conversion and consistency checks to ensure a high-fidelity input dataset suitable for database ingestion.

### 5.2) Database Modeling & ETL Pipeline
* **Technology stack:** Utilized **PostgreSQL** as the core database engine for persistent storage and **pgAdmin 4** as primary GUI tool for execution and administration.
* **Relational architecture:** Converted the flat-file structure into an optimized Snowflake Schema. This normalization strategy established clear dimension tables (e.g., Facility, Survey, Measurement, Date) and a central fact table, drastically reducing data redundancy.
* **Implementation:** Developed and executed all Data Definition Language (DDL) and Data Manipulation Language (DML) scripts using the pgAdmin 4 Query Tool to construct the schema, load the data, and enforce referential integrity. This optimization improved subsequent query performance for the BI layer.

### 5.3) Advanced Statistical Analysis (R)
* **Driver Analysis:** Conducted a statistically robust Relative Importance Analysis to precisely quantify the impact of each surveyed domain (e.g., Nurse Communication, Cleanliness) on the overall "Satisfaction Star Rating" metric.
* **Methodology:** Employed **Shapley Regression** (performed in **R**) to determine the marginal contribution of each predictor variable. This method ensures fair and accurate attribution of impact levels, moving beyond simple correlation.
* **Insight generation:** the calculated importance weight of each domain are categorized into 3 impact levels ("High", "Moderate" and "Low") and integrated into the Power BI model to drive the final business recommendations.

### 5.4) Business Intelligence & Visualization
* **Data sourcing strategy:** Rather than a live connection, the optimized Snowflake Schema was queried and exported into clean, delimited flat files (CSVs) using **pgAdmin 4**.
* **Model ingestion:** These structured CSV files were then loaded into the Power BI Data Model. This approach ensured a consistent, performant snapshot of the modeled data, separating the data transformation load from the visualization environment.
* **Dashboard development:** Designed a comprehensive, interactive dashboard with visuals tailored to answer key business questions, including trend analysis, comparative performance across Piedmont hospitals and national and state averages.
* **Key feature:** Incorporated the impact levels from the Shapley Regression analysis to visually highlight the highest-impact drivers of patient satisfaction, enabling stakeholders to prioritize targeted operational improvements.

## 6. Project Insights:
1. **Primary outcome:** the dashboard is designed as a dynamic, hospital-level diagnostic tool, enabling Piedmont health executives to pinpoint specific operational metrics driving their facility's patient experience scores. The key insight is its ability to highlight a hospital's **performance gaps and critical success factors** relative to its peers.
2. **What matters here:** the Relative importance analysis (Shapley regression), integrated into the dashboard, provides a personalized driver analysis for any selected hospital. For example, while "Nurse Communication" is the top national driver of satisfaction, key focus for Piedmont Macon North Hospital should be placed on improving Care transition and Communication on medicine.
3. **How do we compare:** each Piedmont hospital is ranked based on how many satisfied respondents it has for each Q2. About half of the hospitals have a satisfaction level of 70% or more.
