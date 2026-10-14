# Music Listener Segmentation

This project is an end-to-end unsupervised machine-learning application that groups music listeners into behavioral segments. It trains a K-Means clustering model from sample listening data and provides a Flask web app, a JSON API, and an interactive command-line predictor.

Because the model is unsupervised, it discovers groups from the data rather than learning predefined user labels. The application assigns descriptive names to the clusters by ordering their centers by weekly listening hours.

## How it works

1. `train_model.py` reads `music_listeners.csv` and selects four numeric listener metrics.
2. A `StandardScaler` standardizes the metrics so that features with different scales can contribute to clustering.
3. K-Means is fitted with three clusters (`k=3`).
4. The trained model, scaler, and cluster-to-name mapping are saved as `model.pkl`, `scaler.pkl`, and `cluster_mapping.pkl`.
5. `app.py` loads those artifacts, scales each new listener's metrics with the same scaler, predicts a cluster, and returns its descriptive segment.

The segment names are **Casual Listener**, **Music Explorer**, and **Heavy Listener**. They are interpretations of the discovered clusters, not verified categories or guarantees about an individual listener.

## Input features

The model uses these columns from the dataset:

| Feature | Description |
| --- | --- |
| `listening_hours_per_week` | Hours spent listening in a typical week |
| `songs_per_day` | Number of songs listened to per day |
| `skip_rate` | Fraction of songs skipped, from 0 to 1 |
| `playlist_count` | Number of playlists maintained |

## Project files

| File | Purpose |
| --- | --- |
| `app.py` | Flask web application, `/predict` endpoint, and interactive CLI |
| `train_model.py` | Preprocesses data, trains K-Means, and saves model artifacts |
| `dataset.py` | Dataset-related helper code |
| `music_listeners.csv` | Training data used by the model |
| `music_listeners.xlsx` | Spreadsheet version of the sample dataset |
| `model.pkl` | Serialized trained K-Means model |
| `scaler.pkl` | Serialized fitted feature scaler |
| `cluster_mapping.pkl` | Mapping from cluster IDs to descriptive names |
| `templates/index.html` | Web interface for entering listener metrics |
| `requirements.txt` | Python package dependencies |
| `INSTRUCTIONS.md` | Quick setup and usage instructions |
| `ABOUT.md` | Short project summary |

## Requirements

- Python 3.9 or newer
- Packages listed in `requirements.txt`

Install dependencies from this directory:

```bash
python -m pip install -r requirements.txt
```

## Run the web application

Run the Flask development server from this directory:

```bash
python app.py server
```

Open [http://127.0.0.1:5000](http://127.0.0.1:5000), enter the four metrics, and submit the form to view the predicted segment.

## Use the JSON API

Send a `POST` request to `/predict` with a JSON body:

```json
{
  "listening_hours_per_week": 12,
  "songs_per_day": 18,
  "skip_rate": 0.25,
  "playlist_count": 7
}
```

The response is a JSON object containing the predicted segment:

```json
{
  "segment": "Music Explorer"
}
```

## Run the command-line predictor

Run the application without the `server` argument to enter the metrics interactively:

```bash
python app.py
```

## Retrain the model

To train again using `music_listeners.csv` and regenerate the three `.pkl` artifacts, run:

```bash
python train_model.py
```

Run the training and application commands from this directory so the scripts can find the dataset, template, and model artifacts.
