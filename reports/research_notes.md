# Signal-processing research notes

## Research question

How do sampling, window length, smoothing, and simple time- and frequency-domain summaries change what we can see in accelerometer and gyroscope signals?

## Objective

Practice a transparent signal-processing workflow before machine learning. This lab does not repeat the activity-classification model from `wearable-ai-101` and does not detect fatigue, driver strain, or safety risk.

## Dataset and source

UCI Human Activity Recognition Using Smartphones: <https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones>. The source README documents three-axis measurements at 50 Hz, 128 samples per 2.56-second window, 50% overlap, acceleration in units of gravity (`g`), and gyroscope angular velocity in radians per second. The original train/test split and activity labels are used.

## Methods

The notebooks load the nine inertial signal files per split (three axes for total acceleration, body acceleration, and body gyroscope), validate row alignment and 128 samples per row, and visualize individual labeled windows. Notebook 02 applies an illustrative moving average and an additional low-pass Butterworth filter to an already preprocessed dataset signal. It computes mean, population standard deviation, minimum, maximum, RMS, vector magnitude, and a Hann-windowed single-sided FFT amplitude spectrum. Feature and spectrum summaries are compared across activity labels and window sizes.

## Results

Both notebooks' code cells were executed against the inspected UCI files. The checks found 7,352 training and 2,947 test windows, with nine signal matrices per split and 128 samples per row. For 128 samples at 50 Hz, FFT-bin spacing is 0.3906 Hz.

Notebook 02's mean body-acceleration magnitude RMS across the 7,352 training windows was:

| Activity | Mean RMS magnitude (g) |
|---|---:|
| LAYING | 0.0317 |
| SITTING | 0.0237 |
| STANDING | 0.0222 |
| WALKING | 0.3161 |
| WALKING_DOWNSTAIRS | 0.4458 |
| WALKING_UPSTAIRS | 0.3498 |

For the example WALKING window selected by Notebook 02 (training row 78), body-acceleration X RMS was 0.21880 g for the supplied signal, 0.17133 g after a 5-sample moving average, and 0.17868 g after the illustrative 5 Hz Butterworth filter. This is one window, so it demonstrates filter effects rather than a typical activity-level change.

## Observations from this run

- In these training windows, mean body-acceleration magnitude RMS is much higher for the three walking labels than for sitting, standing, or laying. This is a descriptive difference in this dataset, not a fatigue measure or a classifier result.
- Smoothing reduced the RMS of the selected example X-axis segment. Filter choice changes signal amplitude; the result depends on the chosen window, width, and cutoff.
- FFT-bin spacing is 50/N Hz: 1.5625 Hz for 32 samples, 0.78125 Hz for 64, and 0.390625 Hz for 128. Shorter windows give coarser frequency spacing and more local summaries.

## Limitations

- The data consists of pre-segmented smartphone signals, not continuous wearable recordings.
- Neighboring 2.56-second windows overlap by 50%; window boundaries affect statistics and spectra.
- The published inertial signals have already been filtered and gravity-separated as described in the UCI documentation. Filters in this lab are additional demonstrations, not recovery of raw sensor measurements.
- Filter choice can attenuate real movement, shift timing in causal use, and create edge artifacts.
- FFT summaries depend on the selected segment, detrending, window function, and window length.
- Activity differences in this dataset do not imply fatigue or driver-strain differences.
- No Formula 1 telemetry, fatigue target, medical validation, or motorsport safety evidence is present.

## Future learning directions

Study sampling and aliasing, filter frequency response and phase delay, window functions and spectral leakage, sensor calibration, and participant-independent evaluation. Before any driver-monitoring research, define an ethically sound target and collect appropriate synchronized, representative measurements with domain experts.
