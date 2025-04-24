# Monolithic-Polylithic Crystal Segmentation

This project provides a grid-based segmentation approach to identify monolithic and polylithic crystal structures from diffraction patterns. The method partitions diffraction data into grids, detects peaks in each tile, extracts features, and applies k-means clustering for grouping similar diffraction patterns.

## Clustered Output Examples
 ![animated_plot](https://github.com/user-attachments/assets/b88677aa-dcc2-4830-8c0a-a34aa9fa2030)
 <img width="240" alt="Screenshot 2024-08-16 at 12 49 22 PM" src="https://github.com/user-attachments/assets/687860e8-5789-4e8c-9a49-b7fea5fbd1a8">
 <img width="366" alt="Screenshot 2024-08-16 at 12 49 31 PM" src="https://github.com/user-attachments/assets/4e69d6d6-e2f6-4011-ba62-a9b21d8cfb16">

## Table of Contents
- [Output Example](#output-example)
- [Overview](#overview)
- [Algorithm Explanation](#algorithm-explanation)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Output](#output)
- [Project Structure](#project-structure)
- [Future Work](#future-work)
- [License](#license)

## Overview

This project segments diffraction patterns into square grids, each analyzed for peak detection. The algorithm then clusters the grids using k-means and visualizes the segmented diffraction patterns to identify monolithic vs. polylithic structures.

## Algorithm Explanation

The segmentation algorithm follows a structured approach:

### 1. **Grid Partitioning**
First, the diffraction pattern is divided into square grids. Each grid cell is treated as a separate region for analysis.

```python
import numpy as np

def create_grid(data, grid_size):
    """
    Divides the diffraction data into square grids based on the given grid size.
    """
    rows, cols = data.shape
    grid_rows = rows // grid_size
    grid_cols = cols // grid_size
    grids = []

    for i in range(grid_rows):
        for j in range(grid_cols):
            grid = data[i*grid_size:(i+1)*grid_size, j*grid_size:(j+1)*grid_size]
            grids.append(grid)
    
    return grids

```

2. Peak Detection

For each grid, local maxima are identified using a peak detection algorithm. The scipy.signal.find_peaks function is often employed for this purpose.

from scipy.signal import find_peaks

```python
def detect_peaks(grid):
    """
    Detects peaks in the grid data using scipy's find_peaks function.
    """
    peaks, _ = find_peaks(grid)
    return peaks
```

3. Feature Extraction

For each grid, features such as peak intensity and spatial distribution are extracted into a feature vector. These features are essential for clustering.

```python
def extract_features(grid, peaks):
    """
    Extracts features from the grid based on the detected peaks.
    """
    features = []
    for peak in peaks:
        intensity = grid[peak]  # Peak intensity
        position = peak  # Peak position (x, y)
        features.append([intensity, position])
    
    return np.array(features)
```

4. Clustering

The features are clustered using k-means. The optimal number of clusters is determined using the elbow method.

```python
from sklearn.cluster import KMeans

def cluster_features(features, n_clusters=3):
    """
    Clusters the feature vectors using k-means clustering.
    """
    kmeans = KMeans(n_clusters=n_clusters)
    clusters = kmeans.fit_predict(features)
    return clusters
```

5. Visualization

Finally, the clusters are visualized using matplotlib. Each grid cell is colored based on the cluster it belongs to.

```python
import matplotlib.pyplot as plt

def plot_clusters(clusters, grid_size, data_shape):
    """
    Visualizes the clustered data with color coding.
    """
    rows, cols = data_shape
    grid_rows = rows // grid_size
    grid_cols = cols // grid_size

    # Create an empty image for the cluster visualization
    cluster_image = np.zeros((rows, cols))

    idx = 0
    for i in range(grid_rows):
        for j in range(grid_cols):
            cluster_image[i*grid_size:(i+1)*grid_size, j*grid_size:(j+1)*grid_size] = clusters[idx]
            idx += 1

    plt.imshow(cluster_image, cmap='viridis')
    plt.title('Cluster Visualization')
    plt.colorbar()
    plt.show()
```

Setup Instructions

Prerequisites
	•	Python 3.x
	•	Jupyter Notebook

Install Dependencies

```
pip install numpy matplotlib scikit-learn tifffile
```

Clone and Run

```
git clone https://github.com/mrsamsonn/Monolithic-Polylithic-Crystal-Segmentation.git
cd Monolithic-Polylithic-Crystal-Segmentation
jupyter notebook Grid_Segmentation.ipynb
```

Usage
	1.	Open Grid_Segmentation.ipynb in Jupyter Notebook.
	2.	Follow the instructions to load diffraction data, define grid parameters, and run the segmentation algorithm.

Output

The segmentation process outputs:
	•	Animated GIFs showing the clustering process.
	•	Static images with color-coded clusters.
	•	Legends and clustering metrics.

Project Structure

```
Monolithic-Polylithic-Crystal-Segmentation/
│
├── Grid_Segmentation.ipynb   # Main analysis notebook
├── animated_plot.gif         # Example output GIF
├── *.png                     # Sample output images
├── README.md                 # Project documentation
└── data/                     # Input diffraction files (user-provided)
```

Future Work
	•	Dynamic Grid Resizing: Implement adaptive grid resizing based on the size of detected structures.
	•	Advanced Clustering: Incorporate DBSCAN or spectral clustering for better handling of noisy diffraction data.
	•	Real-Time Analysis: Support live data processing for real-time diffraction pattern segmentation.
