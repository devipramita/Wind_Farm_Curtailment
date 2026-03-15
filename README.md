# 🌀🌍⚡ Wind Farm Curtailment Prediction
Data-driven prediction of wind power curtailment using SCADA data, weather conditions, electricity demand, and market price signals.

This project investigates the drivers of wind farm curtailment in the UK and builds machine learning models to identify curtailment events.

Finished as part of Final Project of UCL BENV0091 Energy Data Analytics (25/26).

## Problem Motivation
Wind power curtailment occurs when available wind generation cannot be fully utilized due to grid constraints, market conditions, or system balancing requirements. Curtailment leads to:<br>
- lost renewable energy
- reduced revenue for wind farm operators
- inefficient grid operation

Understanding and predicting curtailment events can help improve grid planning and renewable integration.<br>

## Project Objective
The objective of this project is to:<br>
1. Integrate multiple energy datasets including SCADA, weather, demand, and market signals.
2. Identify key drivers of wind curtailment events.
3. Develop machine learning models to classify curtailment conditions.
4. Analyze electricity demand and market price patterns using clustering techniques.

## How to Run
1. Clone the repository<br>
`git clone https://github.com/devipramita/Wind_Farm_Curtailment.git`

2. Install dependencies<br>
`pip install -r requirements.txt`

3. Run the notebook<br>
`jupyter notebook curtailment_prediction_pipeline.ipynb`

## Data Sources
The analysis integrates several datasets related to wind generation and electricity markets in the UK.

No | Dataset | Description | Source Link 
--- | --- | --- | --- 
1 | SCADA Hill of Towie in Scotland | Wind turbine operational data from Hill of Towie wind farm | https://zenodo.org/records/14870023 (2023 & 2024)
2 | ERA5 meteorological data in Scotland | Meteorological data including wind speed and atmospheric conditions | https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels?tab=overview 
3 | NESO BOA volume data in Scotland | Balancing mechanism actions related to wind curtailment | https://www.neso.energy/data-portal/wind-bmu-boa-volumes 
4 | IMRP Market Price data | Intermittent Market Reference Price for electricity | https://dp.lowcarboncontracts.uk/dataset/imrp-actuals 
5 | Electricity Demand Data | Historical electricity demand | https://www.neso.energy/data-portal/historic-demand-data 
6 | Regional Electricity Consumption | Regional electricity consumption statistics | https://www.gov.uk/government/statistics/regional-and-local-authority-electricity-consumption-statistics 

Note: Main dataset (merged result from original data) for Wind Farm Curtailment Classification: <br>
HTW_FINAL_DATASET.csv

## System Architecture
```
SCADA Data        ERA5 Weather        Market Price        Electricity Demand
     │                 │                   │                       │
     └────────────── Data Integration & Cleaning ──────────────────┘
                                 │
                        Feature Engineering
                                 │
                     Curtailment Classification
                                 │
                   Demand & Market Price Clustering
                                 │
                         Insight Generation
```

## Feature Engineering
Several features were constructed by integrating operational, weather, and market datasets.

Key features include:
- Wind speed measurements derived from ERA5 weather data
- Turbine power output from SCADA operational data
- Electricity demand signals
- Intermittent Market Reference Price (IMRP)
- Curtailment indicators from NESO balancing mechanism actions

All datasets were temporally aligned and merged into a unified dataset used for modeling.

## Machine Learning Models
Two types of machine learning approaches were applied in this project.

#### 1. Curtailment Classification
Supervised learning models were trained to identify wind curtailment events using operational, weather, and market variables.

Models explored:
- Logistic Regression
- Random Forest
- Multi-Layer Perceptron (MLP)

These models use features derived from SCADA turbine data, ERA5 weather conditions, electricity demand signals, and market price indicators.

#### 2. Demand Clustering
Unsupervised learning was applied to identify patterns in electricity demand.

Algorithm used:
- K-Means Clustering

#### 3. Market Price Clustering
Clustering was also applied to electricity market price data to identify distinct price regimes associated with curtailment conditions.

## 📊 Model Performance
Curtailment Prediction
| Model | ROC-AUC score | Notes |
|------|--------|------|
| Logistic Regression | 95% | baseline model |
| Random Forest | 97% | best performance |
| Multi Layer Perceptron | 94% | sensitive to hyperparameters |


## Repository Structure
```
Wind_Farm_Curtailment/
│
├── SCADA/                        # Wind turbine operational data
├── ERA5/                         # Meteorological data
├── NESO BOA/                     # Curtailment & market demand data
│
├── HTW_FINAL_DATASET.csv         # Merged dataset used for modeling
|
├── Data_Prep_and_Curtailment_Classification_and_Demand_Clustering.ipynb
├── Market_Price_Clustering.ipynb
│
└── README.md
```

## Key Insights
Key findings include:
- Curtailment events are correlated with low electricity demand periods.
- Market price signals influence curtailment decisions.
- Wind conditions alone do not fully explain curtailment events.

Clustering analysis revealed distinct demand and market regimes associated with curtailment risk.

## Tech Stack
- Python
- Pandas
- Scikit-learn
- Jupyter Notebook
- Energy market datasets

## Future Work
Potential extensions include:
- time-series forecasting of curtailment events
- deep learning models for curtailment prediction
- reinforcement learning for grid dispatch optimization

### References
1. Clerc, A. and Lingkan, E. (2025) “Hill of Towie wind farm open dataset”. Zenodo. doi:10.5281/zenodo.14870023.
2. Copernicus Climate Change Service (C3S) Climate Data Store (CDS). doi: 10.24381/cds.adbb2d47.
3. National Energy System Operator (2025). Wind BOA Volumes. [Data set]. Available at: https://www.neso.energy/data-portal/wind-bmu-boa-volumes 
4. Low Carbon Contracts Company (2025). Intermittent Market Reference Price (IMRP) Actuals. [Data set]. Available at: https://dp.lowcarboncontracts.uk/dataset/imrp-actuals
5. National Energy System Operator (2025). Historic Demand Data. [Data set]. Available at: https://www.neso.energy/data-portal/historic-demand-data
6. Department for Energy Security and Net Zero (2024). Regional and local authority electricity consumption statistics: 2005 to 2023. [Data set]. Available at: https://www.gov.uk/government/statistics/regional-and-local-authority-electricity-consumption-statistics 
