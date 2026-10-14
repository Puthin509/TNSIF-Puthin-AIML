# Instructions

## Requirements

- Python 3.9 or newer
- The packages listed in `requirements.txt`

## Install dependencies

Open a terminal in this `unsupervised` folder and run:

```bash
python -m pip install -r requirements.txt
```

## Run the web application

Start the Flask development server from this folder:

```bash
python app.py server
```

Open [http://127.0.0.1:5000](http://127.0.0.1:5000) in a browser. Enter listening hours per week, songs per day, skip rate, and playlist count, then submit the form to see the predicted listener segment.

## Use the JSON API

Send a `POST` request to `/predict` with a JSON body containing all four numeric fields:

```json
{
  "listening_hours_per_week": 12,
  "songs_per_day": 18,
  "skip_rate": 0.25,
  "playlist_count": 7
}
```

The response contains the predicted segment:

```json
{
  "segment": "Music Explorer"
}
```

## Run the command-line predictor

Run `python app.py` from this folder to enter the four values interactively in the terminal.

## Retrain the model

Run `python train_model.py` from this folder to train the K-Means model using `music_listeners.csv`. This regenerates `model.pkl`, `scaler.pkl`, and `cluster_mapping.pkl`.
