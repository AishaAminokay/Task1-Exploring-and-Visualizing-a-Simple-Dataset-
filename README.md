#  Task 1 — Exploring and Visualizing the Iris Dataset
**DevelopersHub Corporation — AI/ML Engineering Internship**

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-teal)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

##  Objective
Load, inspect, and thoroughly visualize the **Iris Dataset** to understand:
- Feature distributions across 3 flower species
- Relationships between features
- Which features best separate the species
- Presence of outliers

---

##   Dataset

| Property | Detail |
|:---|:---|
| **Name** | Iris Dataset |
| **Source** | Built-in via `seaborn.load_dataset('iris')` — no download needed |
| **Total Samples** | 150 (50 per class — perfectly balanced) |
| **Features** | 4 numeric features |
| **Target** | 3 species — *setosa*, *versicolor*, *virginica* |
| **Missing Values** | None ✅ |

### Feature Description

| Feature | Description | Unit |
|:---|:---|:---:|
| `sepal_length` | Length of the sepal | cm |
| `sepal_width` | Width of the sepal | cm |
| `petal_length` | Length of the petal | cm |
| `petal_width` | Width of the petal | cm |
| `species` | Flower species **(Target)** | — |

---

##  Analysis Performed

| Step | Analysis | Purpose |
|:---:|:---|:---|
| 1 | Data Loading & Shape Inspection | Understand structure |
| 2 | Missing Value Check | Confirm data quality |
| 3 | Descriptive Statistics | Overall + per-species means |
| 4 | Scatter Plots | Feature pair relationships |
| 5 | Histograms | Value distributions per species |
| 6 | Box Plots | Spread and outlier detection |
| 7 | Correlation Heatmap | Inter-feature linear relationships |
| 8 | Pairplot | All feature combinations at once |
| 9 | Violin Plots | Distribution shape per species |

---

##  Key Results & Findings

### Species Separability
| Feature Pair | Separability |
|:---|:---:|
| `petal_length` vs `petal_width` | ⭐⭐⭐ Excellent |
| `sepal_length` vs `petal_length` | ⭐⭐ Good |
| `sepal_width` vs `sepal_length` | ⭐ Poor |
| `sepal_width` vs `petal_width` | ⭐ Poor |

### Correlation Matrix Summary
| Feature Pair | Correlation |
|:---|:---:|
| `petal_length` ↔ `petal_width` | **+0.96** (very strong) |
| `sepal_length` ↔ `petal_length` | **+0.87** (strong) |
| `sepal_length` ↔ `petal_width` | **+0.82** (strong) |
| `sepal_width` ↔ `petal_length` | **−0.43** (negative) |

### Key Observations

- ✅ **Setosa** is perfectly separable from the other two species using petal dimensions alone
- ⚠️ **Versicolor & Virginica** overlap in sepal features — harder to separate
- 📌 **Petal length and petal width** are the most discriminative features for classification
- 📌 **Sepal width** is the weakest feature — all 3 species heavily overlap
- 🔴 **Outliers** detected in `sepal_width` for the Setosa species (visible in box plots)
- 📊 Dataset is **perfectly balanced** — 50 samples per class

---

##  Libraries Used

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

##  How to Run

```bash
# 1. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 2. Launch Jupyter
jupyter notebook

# 3. Open and run
Task1_Iris_EDA.ipynb   →   Run All Cells
```

> No dataset download needed — Iris is loaded automatically via seaborn.

---

##  Files

| File | Description |
|:---|:---|
| `Task1_Iris_EDA.ipynb` | Main Jupyter Notebook |
| `README.md` | This file |

---

> 💡 **Note:** This is a purely exploratory task — no ML model is trained. The insights gained here guide feature selection for future classification tasks.
