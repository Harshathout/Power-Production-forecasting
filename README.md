# Power-Production-forecasting
# Forecast + Alerting Pipeline  
*A 24-hour Data Scientist Intern Task for Logic Leap AI Pvt. Ltd.*  

##  Overview  
This project implements a **forecasting and alerting pipeline** for daily multi-site operations data.  
The pipeline predicts the next **14 days of `units_produced` and `power_kwh`**, compares **baseline vs improved models** (evaluated using MAE/MAPE), and detects **downtime anomalies** with interpretable methods.  

Deliverables include:  
- Cleaned + feature-engineered datasets  
- Forecast results with evaluation metrics  
- Downtime anomaly detection (`alerts.csv`)  
- Minimal **FastAPI/CLI** app to return forecasts & anomalies per site/date range  
- **1-page executive brief (PDF)** with insights and automation triggers  

---

## Repository Structure  
/app/ # Minimal FastAPI or CLI app
main.py
/outputs/ # Final outputs
alerts.csv
forecast_units.csv
forecast_power.csv
requirements.txt # Python dependencies
README.md # Project documentation
executive_brief.pdf # 1-page executive summary


---

## Dataset  
The task uses daily site-level operations data:  

- `operations_daily.csv` — daily site operations (production & power)  
- `site_meta.csv` — site metadata  

 Download dataset: [Google Drive Link](https://drive.google.com/drive/folders/1T1L741_L8A1wfDH-fgQkiOFMZlVqZPoc?usp=drive_link)  

 The dataset is **not included in this repo**.  
Please place both CSVs inside a local `data/` folder before running.  

---

##  Setup & Usage  

### 1. Clone the repository  
```bash
git clone https://github.com/<Harshathout>/Power-Production-forecasting.git
cd forecast-alerting-pipeline

### 2. Create environment & install dependencies
python3.10 -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
pip install -r requirements.txt

### 3. Run pipeline (example commands)
# Step 1: Load & preprocess data
python src/loader.py --data data/ --out outputs/

# Step 2: Feature engineering
python src/features.py --in data/operations_daily.csv --out outputs/features.csv

# Step 3: Forecasting (baseline + improved models)
python src/models.py --in outputs/features.csv --out outputs/forecast_units.csv --metric MAE
python src/models.py --in outputs/features.csv --out outputs/forecast_power.csv --metric MAPE

# Step 4: Detect anomalies
python src/anomaly.py --in outputs/features.csv --out outputs/alerts.csv

4. Run FastAPI app
uvicorn app.main:app --reload


### Outputs
outputs/alerts.csv → downtime anomaly alerts (site, date, metric, reason, severity)
outputs/forecast_units.csv → 14-day forecast for production units
outputs/forecast_power.csv → 14-day forecast for power usage (kWh)

### Executive Summary
The executive_brief.pdf (included in this repo) highlights:
Key trends in production & power usage
Forecast accuracy (baseline vs improved models)
Anomaly alerts (downtime events)
Suggested automation triggers for monitoring

### Tech Stack
Python 3.10+
pandas, numpy
scikit-learn, statsmodels, prophet (optional)
xgboost / lightgbm (optional)
fastapi, typer

### Notes
Reproducible: fixed random seeds are set for sklearn, numpy, and random.
Allowed libraries only (no external APIs or paid tools).
Dataset is external (link provided above).

###Author
Harsha Thout
Data Scientist Intern Task — Logic Leap AI Pvt. Ltd.

