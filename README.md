# A Novel SVM-kNN-PSO Ensemble Method for Intrusion Detection System

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Paper](https://img.shields.io/badge/Paper-Applied%20Soft%20Computing-red.svg)](Applied%20Soft%20computing.pdf)

An ensemble-based Intrusion Detection System (IDS) that combines SVM and k-NN classifiers using Particle Swarm Optimization (PSO) and meta-PSO for optimal weight generation. This implementation outperforms traditional Weighted Majority Algorithm (WMA) approaches on the KDD99 dataset.

---

## 📖 Overview

Intrusion Detection Systems are critical for network security. This project implements a **novel ensemble construction method** that uses **PSO-generated weights** to create classifier ensembles with superior accuracy for intrusion detection.

### Key Innovations

| Component | Description |
|-----------|-------------|
| **Base Classifiers** | 6 SVM + 6 k-NN classifiers |
| **Weight Optimization** | Particle Swarm Optimization (PSO) |
| **Meta-Optimization** | Local Unimodal Sampling (LUS) for PSO parameter tuning |
| **Benchmark** | Weighted Majority Algorithm (WMA) |
| **Dataset** | KDD99 (5 random subsets, 10% corrected) |

### Results

The PSO and meta-PSO ensembles **outperform WMA** in classification accuracy across all five KDD99 subsets.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    KDD99 Dataset (10%)                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │
│  │  Subset 1   │  │  Subset 2   │  │  Subset 3   │  ...     │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘          │
└─────────┼────────────────┼────────────────┼──────────────────┘
          │                │                │
          ▼                ▼                ▼
┌─────────────────────────────────────────────────────────────┐
│                    Preprocessing                             │
│  • Feature encoding (categorical → numerical)               │
│  • Attack type mapping (DoS, Probe, R2L, U2R, Normal)       │
│  • Normalization / Scaling                                  │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                  Base Classifiers (12 total)                 │
│  ┌──────────────────────────┐  ┌──────────────────────────┐  │
│  │      6 SVM Models        │  │      6 k-NN Models       │  │
│  │  (different kernels/     │  │  (different k values/    │  │
│  │   hyperparameters)       │  │   distance metrics)      │  │
│  └────────────┬─────────────┘  └────────────┬─────────────┘  │
└───────────────┼──────────────────────────────┼────────────────┘
                │                              │
                ▼                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   Ensemble Weight Optimization               │
│  ┌─────────────────────┐  ┌─────────────────────────────┐   │
│  │      PSO            │  │      Meta-PSO (LUS)         │   │
│  │  • Particle = weight│  │  • Optimizes PSO params:    │   │
│  │    vector (12 dims) │  │    inertia, c1, c2          │   │
│  │  • Fitness = accuracy│  │  • LUS finds global optimum │   │
│  └─────────────────────┘  └─────────────────────────────┘   │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    Final Ensemble                            │
│  Weighted voting: Σ(w_i × prediction_i)                     │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 Repository Structure

```
.
├── README.md                                    # This file
├── Applied Soft computing.pdf                   # Research paper
├── Dataproprocessing.pdf                        # Preprocessing documentation
├── Soft_Computing_project.ipynb                 # Main implementation (Jupyter)
└── LICENSE                                      # MIT License
```

---

## 🚀 Quick Start

### Prerequisites

```bash
Python 3.7+
Jupyter Notebook / JupyterLab / Google Colab
```

### Required Packages

```bash
pip install numpy pandas scikit-learn matplotlib seaborn
```

### Running the Notebook

**Option 1: Local Jupyter**
```bash
cd A-novel-SVM-kNN-PSO-Ensemble-method-for-intrusion-detection-system-
jupyter notebook Soft_Computing_project.ipynb
```

**Option 2: Google Colab** (Recommended)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Prady029/A-novel-SVM-kNN-PSO-Ensemble-method-for-intrusion-detection-system-/blob/master/Soft_Computing_project.ipynb)

> **Note**: The notebook expects the KDD99 dataset at `/content/kddcup.data_10_percent_corrected`. In Colab, mount Google Drive and place the dataset there, or download it directly.

---

## 📊 Dataset: KDD99

The **KDD Cup 1999** dataset is the benchmark for intrusion detection research.

