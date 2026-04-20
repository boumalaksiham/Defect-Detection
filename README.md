# Manufacturing Defect Detection System

A computer vision pipeline for detecting surface defects in manufactured products,
built on the MVTec Anomaly Detection dataset. This project simulates a real-world
quality control system of the type used in electronics and industrial manufacturing.

## Business Context

Undetected surface defects in electronics manufacturing lead to product recalls,
warranty claims, and reputational damage. This system flags anomalous products
in real time during inspection, reducing the rate of defective units reaching
downstream assembly or customers.

Estimated business impact: early anomaly detection can reduce manual inspection
labor by up to 40% and catch defect rates that human inspectors miss at high
throughput (source: industry benchmarks in automated optical inspection literature).

---

## Project Structure

```
project1_defect_detection/
    src/
        dataset.py          # Dataset loading and preprocessing
        model.py            # Model architecture (autoencoder + classifier)
        train.py            # Training loop with logging
        evaluate.py         # Evaluation metrics and threshold selection
        inference.py        # Single-image inference utility
        utils.py            # Shared helper functions
    data/
        raw/                # Place MVTec dataset here (see setup below)
        processed/          # Auto-generated during preprocessing
    models/
        checkpoints/        # Saved model weights
    notebooks/
        01_exploration.ipynb
        02_training_demo.ipynb
    dashboard/
        app.py              # Streamlit dashboard
    requirements.txt
    config.yaml
```

---

## Setup Instructions

### 1. Clone and create a virtual environment

```bash
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Download the MVTec Dataset

Download from: https://www.mvtec.com/company/research/datasets/mvtec-ad
Place the extracted folder inside `data/raw/`.

Expected structure:
```
data/raw/mvtec_anomaly_detection/
    bottle/
        train/good/
        test/good/
        test/broken_large/
        ...
    cable/
    ...
```

### 3. Configure the run

Edit `config.yaml` to set the product category, model hyperparameters,
and output directories.

### 4. Train the model

```bash
python src/train.py --config config.yaml
```

### 5. Evaluate

```bash
python src/evaluate.py --config config.yaml --checkpoint models/checkpoints/best_model.pt
```

### 6. Run the dashboard

```bash
streamlit run dashboard/app.py
```

---

## Model Architecture

The system uses a **convolutional autoencoder** trained exclusively on defect-free
(normal) images. At inference time, images with high reconstruction error are
flagged as anomalous. A threshold is calibrated on a validation set to balance
precision and recall.

Optionally, a supervised **ResNet-18 classifier** can be trained when labeled
defect images are available, providing class-level defect categorization
(e.g., scratch, contamination, bent).

---

## Key Metrics

| Metric        | Description                                      |
|---------------|--------------------------------------------------|
| AUROC         | Area under ROC curve for anomaly detection       |
| F1 Score      | Harmonic mean of precision and recall            |
| Threshold     | Reconstruction error cutoff (tunable)            |
| Inference FPS | Frames per second on CPU / GPU                   |

---

## Requirements

See `requirements.txt`. Python 3.9+ recommended.