# Gaussian Modeling for Uterine Tissue Classification Using Near-Infrared Spectroscopy

This project implements a complete pipeline for classifying five uterine tissue types using near-infrared spectroscopy (NIRS). The workflow includes spectral preprocessing, feature standardization, PCA dimensionality reduction, and Gaussian generative modeling. The goal is to evaluate whether simple probabilistic models can serve as interpretable and data-efficient baselines for uterine pathology classification.

---

## Project Overview

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

## Spectral Preprocessing Pipeline

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







