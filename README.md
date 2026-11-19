# SignBridge AI

SignBridge AI is an experimental American Sign Language (ASL) hand-sign recognition project. It contains Jupyter notebooks for training image- and hand-landmark-based classifiers and trying predictions with a webcam.

> This repository contains experiments, not a finished sign-language translation application. The notebooks recognize individual static hand signs; they do not interpret continuous signing, grammar, or full sentences.

## Project contents

- `HandTracking.ipynb` — image-based CNN experiments for alphabet and additional gesture classes.
- `HandTrack.ipynb` — extracts hand landmarks from images and trains an MLP classifier.
- `hand.ipynb` — extracts MediaPipe hand landmarks, trains a Random Forest classifier, and includes a webcam prediction example.
- `asl_cnn.pth`, `asl_landmark_model.pkl`, `label_map.pkl`, `scaler.pkl` — saved model artifacts. The notebooks may overwrite some of these when run.

## Requirements

- Windows, macOS, or Linux
- Python 3.10 or 3.11 recommended
- A webcam for the live prediction cells
- A working Jupyter environment

Create and activate a virtual environment, then install the packages:

```bash
python -m venv .venv
```

On Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On macOS or Linux:

```bash
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PyTorch installation fails for your platform, install the matching `torch` and `torchvision` builds using the official [PyTorch installation selector](https://pytorch.org/get-started/locally/), then install the remaining packages from `requirements.txt`.

## Dataset setup

The image datasets are intentionally not included in this repository. They take up over 1 GB and may have separate usage or redistribution terms. Obtain datasets from their original sources, review their licenses, and arrange the folders locally as needed by each notebook:

```text
SignBridge/
├── asl_dataset/       # uppercase class folders; used by HandTrack.ipynb
├── asl_dataset1/      # lowercase class folders; used by hand.ipynb
├── image/             # uppercase letters and gesture folders; used by HandTracking.ipynb
├── HandTrack.ipynb
├── HandTracking.ipynb
└── hand.ipynb
```

The exact folder names and label sets are hard-coded in the notebooks. If your dataset uses a different layout or labels, update the corresponding dataset path and label mapping before running training cells. `HandTrack.ipynb` writes `landmarks.csv` in the project directory.

## Run the notebooks

From the project directory, start Jupyter:

```bash
python -m jupyter notebook
```

Open a notebook and run its cells in order. Training cells expect the corresponding dataset folders above. The webcam examples use camera device `0`; close other programs using the camera and press `q` in the video window to stop a live prediction loop.

The notebooks are independent experiments and use different datasets, label mappings, and model approaches. Select the notebook whose dataset and output you intend to use. Check any model or scaler filenames in its cells before loading saved artifacts, because some notebooks reuse filenames.

## Repository contents and data

Dataset folders, generated feature CSV files, and Python cache files are ignored by Git. Add data only if you have the right to redistribute it, and prefer a documented dataset download/setup process over committing large image collections.

## Limitations

- These notebooks are prototypes and may need adjustments for your dataset, dependency versions, or hardware.
- Accuracy depends on training data and recording conditions; predictions are not guaranteed to be correct.
- This project is not a substitute for an interpreter or accessibility service.
