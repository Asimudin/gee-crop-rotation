# 🔄 Multi-Season Crop Rotation Analysis using Sentinel-2 & GEE

This project performs **multi-year crop rotation analysis** using Sentinel-2 imagery, supervised classification, and unsupervised clustering in **Google Earth Engine (GEE)**. It is designed to classify crops over multiple years and group regions by **dominant rotation patterns** (e.g., Corn → Soybeans → Other) using **K-Means clustering**.

---

## 📌 Objective

- Classify land use for each year using Random Forest.
- Stack annual classifications to represent temporal crop sequences.
- Use unsupervised K-Means clustering to discover recurring crop rotation patterns.
- Export samples to interpret clusters into human-readable labels.
- Visualize crop rotations using a custom legend and color palette.

---

## 🌍 Region of Interest

| Parameter        | Value                               |
|------------------|--------------------------------------|
| Location         | Central Iowa, USA                   |
| AOI Size         | Reduced (~25 km²) to avoid GEE memory limits |
| Years Analyzed   | 2020, 2021, 2022                     |
| Data Source      | Sentinel-2 SR Harmonized Collection |

---

## 🛠️ Methodology Overview

### 🔹 1. Project Configuration
- Define a smaller AOI to resolve the "Computed value is too large" error.
- Select relevant bands (B2–B8) and crop classes: **Corn**, **Soybeans**, and **Other**.

### 🔹 2. Supervised Classification
- Use **ground truth polygons** to train a Random Forest classifier on the base year (2021).
- Classify each year individually using the trained model.

### 🔹 3. Rotation Stack
- Stack annual classified maps using `toBands()` to create a 3-year crop sequence image.

### 🔹 4. Unsupervised Clustering
- Sample thousands of pixels and apply **K-Means clustering** (5 clusters) to group similar crop rotation patterns.

### 🔹 5. Interpretation
- Export cluster + classification samples to Google Drive as a CSV.
- Analyze the CSV in Python to label each cluster (e.g., `Cluster 0: Corn → Soybeans → Other`).

### 🔹 6. Visualization
- Display the rotation map with custom color palette and readable cluster labels using `geemap`.

---

## 🧪 Crop Class Definitions

| Class     | Value | Color     |
|-----------|--------|-----------|
| Corn      | 0      | `#FFD700` |
| Soybeans  | 1      | `#228B22` |
| Other     | 2      | `#A9A9A9` |

---

## 🎨 Cluster Visualization

| Cluster | Example Rotation          | Color     |
|---------|---------------------------|-----------|
| 0       | Corn → Soybeans → Other   | `#e41a1c` |
| 1       | Soybeans → Soybeans → Corn| `#377eb8` |
| 2       | Other → Corn → Soybeans   | `#4daf4a` |
| 3       | Corn → Corn → Soybeans    | `#984ea3` |
| 4       | Soybeans → Other → Other  | `#ff7f00` |

*(These are illustrative; your results will vary based on sampled outputs)*

---

## 🚀 Setup Instructions

### 1. Clone the Repo

```bash
git clone https://github.com/YOUR_USERNAME/crop-rotation-analysis.git
cd crop-rotation-analysis
