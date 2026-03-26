

---

# 🚀 ML4SCI GSoC 2026 — Particle Mass Regression

End-to-end deep learning pipeline for **particle mass regression** using CMS detector data, implemented in PyTorch and exported to ONNX for deployment.

---

## 📌 Overview

This project solves the **mass regression task (Task 2f/2g)** from ML4SCI by building a complete pipeline:

* Efficient data loading from large `.parquet` files
* Reconstruction of detector data into image format
* CNN-based regression model
* Model export to ONNX for inference compatibility

---

## 🧠 Approach

### 🔹 Data Loading

* Dataset provided in **Parquet format**
* Used **PyArrow row-group streaming** to avoid memory overflow
* Loaded subset of data (200–500 samples) for efficient experimentation

---

### 🔹 Data Preprocessing

* Each sample contains detector information in nested format
* Reconstructed into image representation of shape:

```text
(Channels, Height, Width) = (2, 125, 125)
```

* Selected only required channels:

  * **Track pT**
  * **ECAL**

* Used **ieta mapping** to place values into spatial grid

---

### 🔹 Model Architecture

A lightweight CNN designed for sparse detector data:

* 3 Convolutional layers + ReLU + MaxPooling
* Fully connected layers for regression output
* Input shape: `(2, 125, 125)`
* Output: scalar mass value

---

### 🔹 Training

* Train/Test Split: **80/20**
* Loss Function: **Mean Squared Error (MSE)**
* Optimizer: **Adam**
* Target normalization applied for stable training

---

## 📊 Results

* Stable training achieved with normalized loss ≈ **0.95**
* Model successfully learns mass regression from limited dataset

> Note: Training performed on subset due to memory constraints.

---

## 📦 ONNX Export (Task 2g)

The trained model is exported to ONNX format:

```bash
mass_model.onnx
```

This enables compatibility with inference frameworks such as **CMSSW**.

---

## ⚙️ Installation

```bash
pip install -r requirements.txt
```

---

## ▶️ Usage

Run the notebook:

```bash
notebook.ipynb
```

Steps included:

1. Data loading
2. Preprocessing
3. Model training
4. Evaluation
5. ONNX export

---

## 📁 Project Structure

```bash
ml4sci-mass-regression/
│
├── notebook.ipynb
├── mass_model.onnx
├── README.md
├── requirements.txt
```

---

## 🚧 Challenges & Solutions

* Handling **large parquet dataset** → solved using row-group streaming
* Decoding **nested object arrays** → implemented custom flattening
* Reconstructing **sparse detector data** → used coordinate-based mapping
* Ensuring **ONNX compatibility** → exported model with correct opset

---

## 🔮 Future Work

* Train on full dataset for improved accuracy
* Use full `(ieta, iphi)` mapping for better spatial reconstruction
* Experiment with deeper CNN / ResNet architectures
* Add evaluation metrics like MAE / RMSE

---

## 👨‍💻 Author

**Md Aquib Hussain**
B.Tech Robotics & Automation, REVA University

---

## ⭐ Acknowledgements

* ML4SCI (Machine Learning for Science)
* CERN Open Data

---
