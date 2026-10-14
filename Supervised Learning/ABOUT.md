# About

## Loan Approval Prediction

This project is an educational supervised-learning application that predicts a
loan applicant's status from four numeric inputs: annual income, credit score,
loan amount, and years of employment.

The prediction pipeline uses a `StandardScaler` to scale the input features and
a `RandomForestClassifier` to estimate the loan status. The Streamlit interface
displays an approval or rejection prediction and the model's approval
probability. A separate FastAPI application exposes the same model through a
JSON API.

## Project files

- `app.py` - Streamlit loan application interface.
- `main.py` - FastAPI prediction API.
- `dataset.py` - Validates the source CSV columns and writes `loans.csv`.
- `train_model.py` - Trains and evaluates the classifier, then saves the model
  and scaler.
- `loans - loans.csv` - Source loan dataset.
- `loans.csv` - Dataset used by the training script.
- `model.pkl` and `scaler.pkl` - Serialized model and preprocessing artifacts
  used by the applications.
- `requirements.txt` - Python package dependencies.

This is a demonstration project, not a substitute for a lender's review or
professional financial advice. Predictions depend on the training data and
should not be treated as guaranteed or authoritative lending decisions.
