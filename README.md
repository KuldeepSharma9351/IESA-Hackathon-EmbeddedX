# SEM Wafer Defect Detection – Detailed Results and Analysis

This document presents a comprehensive analysis of experiments conducted for automatic classification of semiconductor wafer defects using Scanning Electron Microscope (SEM) images. Multiple deep learning architectures were evaluated under a unified preprocessing and training framework. Further optimization was performed using epoch-wise training and a hybrid CNN–SVM approach to improve classification robustness and generalization.

---

## 1. Overall Experimental Workflow

The objective of this work was to design a high-accuracy yet deployment-efficient SEM wafer defect classification system. Instead of directly optimizing a single model, a systematic multi-stage workflow was followed to ensure fairness and experimental validity.

The complete workflow consists of the following stages:

1. Initial benchmarking of multiple CNN architectures  
2. Comparative evaluation using a fixed dataset and common metrics  
3. Model selection based on accuracy–efficiency trade-off  
4. Class refinement to address imbalance  
5. Epoch-wise optimization  
6. Hybrid CNN–SVM enhancement  

This step-by-step approach ensures that the final model choice is data-driven, explainable, and experimentally justified, which is critical for hackathon evaluation.

---

## 2. Dataset and Preprocessing

The SEM wafer dataset consists of grayscale SEM images representing various wafer defect and non-defect patterns. Initially, the dataset contained 11 classes:

CMSC_Scuff, Clean, Clean_Spot, Cmp, Cracks, Mixed, Particle_Contamination, Ring_Heavy Spot, Scratch, good, and pits_voids.

All images were:

- Converted to single-channel grayscale  
- Resized to 224 × 224 pixels  
- Normalized before training  

To improve generalization and reduce overfitting, the following data augmentation techniques were applied during training:

- Horizontal and vertical flipping  
- Rotation  
- Affine transformations  
- Color jittering  

The same preprocessing and augmentation pipeline was used for all models to ensure a fair comparison.

---

## 3. Initial Model Benchmarking (11-Class Setup)

### 3.1 Models Evaluated

In the first stage, multiple state-of-the-art CNN architectures were trained and evaluated on the same 11-class dataset using identical training and evaluation settings.

The goal of this stage was not only to maximize accuracy, but also to analyze computational efficiency, architectural behavior, and deployment feasibility.

The following models were evaluated using transfer learning with ImageNet-pretrained weights adapted for grayscale input:

- AlexNet  
- EfficientNet-B0  
- MobileNetV2  
- GoogLeNet (Inception v1)  
- SqueezeNet (CNN-only)  

Weighted cross-entropy loss was used to address class imbalance, and all models were evaluated on a fixed test set.

---

### Model Performance Summary

| Model | Accuracy (%) | Key Characteristics |
|-----|-------------|-------------------|
| AlexNet | ~92.0 | Older architecture, large parameter count, lower generalization |
| EfficientNet-B0 | ~98.0 | High accuracy, compound scaling, computationally heavier |
| MobileNetV2 | 97.99 | Lightweight, fast inference, mobile-friendly |
| GoogLeNet | 98.10 | Strong feature extraction, higher architectural complexity |
| SqueezeNet (CNN-only) | 95.97 | Extremely small model, lowest parameter count |

---

### 3.3 Observations

- AlexNet achieved the lowest accuracy due to its outdated architecture, making it unsuitable for fine-grained SEM defect classification.  

- EfficientNet-B0 achieved high accuracy but required higher computational resources, limiting its suitability for edge or real-time deployment.  

- GoogLeNet provided the best pure CNN accuracy but at the cost of increased complexity.  

- MobileNetV2 demonstrated an excellent balance between accuracy and inference speed.  

- SqueezeNet, although slightly lower in baseline accuracy, stood out due to its extreme parameter efficiency and very low memory footprint, making it an ideal candidate for further optimization.
