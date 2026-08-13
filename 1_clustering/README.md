# Clustering

Two clustering algorithms written from scratch and compared on the same data, with the
quality metric implemented by hand as well.

## Data

The chemical composition of ancient Chinese ceramics, 88 samples described by the oxide
content of the body or the glaze. The name of the piece and the part it comes from are
dropped, leaving only the numeric composition, since the question is whether the chemistry
alone separates the samples into groups.

## Method

`kmeanspp.py` implements k-means with the k-means++ initialisation, which spreads the
starting centroids apart instead of placing them at random and so avoids the degenerate
splits a bad start produces. `dbscan.py` implements density clustering, which needs no
number of clusters in advance but two other parameters, the neighbourhood radius and the
minimum number of points that makes a neighbourhood dense, and which is free to call a point
noise rather than force it into a cluster.

`metrics.py` implements the silhouette score, which compares how close a point sits to its
own cluster against the nearest other one, so the two algorithms can be judged on the same
scale.

## Results

k-means++ scores best at two clusters and falls away as more are demanded.

| Clusters | Silhouette |
|---------:|-----------:|
| 2 | 0.542 |
| 3 | 0.513 |
| 4 | 0.413 |
| 5 | 0.402 |

DBSCAN scores higher, but the comparison is not free. Its silhouette is computed over the
points it kept, and at its best settings it discards a large share of the sample as noise.

| Clusters | Silhouette | eps | Noise |
|---------:|-----------:|----:|------:|
| 2 | 0.648 | 190 | 47% |
| 3 | 0.653 | 210 | 40% |
| 4 | 0.584 | 230 | 31% |

Both agree that the natural split is two or three groups, which matches the data being body
and glaze samples of a few production sites. DBSCAN buys its tighter clusters by refusing to
classify a third to a half of the points, and whether that is a better answer depends on
whether the outliers are noise or the very thing being looked for.
