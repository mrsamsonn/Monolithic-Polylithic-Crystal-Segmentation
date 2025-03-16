# Monolithic-Polylithic-Crystal-Segmentation

| Documentation Report | Currently Unpublished |
| ------------- | ------------- |

## Example Output
![animated_plot](https://github.com/user-attachments/assets/b88677aa-dcc2-4830-8c0a-a34aa9fa2030)
<img width="240" alt="Screenshot 2024-08-16 at 12 49 22 PM" src="https://github.com/user-attachments/assets/687860e8-5789-4e8c-9a49-b7fea5fbd1a8">
<img width="366" alt="Screenshot 2024-08-16 at 12 49 31 PM" src="https://github.com/user-attachments/assets/4e69d6d6-e2f6-4011-ba62-a9b21d8cfb16">


# Grid Segmentation Overview 🧩

## 1. Introduction

	•	Purpose:
	•	Partition real space into grids to analyze and cluster crystal structures using diffraction patterns.
	•	Applications:
	•	Used for segmenting monolithic and polylithic crystals.
	•	Supports k-means clustering, similarity calculations, and visualization.

## 2. Setup

	•	Grid Partitioning:
	•	Divide real space into square grids.
	•	Map each grid to a region in diffraction space.
	•	Data Structures:
	•	Grids: Represents the grid layout.
	•	Features Array: Stores features like peak intensities.
	•	Similarity Matrix: Holds similarity scores for clustering.

## 3. Diffraction Pattern Analysis

	•	Collect Data:
	•	Obtain diffraction patterns for each grid.
	•	Peak Detection:
	•	Locate peaks in a defined region around expected locations.
	•	Calculate peak intensity, adjust for edge effects.

## 4. Similarity Calculation

	•	Feature Extraction:
	•	Extract key features from diffraction data.
	•	Measure Similarity:
	•	Use distance metrics to calculate similarity between grids.
	•	Normalize values for consistency in clustering.

## 5. Clustering

	•	K-Means Clustering:
	•	Apply k-means to group similar grids.
	•	Determine the optimal number of clusters using elbow method.
	•	Edge Cases:
	•	Handle grids near edges or isolated outliers.

## 6. Visualization

	•	Color Mapping:
	•	Use color codes  to distinguish clusters.
	•	Plotting:
	•	2D Plotting: Represent each grid as a colored rectangle.
	•	3D Plotting: Optionally visualize in 3D, excluding grids with zero similarity.
	•	Legend Creation:
	•	Generate a legend to label clusters for clear interpretation.

## 7. Practical Considerations

	•	Efficiency:
	•	Optimize for large datasets, possibly using parallel processing.
	•	Parameter Tuning:
	•	Experiment with grid sizes and clustering parameters to refine results.
	•	Extensions:
	•	Dynamic Grid Sizes: Implement adaptive grid sizing.
	•	Integration: Combine with other segmentation methods for better accuracy.

## 8. Conclusion

	•	Summary:
	•	Grid segmentation is key for detailed analysis and clustering of crystal structures.
	•	Future Work:
	•	Focus on refining techniques for better performance and new applications.
