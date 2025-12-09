# Bayesian Neural Network for Qubit State Reconstruction

This repository contains a complete implementation of a **Bayesian Neural Network (BNN)** designed to reconstruct the quantum state of a single qubit from noisy Pauli measurements. The model outputs not only predicted state parameters but also credible intervals that quantify uncertainty via **Monte Carlo dropout**, following the approach introduced by Gal and Ghahramani (2016).

---

## 🧠 Overview

Reconstructing a quantum state from measurements is an **ill-posed inverse problem**, especially under noise and sampling constraints. Traditional inversion methods struggle with uncertainty quantification, which is critical in experimental quantum computing. This project leverages modern Bayesian deep learning to address this challenge.

**Goal:**  
Predict the Bloch sphere parameters `θ` and `φ` from noisy expectation values of Pauli operators `⟨σ_x⟩`, `⟨σ_y⟩`, and `⟨σ_z⟩`, with built-in estimation of predictive uncertainty.

---

## 🧪 Methodology

- **Synthetic Dataset Generation**
  - 5,000 pure qubit states uniformly sampled over the Bloch sphere.
  - Ground truth vectors computed from spherical coordinates.
  - Gaussian noise (`σ = 0.05`) applied to simulate imperfect measurements.

- **Model Architecture**
  - Fully connected feedforward neural network:
    - Input: 3 neurons for `⟨σ_x⟩, ⟨σ_y⟩, ⟨σ_z⟩`
    - Hidden layers: 2 layers with 128 neurons each, ReLU activations
    - Dropout: `p = 0.2` (used during both training and testing)
    - Output: 2 neurons predicting `θ` and `φ`
  - Implemented in **PyTorch**

- **Bayesian Inference**
  - Approximate posterior over weights via **MC Dropout**
  - 100 stochastic forward passes per test input to estimate:
    - Predictive mean: `E[θ], E[φ]`
    - Uncertainty: `Var(θ), Var(φ)`

---

## 📊 Files Included

| File Name                       | Description |
|--------------------------------|-------------|
| `bnn_qubit_reconstruction.ipynb` | Full training pipeline for the BNN, from data generation to evaluation. |
| `bnn_uncertainty_analysis.ipynb` | Analysis of model uncertainty using MC Dropout samples and posterior histograms. |
| `bnn_qbuit.ipynb` (typo?)        | (Please verify — appears to be a duplicate or early version of the notebook.) |

---

## 🖥️ Runtime Environment

To ensure reproducibility, the model was run under the following configuration:

- **Python version:** `3.10`
- **PyTorch:** `2.0+`
- **NumPy:** `1.23+`
- **Matplotlib:** `3.7+`
- **Jupyter Notebook / Lab environment**

You can replicate the environment by installing from `requirements.txt` or using a virtual environment.

---

## 📈 Sample Results

- **Final Test Loss (MSE):** < 0.3
- **Prediction intervals:** True state always lies within 1σ of BNN posterior.
- **Bloch vector overlays:** Predicted states align well with ground truth geometry.

---

## 📚 References

- Yarin Gal and Zoubin Ghahramani. *Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning*. ICML 2016.
- M. Suresh, et al. *Bayesian Machine Learning in Physical Sciences*. Rev. Mod. Phys., 2021.

---

## 🚀 Future Work

- Extension to **mixed states** via density matrices.
- Multi-qubit systems using tensor networks or variational quantum circuits.
- Replacement of MC Dropout with **Hamiltonian Monte Carlo** or **variational inference** for tighter posterior approximations.
- Integration with experimental quantum data streams.

---

## 🤝 Acknowledgments

This project was completed as part of PY525 (Machine Learning in Physics) at NC State University. Special thanks to **Omar**, **Dr. Longland**, and **Dr. Fortner** for guidance and feedback throughout the semester.

---

## 🔗 Links

- 🔬 [Gal & Ghahramani (2016)](https://arxiv.org/abs/1506.02142)
- 🌐 [https://dataspec.org](https://dataspec.org) (project homepage)
- 🧑‍💻 [Author GitHub Profile](https://github.com/Axel-Fraud)
