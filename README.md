# EEG Signal Processing and Visualization Pipeline

This project implements a comprehensive pipeline for processing and visualizing EEG (Electroencephalogram) signals, specifically designed for the HMS Harmful Brain Activity Classification competition. The pipeline includes signal preprocessing, advanced feature extraction, and spectrogram generation using wavelet transforms.

## Features

- **Signal Processing**
  - Bandpass filtering (0.5-40 Hz)
  - Notch filtering for power line interference (60 Hz)
  - Automated handling of NaN values and signal artifacts
  - Cubic/linear interpolation for short gaps

- **Advanced Analysis**
  - Continuous Wavelet Transform (CWT) with Morlet wavelets
  - Channel-specific metrics calculation:
    - Signal power
    - Signal-to-Noise Ratio (SNR)
    - Spectral Edge Frequency (SEF95)
    - Wavelet energy
  - Weighted channel combination based on signal quality

- **Visualization**
  - Time-frequency spectrograms
  - Multiple duration windows (10s and 50s)
  - Color-mapped visualization using cv2
  - Support for both bipolar and reference montages

## Requirements

```python
pandas
numpy
opencv-python
tqdm
matplotlib
scipy
torch
cupy
kagglehub
```

## Project Structure

- `EEGProcessor`: Main class for signal processing
- `Morlet`: Wavelet implementation for time-frequency analysis
- Data preprocessing utilities
- Visualization tools

## Usage

1. **Data Preparation**
```python
from eeg_processor import EEGProcessor
processor = EEGProcessor(device='cuda')
```

2. **Process EEG Data**
```python
# Load and preprocess EEG data
processed_signals, weights = processor.process_channels(
    eeg_data, 
    bipolar_pairs, 
    reference_pairs
)
```

3. **Generate Spectrograms**
```python
spectrogram_img, weights = processor.create_spectrogram_image(
    eeg_data,
    start_time,
    duration=duration,
    bipolar_pairs=bipolar_pairs,
    reference_pairs=reference_pairs
)
```

## Signal Processing Pipeline

1. **Preprocessing**
   - Raw EEG signal input
   - NaN handling and interpolation
   - Filtering (bandpass and notch)

2. **Feature Extraction**
   - Signal power calculation
   - SNR estimation
   - Frequency analysis
   - Wavelet transformation

3. **Visualization**
   - Spectrogram generation
   - Channel weighting
   - Image creation

## Key Components

### EEGProcessor Class
The main processing class that handles:
- Signal filtering
- Metric calculation
- Spectrogram generation
- Channel weighting

### Morlet Wavelet
Implementation of the Morlet wavelet for time-frequency analysis:
- Configurable central frequency
- Scale-to-frequency conversion
- Complete and incomplete wavelet forms

## Data Processing Statistics

The pipeline includes comprehensive statistics tracking:
- Number of processed files
- NaN value handling
- Interpolation statistics
- Error logging

## Visualization Examples

The project includes visualization capabilities for:
- Different time windows (10s and 50s)
- Multiple brain activity patterns:
  - Seizures
  - LPDs (Lateralized Periodic Discharges)
  - GPDs (Generalized Periodic Discharges)
  - LRDAs (Lateralized Rhythmic Delta Activity)
  - GRDAs (Generalized Rhythmic Delta Activity)

## Contributing

Feel free to submit issues and enhancement requests!
