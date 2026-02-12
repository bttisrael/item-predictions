# Retail-Demand-Forecasting: An End-to-End Predict-then-Optimize Pipeline
<img width="1615" height="684" alt="image" src="https://github.com/user-attachments/assets/cfa81f7f-0883-415b-83bb-55576696407a" />

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

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
git clone [https://github.com/YOUR-USERNAME/retail-demand-forecast.git](https://github.com/YOUR-USERNAME/retail-demand-forecast.git)
cd retail-demand-forecast
