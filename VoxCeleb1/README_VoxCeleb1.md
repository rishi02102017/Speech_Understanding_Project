
# Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition  
**Dataset: VoxCeleb1**  
**Authors:** Jyotishman Das, Pranjal Malik  
**Course Instructor:** Dr. Richa Singh  
**Course:** Speech Understanding
**Institute:** Indian Institute of Technology Jodhpur  


---

## 🔍 Project Overview

This project implements and evaluates multiple temporal modeling architectures for **continuous emotion recognition**. The core idea is inspired by the paper _"Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition"_ by Huang et al., with the goal of comparing different neural network architectures in their ability to track emotion dynamics over time.

Due to the unavailability of real-time continuous emotion datasets like **AVEC 2017** or **SEWA**, we use the **VoxCeleb1** dataset and synthetically simulate emotion trajectories (arousal and valence) for experimentation.

---

## 🎯 Objective

To benchmark and compare **7 different temporal architectures** for continuous prediction of **arousal and valence**, focusing on:
- How well different models capture long-range temporal dependencies
- Quantitative performance in terms of **Mean Squared Error (MSE)** and **Concordance Correlation Coefficient (CCC)**

---

## 📦 Dataset Used: VoxCeleb1

- Source: [VoxCeleb1](http://www.robots.ox.ac.uk/~vgg/data/voxceleb/)
- Type: Clean speech utterances from real speakers
- Labels: Since real emotion labels are unavailable, we **generate synthetic continuous values** for **arousal** and **valence** using smooth sinusoidal or controlled noise signals.

---

## 🧪 Feature Extraction

- We extract **88-dimensional eGeMAPS features** for each utterance using the **openSMILE toolkit**.
- Only one feature vector is computed per utterance (i.e., no frame-level variation).

---

## 🏗️ Models Implemented

We implemented the following temporal architectures using **TensorFlow**:

### Individual Models:
1. **LSTM**: 2 stacked LSTM layers with 64 hidden units  
2. **TDNN**: 4 stacked 1D dilated convolutions (kernel size 3)  
3. **Multi-head Attention**: 2 layers of attention with 4 heads each  

### Combined Models:
4. **TDNN + LSTM**  
5. **Attention + TDNN**  
6. **Attention + LSTM**  
7. **Attention + TDNN + LSTM**  

Each model ends with a sigmoid activation to output continuous values in the [0, 1] range.

---

## ⚙️ Training Configuration

- Optimizer: **Adam**
- Loss: **Mean Squared Error (MSE)**
- Batch Size: **3**
- Epochs: **70**
- Evaluation Metrics:
  - **Mean Squared Error (MSE)**
  - **Concordance Correlation Coefficient (CCC)**

---

## 📊 Evaluation Strategy

Each model is trained **separately** for **arousal** and **valence** using the synthetic targets.

We plot:
- **Validation Loss vs Epoch** for each model
- **Bar graphs comparing MSE and CCC across models**
- **Synthetic Ground Truth vs Model Prediction** for selected utterances

---

## 📈 Results (Summary)

| Model                     | Arousal MSE | Arousal CCC | Valence MSE | Valence CCC |
|--------------------------|-------------|--------------|--------------|--------------|
| LSTM                     | 0.0862      | 0.0008       | 0.0776       | 0.0090       |
| TDNN                     | 0.3584      | NaN          | 0.3747       | NaN          |
| Attention                | 0.0862      | NaN          | 0.0768       | -0.0004      |
| TDNN + LSTM              | 0.0862      | NaN          | 0.0780       | NaN          |
| Attention + TDNN         | 0.0862      | NaN          | 0.0779       | NaN          |
| Attention + LSTM         | 0.0862      | -0.0000      | 0.0786       | 0.0181       |
| Attention + TDNN + LSTM  | 0.0861      | -0.0000      | 0.0778       | 0.0261       |

*Note: CCC becomes NaN when the predictions or ground truth are nearly constant — this is common with synthetic datasets and short sequences.*

---

## 📌 Observations

- All models tend to converge to a **flat prediction**, as they are trying to approximate smooth synthetic curves using averaged features.
- TDNN performs poorly in most configurations, while LSTM and attention-based combinations perform more consistently.
- CCC values are very low due to limited temporal variability in synthetic ground truth.

---

## 📎 Limitations

- The use of synthetic emotion labels restricts real-world applicability.
- No time-aligned labels or frame-level dynamics — each utterance is treated as a single timestep.
- Flat predictions are expected due to the lack of temporal variance within utterances.

---

## 📝 Future Work

- Incorporate **frame-level emotion tracking** using continuous annotations.
- Use real emotional datasets like **RECOLA** or **AVEC SEWA** when available.
- Explore multimodal fusion with facial features.

---

## 📚 References

1. J. Huang et al., “Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition,” ICASSP, 2019.  
2. openSMILE Toolkit: https://audeering.github.io/opensmile/

---

