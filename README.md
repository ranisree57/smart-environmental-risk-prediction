# 🌍 Smart Environmental Risk Prediction and Analytics

An ML-powered environmental analytics web application for exploring historical Air Quality Index (AQI) data, analyzing pollution trends, comparing machine learning models, and experimenting with AQI forecasting.

**Built with Python, FastAPI, Machine Learning, and a responsive web interface.**

> Project status: Developed as a B.Tech final-year project. The application analyzes historical data; it does not provide verified real-time AQI readings.

---

## 📌 Project Overview

Air pollution is an important environmental concern. Historical air-quality data can help people explore pollution patterns, compare locations, and understand changes in AQI over time.

**Smart Environmental Risk Prediction and Analytics** transforms historical AQI data into an interactive web application with data visualizations, regional analysis, model comparisons, and forecasting demonstrations.

## 🎯 Objectives

- Analyze historical AQI data and identify trends.
- Visualize air-quality patterns across regions and time periods.
- Prepare historical data for machine learning.
- Compare forecasting models using appropriate evaluation metrics.
- Provide an interactive interface for exploring results.
- Demonstrate how a machine learning model can be integrated with a web application.

## ✨ Key Features

- **Environmental dashboard:** View AQI statistics and historical trends.
- **Regional exploration:** Search and compare available locations.
- **Data visualization:** Explore AQI distributions and changes over time.
- **Forecasting lab:** Experiment with different forecast horizons.
- **Model comparison:** Compare machine learning approaches with a simple baseline.
- **Model evaluation:** Review metrics such as Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE).
- **Data quality analysis:** Examine missing observations and potential data inconsistencies.
- **CSV export:** Download supported data tables for further analysis.
- **API documentation:** Explore backend endpoints through FastAPI's interactive documentation.

*Available features depend on the functionality implemented in the deployed version.*

## 🛠️ Technology Stack

| Component | Technology |
|---|---|
| Programming language | Python |
| Data processing | Pandas, NumPy |
| Machine learning | Scikit-learn |
| Backend API | FastAPI |
| API server | Uvicorn |
| Visualization | JavaScript-based charts and frontend components |
| Data storage | CSV and processed files |
| Version control | Git and GitHub |
| Deployment | Render (planned or in progress) |

## 🧠 Machine Learning Approach

The project follows a structured machine learning workflow:

1. Data collection and inspection.
2. Data cleaning and validation.
3. Exploratory Data Analysis (EDA).
4. Feature engineering using historical observations.
5. Chronological training, validation, and testing.
6. Model training and comparison.
7. Evaluation against a persistence baseline.
8. Integration with the web application.

Candidate models include Ridge Regression, Random Forest, and Gradient Boosting, subject to the models implemented in the current application.

**Evaluation metrics**

- **MAE:** Average absolute difference between actual and predicted AQI values.
- **RMSE:** Penalizes larger prediction errors more strongly.
- **Baseline comparison:** Checks whether a machine learning model improves on a simple persistence forecast.

Model performance should be reported using actual evaluation results from the project's trained models. Results can vary with data, features, and evaluation settings.

## 📊 Dataset

The project uses historical AQI records containing fields such as:

- Date
- State
- Area
- Number of monitoring stations
- Prominent pollutants
- AQI value
- Air-quality status

The analyzed dataset contains 235,785 records covering **April 1, 2022, through April 30, 2025**, across 32 states and 291 distinct area names.

The initial analysis focuses on Ahmedabad for a more specific regional use case.

**Data limitation:** The dataset ends on April 30, 2025. Forecasts based on it are historical demonstrations and should not be interpreted as current AQI readings or verified live forecasts.

Please consult the original data provider's licensing
