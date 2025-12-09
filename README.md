# Gaussian Modeling for Uterine Tissue Classification Using Near-Infrared Spectroscopy

This project implements a complete pipeline for classifying five uterine tissue types using near-infrared spectroscopy (NIRS). The workflow includes spectral preprocessing, feature standardization, PCA dimensionality reduction, and Gaussian generative modeling. The goal is to evaluate whether simple probabilistic models can serve as interpretable and data-efficient baselines for uterine pathology classification.

---

## 🔍 Project Overview

Near-infrared spectroscopy provides wavelength–dependent reflectance measurements that encode biochemical and structural tissue information. This project analyzes **91,845 spectra** collected from **95 specimens** across **34 patients**, covering five uterine tissue types:

- **0 — Normal uterus**
- **1 — Endometrial cancer**
- **2 — Fibroid**
- **3 — Leiomyosarcoma**
- **4 — Adenomyosis**

Each spectrum contains **intensity values from 434–1144 nm** (interpolated to 501 points).

The objective is to determine the separability of these classes under a **Gaussian generative model** and compare performance between:

- **Original normalized spectra**
- **First-order derivative spectra**

---


---

## 🧪 Spectral Preprocessing Pipeline

The preprocessing follows four key steps:

1. **Area Normalization**  
   Normalizes each spectrum by its integral from 500–1000 nm.

2. **Low-Pass Filtering**  
   4th-order Butterworth filter (cutoff 0.05π rad/sample) removes high-frequency noise.

3. **First-Order Derivative (Optional)**  
   Enhances local slope changes and morphological differences.

4. **Interpolation**  
   All spectra resampled to integer wavelengths 500–1000 nm (501 points).

These steps produce two feature sets:
- **Original normalized spectra**
- **First-order derivative spectra**

---

## 📉 Dimensionality Reduction

Principal Component Analysis (PCA) is applied after standardization:

- Input dimension: **501**
- Output dimension: **20 PCs**
- PCA is fit only on the training folds (to avoid data leakage)

The transformed features approximate class clusters in a Gaussian-like feature space.

---

## 🤖 Gaussian Generative Classifier

Each tissue class is modeled using:

- Class mean vector:  
  \[
  \mu_c = \frac{1}{N_c}\sum_{i:y_i=c} X_i
  \]

- Covariance matrix with regularization:  
  \[
  \Sigma_c = \operatorname{Cov}(X_i \mid y_i=c) + \epsilon I
  \]

Prediction uses the Maximum A Posteriori (MAP) rule:

\[
\hat{y} = \arg\max_c \ \log \pi_c + \log\mathcal{N}(X \mid \mu_c, \Sigma_c)
\]






