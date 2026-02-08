# 🔬 Hybrid SqueezeNet + SVM for SEM Wafer Defect Classification

**Team Name:** EMBEDDEDX  
**Event:** IESA DeepTech Hackathon  

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python) ![PyTorch](https://img.shields.io/badge/PyTorch-2.0-orange?logo=pytorch) ![Scikit-Learn](https://img.shields.io/badge/scikit--learn-SVM-blue) ![Status](https://img.shields.io/badge/Status-Prototype%20Ready-success)

## 📖 Project Overview
This project introduces a **Hybrid CNN + SVM architecture** for the automatic classification of semiconductor wafer defects using Scanning Electron Microscope (SEM) images. 

Standard manual inspection is slow, error-prone, and non-scalable for sub-7nm nodes. Our solution replaces the standard Softmax classifier of a Convolutional Neural Network (CNN) with a **Support Vector Machine (SVM)** to achieve higher accuracy and better generalization on rare defect classes.

### **Key Features**
* **Lightweight Architecture:** Uses **SqueezeNet 1.1** as a feature extractor (~0.7M parameters).
* **Robust Classification:** Replaces the final fully connected layer with an **SVM (RBF Kernel)**.
* **Edge-Ready:** Total deployment size is **~4MB**, suitable for Raspberry Pi/Jetson Nano.
* **High Performance:** Achieves **98.54% Accuracy** and **0.96 Macro F1-Score**.

---

## 📊 Model Comparison & Results
We evaluated multiple architectures to determine the optimal balance between accuracy, model size, and inference speed. The **SqueezeNet + SVM** hybrid approach outperformed standalone CNN baselines.

| Model Architecture | Parameters | Accuracy (%) | Inference Time | Deployment Size |
|--------------------|------------|--------------|----------------|-----------------|
| **MobileNetV2** | 3.4M       | 97.99%       | ~2.2 ms        | ~14 MB          |
| **GoogLeNet** | 6.6M       | 98.10%       | ~4.1 ms        | ~26 MB          |
| **SqueezeNet (Base)**| 0.7M     | 95.97%       | ~4.7 ms        | ~3 MB           |
| **Hybrid SqueezeNet + SVM** | **0.7M** | **98.54%** | **<50 ms (CPU)** | **~4 MB** |

> **Why SqueezeNet + SVM?** > While GoogLeNet had high accuracy, it is heavy for edge devices. SqueezeNet is 50x smaller but struggled with classification accuracy on its own (95.97%). By using SqueezeNet solely for **feature extraction** and offloading classification to an **SVM**, we boosted accuracy to **98.54%** without increasing model weight significantly.

---

## 📂 Dataset Details
* **Source:** SEM Wafer Defect Dataset
* **Classes (10 Types):** `CMSC_Scuff`, `Clean`, `Clean_Spot`, `Cracks`, `Mixed`, `Particle_Contamination`, `Scratch`, `good`, `pits_voids`, `Cmp`.
* **Preprocessing:** * Resized to 224x224
    * Grayscale conversion
    * Data Augmentation (Flip, Rotation, Color Jitter)

---

## 🛠️ Methodology
1.  **Feature Extraction:** We strip the classifier head from a pre-trained SqueezeNet 1.1 model.
2.  **Forward Pass:** Input images are passed through the CNN to generate a **512-dimensional feature vector**.
3.  **Classification:** These vectors are fed into an SVM (RBF Kernel, $C=10, \gamma=scale$) to predict the final class.

---

## 🚀 Installation & Usage

### **1. Clone the Repository**
```bash
git clone [https://github.com/KuldeepSharma9351/IESA-Hackathon-EmbeddedX.git](https://github.com/KuldeepSharma9351/IESA-Hackathon-EmbeddedX.git)
cd IESA-Hackathon-EmbeddedX
