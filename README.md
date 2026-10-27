# Wearable Signal Lab

This project is the signal-processing follow-up to `wearable-ai-101`. It uses UCI HAR's accelerometer and gyroscope windows to look at what filtering, window length, and simple features do to sensor data. There is no activity classifier in this lab.

The supplied inertial files contain 128 samples per example at 50 Hz, or 2.56 seconds per window. Neighboring windows overlap by 50%. They are segments from the study, not one continuous recording. The signal files have already been filtered and separated into body and total acceleration by the dataset authors; any filter here is an additional demonstration.

## Run it

Use Python 3.10 or newer. From this folder:

```zsh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m jupyter notebook
```

Run `notebooks/01_signal_exploration.ipynb` first, then `notebooks/02_filtering_and_features.ipynb`. In VS Code, choose `.venv/bin/python` for the notebook kernel.

## Find the data

The notebook looks for the UCI HAR folder in this project and its parents, then in the sibling `wearable-ai-101/data/raw/` folder. This lets both projects use one local copy. If the folder is not there, download the archive from [UCI](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones) and extract `UCI HAR Dataset/` under this project's `data/raw/`. More detail is in [data/README.md](data/README.md).

The dataset is not stored in this repository. UCI lists it under CC BY 4.0; keep the source citation with any work based on it. The notebooks check the expected files, split lengths, and samples per window before plotting.

## In the notebooks

The first notebook checks the nine inertial files per split, looks at the six activity labels, and plots acceleration and gyroscope axes from individual examples. The second compares raw and smoothed segments, demonstrates a moving average and Butterworth low-pass filter, and calculates summary statistics, three-axis magnitude, and FFT spectra. Each includes exercises and a glossary.

The notes in [reports/research_notes.md](reports/research_notes.md) summarize the actual run. The activity comparisons are descriptive; this project makes no claims about stress, fatigue, driving, or safety.
