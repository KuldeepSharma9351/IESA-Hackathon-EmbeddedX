# 🧠 SEM Wafer Defect Detection – Detailed Results and Analysis  

This repository presents a comprehensive experimental study on **automatic classification of semiconductor wafer defects using Scanning Electron Microscope (SEM) images**.  

Multiple deep learning architectures were evaluated under a unified preprocessing and training framework. Further optimization was performed using **epoch-wise training** and a **hybrid CNN–SVM approach** to improve classification robustness and generalization.

---

## 📌 Objective  

To design a **high-accuracy, lightweight, and deployment-efficient SEM wafer defect classification system** by following a systematic, multi-stage experimental workflow rather than directly optimizing a single model.

This methodology ensures that the final model choice is:

- Data-driven  
- Explainable  
- Experimentally justified  
- Suitable for hackathon and real-world deployment  

---

## 🔁 Overall Experimental Workflow  

The complete workflow consists of the following stages:

1. Initial benchmarking of multiple CNN architectures  
2. Comparative evaluation using a fixed dataset and common metrics  
3. Model selection based on accuracy–efficiency trade-off  
4. Class refinement to address imbalance  
5. Epoch-wise optimization  
6. Hybrid CNN–SVM enhancement  

This step-by-step pipeline ensures **fairness, reproducibility, and transparency**.

---

## 📂 Dataset and Preprocessing  

The SEM wafer dataset consists of grayscale SEM images representing various wafer defect and non-defect patterns.

### 🔹 Original Classes (11)

- CMSC_Scuff  
- Clean  
- Clean_Spot  
- Cmp  
- Cracks  
- Mixed  
- Particle_Contamination  
- Ring_Heavy Spot  
- Scratch  
- good  
- pits_voids  

### 🔹 Preprocessing Steps

- Converted to **single-channel grayscale**  
- Resized to **224 × 224 pixels**  
- Pixel value **normalization**

### 🔹 Data Augmentation

Applied during training:

- Horizontal & vertical flipping  
- Rotation  
- Affine transformations  
- Color jittering  

> The same preprocessing and augmentation pipeline was used for all models to ensure a fair comparison.

---

## 🧪 Initial Model Benchmarking (11-Class Setup)

### Models Evaluated

All models used **transfer learning** with ImageNet-pretrained weights adapted for grayscale input:

- AlexNet  
- EfficientNet-B0  
- MobileNetV2  
- GoogLeNet (Inception v1)  
- SqueezeNet (CNN-only)  

**Weighted Cross-Entropy Loss** was used to mitigate class imbalance.

---

## 📊 Performance Comparison

| Model | Accuracy (%) | Key Characteristics |
|------|--------------|-------------------|
| AlexNet | ~92.0 | Older architecture, large parameter count |
| EfficientNet-B0 | ~98.0 | High accuracy, heavier computation |
| MobileNetV2 | 97.99 | Lightweight, fast inference |
| GoogLeNet | 98.10 | Strong feature extraction |
| SqueezeNet (CNN-only) | 95.97 | Extremely small model |

---

## 🔍 Observations

- AlexNet shows weakest performance due to outdated design.  
- EfficientNet-B0 offers excellent accuracy but higher computational cost.  
- GoogLeNet achieves best pure CNN accuracy.  
- MobileNetV2 provides an **excellent balance between accuracy and speed**.  
- SqueezeNet stands out for **extreme parameter efficiency**, making it ideal for further optimization.

---

## ⭐ Conclusion (Stage 1)

SqueezeNet and MobileNetV2 were selected as **primary candidates for advanced optimization** due to their:

- High efficiency  
- Low memory footprint  
- Suitability for edge deployment  

Subsequent stages focus on:

- Epoch-wise tuning  
- Class refinement  
- Hybrid CNN–SVM integration  

---

## 📁 Results Visualization

Confusion matrices and evaluation plots are stored inside:

