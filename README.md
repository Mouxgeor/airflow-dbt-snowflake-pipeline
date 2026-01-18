# 🚀 End-to-End ELT Pipeline: Airflow, dbt & Snowflake

## 📋 Project Overview
This project demonstrates a production-grade data pipeline that orchestrates the transformation of raw data into analytics-ready models. 

By integrating **Apache Airflow** (orchestration) with **dbt** (transformation) and **Snowflake** (compute), this project solves the problem of manual, error-prone SQL scripts, replacing them with a version-controlled, automated software engineering workflow.

## 🏗️ Architecture & Tech Stack

|Component           | Technology                     | Role in Project                                                                         |
| ------------------ | -------------------------------| ----------------------------------------------------------------------------------------|
| **Orchestrator**   | **Apache Airflow** (Astro CLI) | Schedules jobs, manages dependencies, and handles retries alerts.                       |
| **Transformation** | **dbt Core** (Data Build Tool) | Compiles modular SQL, runs data quality tests, and handles lineage.                     |
| **Warehouse**      | **Snowflake**                  | Scalable cloud compute for executing heavy SQL transformations.                         |
| **Integration**    | **Astronomer Cosmos**          | Dynamically renders dbt models as individual Airflow tasks for granular visibility.     |
| **Environment**    | **Docker**                     | Ensures consistent runtime across development and production.                           |

## 🔄 Data Flow
1.  **Extract/Load:** Raw data is ingested into Snowflake (simulated via TPC-H dataset).
2.  **Transform (Staging):** dbt cleans and normalizes raw tables (`stg_tpch_orders`).
3.  **Transform (Marts):** dbt joins and aggregates data into business-logic tables (`fct_orders`).
4.  **Quality Check:** Automated tests run on every pipeline execution to ensure data integrity.

## 📂 Project Structure
* `dags/dbt_dag.py`: The Python entry point that uses Cosmos to generate the Airflow DAG.
* `dags/data_pipeline/`: The full dbt project containing SQL models (`.sql`) and configuration (`dbt_project.yml`).
* `Dockerfile`: Custom image definition ensuring `dbt-snowflake` and `cosmos` are installed in an isolated virtual environment.
<img width="1305" height="484" alt="pipeline_graph" src="https://github.com/user-attachments/assets/57fbceec-0c71-416c-812e-23530dbf9ec0" />
<img width="394" height="333" alt="success_grid" src="https://github.com/user-attachments/assets/97b0f582-c8b7-48a0-9962-791b78feca5b" />
<img width="1239" height="409" alt="proof_of_data" src="https://github.com/user-attachments/assets/56e035b8-4da3-4b44-a687-a3aadfcdedda" />

## 🛠️ How to Run Locally
1.  **Clone the Repository:**
    ```bash
    git clone <https://github.com/Mouxgeor/airflow-dbt-snowflake-pipeline.git>
    ```
2.  **Start the Airflow Environment:**
    ```bash
    astro dev start
    ```
3.  **Access the UI:**
    * **Airflow:** `http://localhost:8080` (Admin/Admin)
    * **Snowflake:** Verify tables in `DBT_DB.DBT_SCHEMA`

---
*Created by George Mouxios - Data Engineer*
