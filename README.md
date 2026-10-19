# CA-CFAR Detector (MATLAB)

A simple Cell-Averaging Constant False Alarm Rate (CA-CFAR) detector applied to a synthetic radar range profile.

## What it does

A radar range profile contains noise in every cell and target echoes in a few. A fixed detection threshold either misses weak targets or triggers on noise, especially when the noise level varies. CFAR estimates the noise locally around each cell under test (CUT) and scales the threshold to keep the probability of false alarm constant.

```
[ training | guard | CUT | guard | training ]
```

Training cells are averaged to estimate the noise. Guard cells are excluded so target energy leaking into neighboring cells does not inflate the estimate.

Threshold:

T = alpha * mean(training cells), with alpha = N * (Pfa^(-1/N) - 1)

where N is the total number of training cells.

## Test signal

- 1000 range cells of exponentially distributed noise (mean power 1)
- Targets at cell 200 (15 dB), cell 500 (20 dB) and cell 800 (10 dB)

## Parameters

| Parameter | Value |
|-----------|-------|
| Training cells per side | 16 |
| Guard cells per side | 2 |
| Pfa | 1e-4 |

## How to run

Open `ca_cfar_demo.m` in MATLAB (or MATLAB Online) and run it. No toolboxes are required. The script prints the detected cells and plots the signal, the CFAR threshold and the detections.

## Next steps

- Measure false alarm rate over many runs and compare with the design Pfa
- Add OS-CFAR and compare behavior with closely spaced targets
- Plot probability of detection versus SNR
