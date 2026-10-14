# About

This project demonstrates unsupervised learning by grouping music listeners into behavioral segments with a three-cluster K-Means model.

## Features used

The model uses four listener metrics from `music_listeners.csv`:

- Listening hours per week
- Songs per day
- Skip rate
- Playlist count

The training script standardizes these features before fitting K-Means. At prediction time, the saved scaler applies the same transformation, and a saved cluster mapping presents the result as one of three readable labels: **Casual Listener**, **Music Explorer**, or **Heavy Listener**.

## Project contents

- `app.py` — Flask web interface, JSON prediction endpoint, and interactive terminal predictor
- `train_model.py` — trains the model and writes the serialized artifacts
- `dataset.py` — dataset helper
- `music_listeners.csv` and `music_listeners.xlsx` — sample listener data
- `model.pkl`, `scaler.pkl`, and `cluster_mapping.pkl` — pre-trained model and inference artifacts
- `templates/index.html` — web form
- `requirements.txt` — Python dependencies
- `INSTRUCTIONS.md` — installation and run instructions

The project is intended as a learning example; its predicted labels describe clusters inferred from the supplied data rather than verified user categories.
