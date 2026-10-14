# Instructions

## Requirements

- Python 3.9 or newer.
- Run commands from this folder, where `app.py`, `main.py`, `model.pkl`, and
  `scaler.pkl` are located.

## Install dependencies

Create and activate a virtual environment, then install the packages:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

On macOS or Linux, activate the environment with:

```bash
source .venv/bin/activate
```

## Start the Streamlit app

```bash
python -m streamlit run app.py
```

Open the local URL printed in the terminal (normally `http://localhost:8501`).
Enter annual income, credit score, loan amount, and years of employment, then
select **Analyze Loan Application**.

## Start the FastAPI service

In a separate terminal, with the virtual environment activated:

```bash
python -m uvicorn main:app --reload
```

The API is available at `http://localhost:8000`; interactive API
documentation is at `http://localhost:8000/docs`.

Send a prediction request to `POST /predict` with JSON such as:

```json
{
  "income": 50000,
  "credit_score": 700,
  "loan_amount": 15000,
  "employment_years": 5
}
```

The response contains the predicted loan status, approval probability, and a
numeric status code.

## Prepare data and retrain (optional)

From this folder, validate and prepare the source dataset:

```bash
python dataset.py
```

Then train and evaluate the model and regenerate `model.pkl` and `scaler.pkl`:

```bash
python train_model.py
```

Training overwrites the existing model artifacts. Stop the running app or API
before replacing them, then restart it to load the newly trained artifacts.
