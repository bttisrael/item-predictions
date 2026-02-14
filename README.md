# Item Demand Predictions: An Predict sales by item, store and day Pipeline

<img width="100%" alt="Dashboard Preview" src="https://github.com/user-attachments/assets/cfa81f7f-0883-415b-83bb-55576696407a" />

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=flat&logo=google-cloud&logoColor=white)](https://cloud.google.com/)
[![BigQuery](https://img.shields.io/badge/BigQuery-SQL-4285F4?style=flat&logo=google-cloud&logoColor=white)](https://cloud.google.com/bigquery)
[![Looker Studio](https://img.shields.io/badge/Looker_Studio-BI-4285F4?style=flat&logo=looker&logoColor=white)](https://lookerstudio.google.com/)
[![Google Colab](https://img.shields.io/badge/Colab-Notebook-F9AB00?style=flat&logo=google-colab&logoColor=white)](https://colab.research.google.com/)

## Introduction

Retail-Demand-Forecasting is a Python-based, end-to-end pipeline that supports modeling and predicting daily sales volume for retail item-store combinations. The core capability of this project is to integrate raw data ingestion, feature engineering, machine learning forecasting, and business intelligence deployment. 

The pipeline builds predictive models using Scikit-Learn (Random Forest) and embeds the outputs into a cloud data warehouse (Google BigQuery) for dashboard consumption. For local reproducibility and offline environments, the repository implements a hybrid architecture utilizing DuckDB for local SQL-based processing without cloud dependency.

## Features

* Implement automated ETL processes connecting raw CSV sources to Google BigQuery.
* Support advanced feature engineering including lag features, moving averages, and cyclical time transformations (Sine/Cosine).
* Support hybrid execution mode using DuckDB for local SQL queries.
* Implement time-series split validation for robust backtesting.
* Support post-processing bias correction to handle structural breaks (e.g., Flagship store anomalies).

## Installation

Clone and install from this repository. You can download the project using git:

```bash
git clone [https://github.com/bttisrael/item-predictions.git](https://github.com/bttisrael/item-predictions.git)
cd item-predictions
```

Install the required packages using pip:

```bash
pip install -r requirements.txt
```

## Usage & Sample Code

The main execution is performed via the provided Jupyter Notebook. Below is a simplified snippet demonstrating the **hybrid data ingestion** (Cloud vs. Local) mechanism implemented in the pipeline:

```python
import pandas as pd
import duckdb

# Configuration flag
USE_BIGQUERY = False

if USE_BIGQUERY:
    # Cloud Mode: Connect to GCP BigQuery
    query = "SELECT * FROM `otimizador-cargas.sales.transactions`"
    df = pd.read_gbq(query, project_id='otimizador-cargas')
else:
    # Offline Mode: Use DuckDB for local SQL execution without Cloud Auth
    query = """
        SELECT store_id, SUM(sales) as total_sales
        FROM read_csv_auto('data_sample.csv')
        GROUP BY store_id
        ORDER BY total_sales DESC
        LIMIT 5
    """
    df = duckdb.query(query).df()

print(df.head())
```

## Experiments and Diagnostics

To reproduce the experiments and the business diagnostics, run the `item_predictions.ipynb` notebook. The evaluation yielded the following insights:

* **General Performance:** The model achieved a Mean Absolute Percentage Error (MAPE) of **~22%** for standard retail stores using a log-transformed Random Forest Regressor.
* **Structural Break Detection:** The error analysis identified a significant anomaly in Store 1 (Flagship Store) starting in Jan 2024. The empirical results suggest segregating outlier stores into a dedicated predictive cluster to maintain global model accuracy.

## Reference

[1] Breiman, L. (2001). Random Forests. *Machine Learning*, 45(1), 5-32.  
[2] Raasveldt, M., & Mühleisen, H. (2019). DuckDB: an Embeddable Analytical Database. *Proceedings of the 2019 International Conference on Management of Data*.
