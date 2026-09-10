# AERIS Passenger Intelligence

AERIS is a premium Streamlit application for predicting airline passenger satisfaction from passenger profile, journey details, operational delays, and onboard service ratings.

The application uses a saved XGBoost classification model and presents predictions through a responsive airline intelligence dashboard.

## Features

- Passenger satisfaction prediction
- Passenger profile inputs
- Journey and flight delay inputs
- 14 onboard service ratings
- Satisfaction forecast with model probability when available
- Dynamic passenger experience signals
- Journey summary with distance, class, delays, and experience score
- Responsive premium aviation-themed interface
- Cached model loading with `st.cache_resource`
- User-friendly model and prediction error handling

## Project Structure

```text
Airline-Passenger-Satisfaction/
|-- app.py
|-- ml_model.joblib
|-- ml_model (1).joblib
|-- requirements.txt
|-- README.md
`-- .venv/
```

`ml_model.joblib` is the model used by the application. The duplicate model file is kept in the project but is not required at runtime.

## Requirements

- Python 3.10 or newer
- Windows, macOS, or Linux
- An environment capable of installing the packages in `requirements.txt`

The model was serialized with an older XGBoost format, so the project pins:

```text
xgboost==2.0.3
```

Do not replace this version unless the model is re-exported and tested again.

## Installation

Create and activate a virtual environment.

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

If PowerShell blocks activation for the current terminal session:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1
```

## Run the Application

```powershell
streamlit run app.py
```

Open the local URL shown by Streamlit, usually:

```text
http://localhost:8501
```

If port `8501` is already in use, run the app on another port:

```powershell
streamlit run app.py --server.port 8502
```

## Model Inputs

The model receives 22 features in the following order:

- Gender
- Customer Type
- Age
- Type of Travel
- Class
- Flight Distance
- Inflight wifi service
- Departure/Arrival time convenient
- Ease of Online booking
- Gate location
- Food and drink
- Online boarding
- Seat comfort
- Inflight entertainment
- On-board service
- Leg room service
- Baggage handling
- Checkin service
- Inflight service
- Cleanliness
- Departure Delay in Minutes
- Arrival Delay in Minutes

Categorical values are encoded in `encode_inputs()` using the mappings expected by the trained model. The feature names and feature order should not be changed unless the model is retrained.

## Prediction Output

The application displays:

- Satisfied or neutral/dissatisfied forecast
- Prediction probability when the loaded model supports `predict_proba()`
- Strongest passenger experience signals from the submitted ratings
- Journey summary and overall experience score

The application does not display a fabricated accuracy score or confidence value. If probability support is unavailable, it displays that model probability is unavailable.

## Validation

Useful checks after installation:

```powershell
python -m pip check
python -m py_compile app.py
```

To verify the model input shape:

```powershell
python -c "import joblib; import app; model=joblib.load('ml_model.joblib'); print(model.n_features_in_)"
```

The bundled model is expected to report `22` input features.

## Important Notes

- Keep `ml_model.joblib` in the same directory as `app.py`.
- Keep `xgboost==2.0.3` installed for the current serialized model.
- The app does not download the Kaggle dataset at runtime.
- Do not claim model accuracy or feature importance unless those metrics are calculated from a documented evaluation workflow.

## License

Add the appropriate license before publishing this project publicly.
