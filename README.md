

![PyTorch](https://img.shields.io/badge/PyTorch-DeepLearning-red)
![ONNX](https://img.shields.io/badge/ONNX-Export-blue)

# ML4SCI GSoC 2026 — Mass Regression (Task 2f/2g)

This notebook implements an end-to-end pipeline for particle mass regression using CMS detector data, including preprocessing, model training, and ONNX export.


## 🚀 ML4SCI GSoC 2026 — Particle Mass Regression

> End-to-end deep learning pipeline for **particle mass regression** using CMS detector data, with ONNX export for deployment.

---

## 📌 Overview

This project implements a complete pipeline for **mass regression (Task 2f/2g)** using PyTorch, starting from raw CMS detector data in `.parquet` format to a deployable ONNX model.

The focus is on handling **real-world scientific data challenges**, including memory constraints, nested data structures, and sparse detector representations.

---

## 🧠 Key Contributions

* ✅ Efficient **row-group streaming** for large parquet dataset
* ✅ Reconstruction of **detector data into image format**
* ✅ Selection of relevant physics channels (**Track pT, ECAL**)
* ✅ CNN-based regression model
* ✅ Stable training via **target normalization**
* ✅ Exported model to **ONNX for inference compatibility**

---

## ⚙️ Methodology

### 🔹 Data Processing

* Used **PyArrow** to load parquet data incrementally
* Handled **nested object arrays** via custom flattening
* Reconstructed sparse detector data into:

```text
(2, 125, 125)
```

---

### 🔹 Model Architecture

* Lightweight CNN:

  * 3 Conv layers + ReLU + MaxPooling
  * Fully connected regression head
* Designed for **sparse and structured physics data**

---

### 🔹 Training Setup

* Train/Test split: **80/20**
* Loss: **Mean Squared Error (MSE)**
* Optimizer: **Adam**
* Applied **target normalization**

---

## 📊 Results & Analysis


<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/b79c48a3-abab-490e-8ab5-4270519fbb2e" />


### Training Analysis

The training and validation losses remain stable across epochs, indicating convergence.  
However, limited improvement suggests constraints due to:
- Small dataset size  
- Simplified detector reconstruction  

Future improvements include using full spatial mapping and larger datasets.


* Achieved stable training with loss ≈ **0.95**
* Training and validation curves show **early convergence**

📌 Insight:

> Performance is limited by small dataset size and simplified spatial reconstruction. Incorporating full detector geometry (ieta, iphi) and larger datasets would significantly improve accuracy.

---

## 📦 ONNX Export

The trained model is exported for deployment:

```bash
mass_model.onnx
```

* Compatible with inference frameworks (e.g., CMSSW)
* Exported using latest ONNX opset

---

## 🚧 Challenges & Solutions

| Challenge            | Solution             |
| -------------------- | -------------------- |
| Large dataset        | Row-group streaming  |
| Nested arrays        | Custom flattening    |
| Sparse detector data | Image reconstruction |
| Memory limits        | Subset training      |

---

## 🔮 Future Work

* Train on full dataset
* Use full `(ieta, iphi)` mapping
* Explore deeper architectures (ResNet)
* Add evaluation metrics (MAE, RMSE)

---

## 👨‍💻 Author

**Md Aquib Hussain**
B.Tech Robotics & Automation, REVA University

---

## ⭐ Acknowledgements

* ML4SCI
* CERN Open Data

---

