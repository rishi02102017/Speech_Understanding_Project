
# Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition  
**Dataset: LibriSpeech**  
**Authors:** Jyotishman Das, Pranjal Malik  
**Course Instructor:** Dr. Richa Singh  
**Institute:** Indian Institute of Technology Jodhpur  

---

## 🔍 Project Overview

This project evaluates temporal deep learning architectures for **continuous emotion recognition** using synthetic arousal and valence signals. The goal is to benchmark models on their ability to capture temporal emotional dynamics — even when trained on datasets lacking explicit emotional annotations.

We base our work on the framework from _"Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition"_ by Huang et al. Since LibriSpeech does not provide real-time arousal or valence annotations, we simulate these signals and train models to regress onto them.

---

## 🎯 Objective

To benchmark and compare **seven temporal architectures** for continuous arousal and valence prediction on the LibriSpeech dataset using synthetic labels. Metrics include:

- **Mean Squared Error (MSE)** for regression accuracy
- **Concordance Correlation Coefficient (CCC)** to evaluate consistency

---

## 📦 Dataset Used: LibriSpeech (dev-clean)

- Source: [LibriSpeech ASR corpus](http://www.openslr.org/12)
- Clean, read speech sampled at 16 kHz
- We use the `dev-clean` subset with 500 utterances
- Each utterance is processed into a single averaged eGeMAPS feature vector

As no ground truth arousal/valence is provided, we synthetically generate **smooth sinusoidal target labels** per utterance.

---

## 🧪 Feature Extraction

- Tool: **openSMILE**
- Feature set: **eGeMAPS v02** (88 features)
- Extracted per utterance using WAV conversions and standard configuration
- One CSV feature vector per file

---

## 🏗️ Models Implemented

We implemented and compared the following deep learning architectures in TensorFlow:

### Individual Models:
1. **LSTM** – 2-layer stacked LSTM (64 units)
2. **TDNN** – Time Delay Neural Network with 4 Conv1D layers (dilated)
3. **Multi-head Attention** – 2 blocks with 4 attention heads

### Combined Models:
4. **TDNN + LSTM**
5. **Attention + TDNN**
6. **Attention + LSTM**
7. **Attention + TDNN + LSTM**

All models predict continuous scalar values for both arousal and valence in the range **[0, 1]**.

---

## ⚙️ Training Configuration

- Loss: **Mean Squared Error (MSE)**
- Optimizer: **Adam**
- Epochs: **70**
- Batch size: **3**
- Train-test split: **80-20** on 500 samples

Each model is trained **separately for arousal and valence**. Evaluation includes both MSE and CCC.

---

## 📈 Results Summary: LibriSpeech

| Model                     | Arousal MSE | Arousal CCC | Valence MSE | Valence CCC |
|--------------------------|-------------|--------------|--------------|--------------|
| LSTM                     | 0.0862      | 0.0008       | 0.0776       | 0.0090       |
| TDNN                     | 0.3584      | NaN          | 0.3747       | NaN          |
| Attention                | 0.0862      | NaN          | 0.0768       | -0.0004      |
| TDNN + LSTM              | 0.0862      | NaN          | 0.0780       | NaN          |
| Attention + TDNN         | 0.0862      | NaN          | 0.0779       | NaN          |
| Attention + LSTM         | 0.0862      | -0.0000      | 0.0786       | 0.0181       |
| Attention + TDNN + LSTM  | 0.0861      | -0.0000      | 0.0778       | 0.0261       |

*Note: CCC becomes NaN when predictions or ground truth values are nearly constant, which is common in synthetic or smoothed datasets.*

---

## 📌 Observations

- Flat model outputs are expected due to the nature of synthetic sinusoidal targets and single timestep input.
- TDNN struggles to fit the targets, showing significantly worse MSE than other models.
- Attention + LSTM and Attention + TDNN + LSTM yield the best CCC scores for valence.

---

## 📎 Limitations

- The use of **synthetic targets** limits real-world generalization.
- No per-frame temporal dynamics were modeled since each utterance maps to a single label.
- Realistic emotional fluctuations cannot be fully captured without annotated datasets.

---

## 📝 Future Work

- Integrate real-time annotated datasets like **AVEC**, **RECOLA**, or **SEWA**.
- Use frame-level emotional targets for finer temporal modeling.
- Extend to multimodal emotion recognition by incorporating visual cues.

---

## 📚 References

1. Huang et al., “Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition,” ICASSP, 2019.  
2. Eyben et al., openSMILE: The Munich Versatile and Fast Open-Source Audio Feature Extractor.

---
