# Mathematical Analysis of VAE Latent Space (MNIST)

- Latent dimensionality: **2**
- Training epochs: **15**, final loss/sample: **144.73** (reconstruction 138.45, KL 6.28)
- Overall clustering quality (silhouette score, range [-1, 1]): **0.034**

## 1. Per-class Gaussian fit

| digit | n | mean log-likelihood | min KS p-value across dims |
|---|---|---|---|
| 0 | 980 | -2.34 | 0.000 |
| 1 | 1135 | -2.17 | 0.012 |
| 2 | 1032 | -1.05 | 0.000 |
| 3 | 1010 | -1.03 | 0.000 |
| 4 | 982 | -1.79 | 0.000 |
| 5 | 892 | -2.19 | 0.000 |
| 6 | 958 | -1.82 | 0.000 |
| 7 | 1028 | -0.95 | 0.005 |
| 8 | 974 | -1.05 | 0.000 |
| 9 | 1009 | -1.58 | 0.000 |

## 2. Inter-class separation

Two complementary distance measures were computed between every pair of class-conditional Gaussians:

- **Euclidean distance** between class means — a simple geometric measure of how far apart class centroids sit in latent space.
- Average pairwise Euclidean distance between class means: **1.60**
- Average pairwise Bhattacharyya distance: **1.79**
- Most separated pair (highest Bhattacharyya distance): digits **0** and **1** (D_B = 6.34)
- Most overlapping pair (lowest Bhattacharyya distance): digits **4** and **9** (D_B = 0.03)

See `latent_scatter.png` for the visual clustering, `distance_euclidean.png` / `distance_bhattacharyya.png` for the full pairwise matrices, and `latent_interpolation.png` for a decoded traversal between the most-overlapping pair of classes.

## 3. Interpretation

## 4. Files produced

- `training_curve.png` — reconstruction/KL/total loss vs. epoch
- `latent_scatter.png` — 2D (or reduced) latent space colored by digit, with fitted-Gaussian ~2-std contours
- `distance_euclidean.png`, `distance_bhattacharyya.png` — pairwise class distance heatmaps
- `latent_manifold.png` — decoded images across a 2D latent grid (only produced when latent_dim = 2)
- `latent_interpolation.png` — decoded linear interpolation between two digit classes' mean latent vectors
- `latent_stats.json` — raw numeric results (means, covariances, distances, silhouette score)