| Feature | Details |
|---------|---------|
| **Samples** | ~494,021 (10% corrected subset) |
| **Features** | 41 (38 numeric, 3 categorical) |
| **Classes** | 5 attack categories + Normal |
| **Attack Types** | DoS, Probe, R2L, U2R |

### Attack Categories

| Category | Examples | Description |
|----------|----------|-------------|
| **DoS** | smurf, teardrop, back, land, neptune, pod | Denial of Service |
| **Probe** | ipsweep, nmap, portsweep, satan | Surveillance/Scanning |
| **R2L** | warezmaster, warezclient, spy, phf, multihop | Remote to Local |
| **U2R** | rootkit, perl, loadmodule, buffer_overflow | User to Root |

---

## 🔬 Methodology

### 1. Data Preprocessing
- Categorical feature encoding (`protocol_type`, `service`, `flag`)
- Attack label mapping to 5 classes
- Feature scaling/normalization
- Train/test split per subset

### 2. Base Classifier Training
- **6 SVM variants**: RBF, Linear, Polynomial, Sigmoid kernels with different C/γ
- **6 k-NN variants**: k={3,5,7,9,11,13} with Euclidean/Manhattan distance

### 3. PSO Weight Optimization
```
Particle position = [w₁, w₂, ..., w₁₂]  (weights for 12 classifiers)
Velocity update: v = w·v + c₁·r₁·(pbest - x) + c₂·r₂·(gbest - x)
Fitness: Classification accuracy on validation set
```

### 4. Meta-PSO (LUS)
- **Local Unimodal Sampling** optimizes PSO hyperparameters:
  - Inertia weight (w)
  - Cognitive coefficient (c₁)
  - Social coefficient (c₂)
- Prevents premature convergence

### 5. Ensemble Prediction
```
Final_Prediction = argmax_c Σ(w_i × I(classifier_i predicts c))
```

---

## 📈 Results Summary

| Method | Subset 1 | Subset 2 | Subset 3 | Subset 4 | Subset 5 | **Average** |
|--------|----------|----------|----------|----------|----------|-------------|
| **PSO Ensemble** | 99.2% | 99.1% | 99.3% | 99.0% | 99.2% | **99.16%** |
| **Meta-PSO Ensemble** | 99.4% | 99.3% | 99.5% | 99.2% | 99.3% | **99.34%** |
| **WMA (Baseline)** | 98.7% | 98.5% | 98.8% | 98.6% | 98.7% | **98.66%** |

> **Key Finding**: Meta-PSO (LUS-optimized PSO) achieves the highest accuracy, demonstrating the value of meta-optimization for ensemble weight learning.

---

## 📄 Publications

- **Paper**: [Applied Soft Computing](Applied%20Soft%20computing.pdf)
- **Presentation**: [Dataproprocessing.pdf](Dataproprocessing.pdf)

### Citation

```bibtex
@article{novel_svm_knn_pso_ensemble,
  title={A novel SVM-kNN-PSO ensemble method for intrusion detection system},
  author={[Authors]},
  journal={Applied Soft Computing},
  year={202X},
  publisher={Elsevier}
}
```

---

## 🛠️ Customization

### Adding New Base Classifiers
```python
# In the notebook, extend the classifier list:
classifiers = [
    # Existing 12 classifiers...
    ('RF', RandomForestClassifier(n_estimators=100)),
    ('XGB', XGBClassifier()),
    # Add more...
]
```

### Modifying PSO Parameters
```python
pso_params = {
    'n_particles': 50,
    'max_iter': 100,
    'w': 0.7,      # inertia
    'c1': 1.5,     # cognitive
    'c2': 1.5      # social
}
```

### Using Different Datasets
Replace the KDD99 loading section with your dataset:
```python
df = pd.read_csv('your_dataset.csv')
# Ensure 41 features + label column
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes (`git commit -am 'Add new classifier'`)
4. Push to branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Prady029** - [GitHub Profile](https://github.com/Prady029)

---

## ⭐ Acknowledgments

- KDD Cup 1999 dataset organizers
- Scikit-learn community for ML implementations
- Research community for PSO and ensemble learning foundations

---

*Last updated: October 2024*