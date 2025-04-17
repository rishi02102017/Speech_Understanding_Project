<h1 align="center">Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition</h1>

<p align="center">
  <img src="Speech.jpg" alt="Speech Understanding" width="500"/>
</p>

---


**Course:** Speech Understanding (CS7460)  
**Institute:** Indian Institute of Technology Jodhpur  
**Course Instructor:** Dr. Richa Singh  
**Authors:** Jyotishman Das and Pranjal Malik  

---

## 📌 Project Overview

This project implements and benchmarks multiple deep learning architectures for the task of **continuous emotion recognition**, focusing on the regression of **arousal** and **valence** signals over time. The work is inspired by the paper:

> _"Efficient Modeling of Long Temporal Contexts for Continuous Emotion Recognition" (Huang et al., ICASSP 2019)_

Due to the absence of real-time emotional annotations in publicly available audio corpora, we simulate emotional trajectories using synthetic continuous signals. Our models are evaluated across three diverse and clean speech datasets:

- **VoxCeleb1**
- **VoxCeleb2**
- **LibriSpeech**

---

## 🎯 Objectives

- Simulate and model continuous **arousal** and **valence** values using speech features
- Evaluate and compare 7 architectures for their ability to model emotional trajectories
- Visualize model predictions and benchmark performance using:
  - **Mean Squared Error (MSE)**
  - **Concordance Correlation Coefficient (CCC)**

---

## 📂 Project Structure

```
Speech Understanding Project/
│
├── VoxCeleb1/
│   ├── Speech_Project_VoxCeleb1.ipynb
│   ├── README_VoxCeleb1.md
│   └── Plots 
│   └── X_vox1.npy
│   └── arousal_vox1.npy
│   └── valence_vox1.npy
|  
├── VoxCeleb2/
│   ├── Speech_Project_VoxCeleb2.ipynb
│   └── README_VoxCeleb2.md
│
├── LibriSpeech/
│   ├── Speech_Project_LibriSpeech.ipynb
│   ├── README_LibriSpeech.md
│   └── plots
│   └── valence_libri.npy
│   └── arousal_libri.npy
│   └── X_libri_.npy
|
└── Poster.pdf
```

---

## 📦 Datasets Used

| Dataset     | Description                        | Ground Truth        |
|-------------|------------------------------------|----------------------|
| VoxCeleb1   | Clean speaker utterances           | Synthetic arousal & valence |
| VoxCeleb2   | Large-scale speaker audio          | Synthetic arousal & valence |
| LibriSpeech | Read speech corpus                 | Synthetic arousal & valence |

All datasets were processed using the **openSMILE** toolkit to extract **eGeMAPS** features. These 88-dimensional feature vectors serve as the input to our models.

---

## 🏗️ Architectures Evaluated

Each dataset includes evaluations of the following models, trained **separately** for arousal and valence:

1. **LSTM** (2-layer)
2. **TDNN**
3. **Multi-Head Attention**
4. **TDNN + LSTM**
5. **Attention + TDNN**
6. **Attention + LSTM**
7. **Attention + TDNN + LSTM**

---

## 📊 Results Summary

### LibriSpeech

| Model                     | Arousal MSE | Arousal CCC | Valence MSE | Valence CCC |
|--------------------------|-------------|--------------|--------------|--------------|
| LSTM                     | 0.0862      | 0.0008       | 0.0776       | 0.0090       |
| TDNN                     | 0.3584      | NaN          | 0.3747       | NaN          |
| Attention                | 0.0862      | NaN          | 0.0768       | -0.0004      |
| TDNN + LSTM              | 0.0862      | NaN          | 0.0780       | NaN          |
| Attention + TDNN         | 0.0862      | NaN          | 0.0779       | NaN          |
| Attention + LSTM         | 0.0862      | -0.0000      | 0.0786       | 0.0181       |
| Attention + TDNN + LSTM  | 0.0861      | -0.0000      | 0.0778       | 0.0261       |

### VoxCeleb1

| Model                     | Arousal MSE | Arousal CCC | Valence MSE | Valence CCC |
|--------------------------|-------------|--------------|--------------|--------------|
| LSTM                     | 0.0862      | 0.0008       | 0.0776       | 0.0090       |
| TDNN                     | 0.3584      | NaN          | 0.3747       | NaN          |
| Attention                | 0.0862      | NaN          | 0.0768       | -0.0004      |
| TDNN + LSTM              | 0.0862      | NaN          | 0.0780       | NaN          |
| Attention + TDNN         | 0.0862      | NaN          | 0.0779       | NaN          |
| Attention + LSTM         | 0.0862      | -0.0000      | 0.0786       | 0.0181       |
| Attention + TDNN + LSTM  | 0.0861      | -0.0000      | 0.0778       | 0.0261       |

### VoxCeleb2

| Model                      | Test MSE | CCC     |
|---------------------------|----------|---------|
| LSTM                      | 0.0991   | -0.0028 |
| TDNN                      | 0.3277   | -0.0000 |
| Attention                 | 0.1005   |  0.0002 |
| TDNN + LSTM               | 0.0989   | -0.0000 |
| Attention + TDNN          | 0.0990   | -0.0000 |
| Attention + LSTM          | 0.0981   |  0.0924 |
| Attention + TDNN + LSTM   | 0.0988   |  0.0000 |

---

## 📈 Visualizations

Each notebook includes:
- **Validation loss plots**
- **Synthetic ground truth vs model predictions**
- **MSE & CCC comparison bar charts**

---

## ⚠️ Limitations

- Synthetic labels limit generalization
- Per-utterance labels only (no temporal signal within utterance)
- CCC values close to zero are expected due to low label variability

---

## 📝 Conclusion

Despite the synthetic nature of the dataset, this project successfully benchmarks various temporal deep learning architectures for continuous emotion modeling, providing a foundation for future work on real-time emotional tracking from audio.

---
