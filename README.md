# Wine Dataset Clustering (KMeans & Hierarchical Clustering)

## Overview

This project applies unsupervised clustering to a wine dataset to discover natural groupings based on chemical composition. KMeans and Agglomerative (Hierarchical) Clustering with Ward linkage are both applied to five scaled numeric features, and the results are compared using silhouette scores, cluster profiles, and a dendrogram.

---

## Dataset

**Source:** [Wine Dataset — Kaggle](https://www.kaggle.com/datasets/tawfikelmetwally/wine-dataset)

The original dataset contains 178 rows. The version used in this project has been pre-prepared as follows:

- Original class labels removed (unsupervised task)
- Only five numeric features retained for clustering
- No missing values or duplicate rows

**Final shape:** 178 rows × 5 columns

**Features used for clustering:**

| Column | Description |
|---|---|
| `alcohol` | Alcohol content |
| `malic_acid` | Malic acid concentration |
| `flavanoids` | Flavanoid concentration |
| `color_intensity` | Color intensity of the wine |
| `proline` | Proline amino acid concentration |

---

### KMeans Clustering
- KMeans was evaluated for different number of clusters (k = 2, 3, 4, 5, 6) using inertia and silhouette score
- The best k is determined based on the highest silhouette score

| k | Inertia | Silhouette Score |
|---|---|---|
| 2 | 591.0345 | 0.3342 |
| **3** | **358.0601** | **0.4182** |
| 4 | 306.8912 | 0.3755 |
| 5 | 273.9672 | 0.3592 |
| 6 | 242.4674 | 0.3005 |

k = 3 is selected as the best value (highest silhouette score).

- Fit the final model with `KMeans(n_clusters=3, random_state=42, n_init=20)`
- Print cluster sizes and a per-cluster mean profile


### Hierarchical Clustering
- Build a Ward-linkage dendrogram from the scaled data
- Fit `AgglomerativeClustering(n_clusters=3, linkage='ward')`
- Print cluster sizes and a per-cluster mean profile



### Cluster Sizes

| Method | Cluster 0 | Cluster 1 | Cluster 2 |
|---|---|---|---|
| KMeans | 71 | 50 | 57 |
| Hierarchical (Ward) | 49 | 60 | 69 |

### Method Comparison

| Method | n_clusters | Silhouette Score |
|---|---|---|
| KMeans | 3 | 0.4182 |
| Hierarchical (Ward) | 3 | 0.4157 |

KMeans edges out hierarchical clustering by a small margin in silhouette score.

### Cluster Interpretation (Hierarchical)

- **Cluster 0** (49 wines): Highest malic acid (3.39) and color intensity (7.33), very low flavanoids (0.80) and proline (622) — likely a bold, high-acid wine type.
- **Cluster 1** (60 wines): Strong flavanoids (2.98) and by far the highest proline (1113) — a full-bodied, flavanoid-rich group.
- **Cluster 2** (69 wines): Lowest averages across most features — color intensity (3.07), proline (516), malic acid (1.88) — likely a lighter-style wine group.
