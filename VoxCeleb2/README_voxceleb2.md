
# Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition  
**Dataset: VoxCeleb2**  
**Authors:** Jyotishman Das, Pranjal Malik  
**Course Instructor:** Dr. Richa Singh  
**Course:** Speech Understanding
**Institute:** Indian Institute of Technology Jodhpur  

This project explores temporal deep learning architectures for emotion and sentiment prediction based on simulated arousal and valence values derived from eGeMAPS audio features. The VoxCeleb2 dataset is used as a proxy in the absence of large-scale publicly available emotion-annotated speech datasets such as AVEC or SEWA.

## Project Overview

The primary objective is to assess and compare different temporal architectures on the task of predicting arousal from eGeMAPS features extracted from speech data. We simulate arousal and valence labels in the [0, 1] range and focus on test MSE and CCC metrics for performance comparison.

## Dataset

- **VoxCeleb2** (audio-only, speaker verification dataset)
- Simulated arousal and valence values in the range [0, 1]
- Features: eGeMAPS extracted using openSMILE (88-dimensional)

## Architectures Implemented

We experiment with seven architectures:

1. **LSTM**: Stacked LSTM layers for temporal modeling
2. **TDNN**: Time Delay Neural Network with dilated 1D convolutions
3. **Multi-Head Attention**: Transformer-based attention modeling
4. **TDNN + LSTM**: Convolutional temporal modeling followed by LSTM
5. **Attention + TDNN**: Attention layer followed by TDNN stack
6. **Attention + LSTM**: Attention layer followed by stacked LSTMs
7. **Attention + TDNN + LSTM**: Full hybrid model

## Training Details

- Optimizer: Adam
- Loss: MSE
- Batch size: 3
- Epochs: 70
- Evaluation Metrics: Test MSE, Concordance Correlation Coefficient (CCC)

## Results

| Model                      | Test MSE | CCC     |
|---------------------------|----------|---------|
| LSTM                      | 0.0991   | -0.0028 |
| TDNN                      | 0.3277   | -0.0000 |
| Attention                 | 0.1005   |  0.0002 |
| TDNN + LSTM               | 0.0989   | -0.0000 |
| Attention + TDNN          | 0.0990   | -0.0000 |
| Attention + LSTM          | 0.0981   |  0.0924 |
| Attention + TDNN + LSTM   | 0.0988   |  0.0000 |

> Note: All models were trained using only 100 samples for fast experimentation.

## Visualizations

- MSE Comparison Across Models
- Train vs Validation Loss Across Epochs
- CCC Computation and Failure Cases (Discussion of constant predictions)

## Key Takeaways

- Simulating [0, 1] labels improves CCC stability compared to [-1, 1]
- TDNN alone performs poorly for this task
- Attention + LSTM achieved the best CCC of **0.0924**, indicating improved correlation
- LSTM-based and hybrid models offer better generalization with low MSE

## File Structure

- `Speech_Project_VoxCeleb2.ipynb` – Full codebase with training, visualization, and evaluation
- `egemaps_features_vox2/` – Folder containing extracted CSV features
- `X_vox2.npy` – eGeMAPS feature matrix
- `arousal_vox2.npy` – Simulated arousal values (ground truth)
- `valence_vox2.npy` – Simulated valence values (optional)

## Future Work

- Extend the experiments to VoxCeleb1 and LibriSpeech datasets
- Integrate real annotated emotion datasets (e.g., SEWA, RECOLA) if available
- Explore multi-task learning for joint arousal and valence prediction

## Authors

- Jyotishman Das
- Pranjal Malik  

This project was implemented as part of the Speech Understanding course assignment under the guidance of Dr. Richa Singh at IIT Jodhpur.