# AERO — Smart Environmental Risk Prediction & Analytics

A full-stack B.Tech project built with **FastAPI + Pandas + Scikit-learn + responsive HTML/CSS/JavaScript**. It includes a dark analytics dashboard, interactive AQI history charts, area explorer, data quality checks, model comparison, a time-aware forecasting lab, and CSV export.

> **Data honesty:** the included source dataset ends on **30 April 2025**. The application labels values as historical and forecast output as a retrospective demonstration. It does not claim to show today's AQI or live sensor readings.

## Quick start (Windows)

1. Download and extract this project ZIP.
2. Open the extracted `smart_environmental_risk_website` folder in VS Code.
3. Ensure standard Python 3.13 is installed (not the free-threaded `3.13t` build). Python 3.12 or 3.13 standard is suitable.
4. Double-click `run_windows.bat`, or open the terminal in this folder and run:

   ```powershell
   .\run_windows.bat
   ```

   The script creates `.venv`, installs dependencies, and starts the server. It does **not** require you to activate the environment manually.
5. Open `http://127.0.0.1:8000` in Chrome or Edge.
6. API documentation is at `http://127.0.0.1:8000/api/docs`.

Keep the terminal window open while presenting. Stop the server with `Ctrl+C`.

## Manual setup (VS Code terminal)

Run from the repository root:

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip setuptools wheel
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m uvicorn app.main:app --host 127.0.0.1 --port 8000
```

This avoids PowerShell activation-policy issues and uses the project interpreter explicitly.

## Product features

- **Overview:** latest available observation, historical mean/peak, AQI timeline, monthly summaries, category distribution, regional watchlist.
- **Forecast lab:** train/evaluate Ridge Regression, Random Forest and Gradient Boosting; select via validation MAE; compare to a persistence baseline; create a 1/3/7/14-day recursive historical demonstration forecast.
- **Regional explorer:** searchable area rankings and category summaries.
- **Model bench:** validation metrics, chronological test metrics, baseline comparison, and feature influence.
- **Data quality:** input coverage, missing date checks, source label consistency, and field missingness.
- **Project brief:** architecture, methods, API links, limitations.
- **CSV export:** download the selected area's processed history.
- **API docs:** interactive Swagger/OpenAPI documentation.

## Architecture

```text
Browser (HTML / CSS / JavaScript / Canvas)
                 │ same-origin fetch
                 ▼
          FastAPI REST API
      ┌──────────┼────────────┐
      ▼          ▼            ▼
 Data service  ML service  CSV export
      │          │
      ▼          ▼
 ZIP/CSV data  Scikit-learn models
                 │
                 ▼
    validation/test metrics + joblib artifact
```

The frontend has no Node.js or npm build step. FastAPI serves both the website and API from the same local server.

## Source data

`data/raw/archive (1).zip` contains `aqi.csv` with columns such as `date`, `state`, `area`, `aqi_value`, `air_quality_status` and prominent pollutants. The application parses the source date format (`DD-MM-YYYY`), validates the AQI range, removes duplicate date/state/area keys, and leaves missing calendar days missing rather than inventing observations.

Before pushing this repository publicly, record the original download URL and confirm the source dataset's license/attribution requirements in `data/SOURCE.md`.

## Modeling notes

- Target: daily area-level AQI value.
- Features: lagged AQI at 1, 2, 3, 7, 14 and 30 days; rolling historical mean/std; calendar seasonality encodings.
- Candidate models: Ridge Regression, Random Forest Regressor, Histogram Gradient Boosting Regressor.
- Selection: lowest validation MAE on an ordered time split.
- Test: later, chronologically separated holdout; includes comparison to persistence (`AQI(t) ≈ AQI(t-1)`).
- The offline test score is a rolling one-step-ahead evaluation using preceding historical observations. Production multi-day forecasting is recursive, so uncertainty and error can grow across the horizon.
- Approximate forecast range is derived from validation residuals and expands with horizon. It is a heuristic interval, not a calibrated guarantee.

Important limitations: the supplied data does not include weather, meteorology, industrial activity, or live station readings. Performance may change with time and region. A forecast from data ending in April 2025 must not be presented as a real-world October 2026 forecast.

## API endpoints

| Endpoint | Purpose |
|---|---|
| `GET /api/health` | Health and data range |
| `GET /api/overview` | Dataset coverage startup payload |
| `GET /api/areas` | Area selector options |
| `GET /api/summary?area=Ahmedabad&state=Gujarat` | Selected-area KPI and monthly data |
| `GET /api/history?area=Ahmedabad&state=Gujarat&days=365` | Historical observations |
| `GET /api/regions?sort=highest&limit=25` | Latest area-level ranking |
| `GET /api/alerts` | Historical high-AQI flags |
| `GET /api/data-quality` | Dataset and selected-area checks |
| `GET /api/models?area=Ahmedabad&state=Gujarat` | Train/return model comparison |
| `GET /api/forecast?horizon=7` | Generate demonstration forecast |
| `GET /api/export?area=Ahmedabad&state=Gujarat` | Download CSV |
| `GET /api/docs` | Interactive Swagger docs |

Some endpoints default to Ahmedabad/Gujarat. For names duplicated across states, pass both `area` and `state`.

## GitHub hygiene

- Do not commit `.venv`, credentials or private material.
- Confirm data license/attribution before publishing the supplied archive.
- Model artifacts under `models/` and generated reports under `reports/` are produced by running the app and are not required for the first launch.
- Add your own screenshots in `screenshots/` after you have run the project successfully.

## Troubleshooting

**Port 8000 is already in use:** stop the other server or change the port in `run_windows.bat` and use the matching browser URL.

**Package installation fails:** inspect the first error above `subprocess-exited-with-error`; do not type requirement specifiers like `joblib>=1.3` into PowerShell. They belong in `requirements.txt`.

**Dataset not found:** ensure `data/raw/archive (1).zip` is present and contains `aqi.csv`.

**Forecast returns an error:** check `http://127.0.0.1:8000/api/health`, then open `/api/docs`; the server terminal prints the underlying traceback.
