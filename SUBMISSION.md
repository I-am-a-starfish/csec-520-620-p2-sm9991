# Submission Manifest — Project 2

Fill this in before submitting. The grading agent reads it first.

## Student
- Name (RIT ID): Shefali Maurya

## Course level
- [this] 520 (undergraduate)
- [ ] 620 (graduate)

## Dataset
- Name / source / version / URL: UNSW_NB15_training-set.csv
- How to obtain it (command or steps):run make data
- Label column (used for EVALUATION ONLY): 
- Subsample size and how you chose it: just played around with the numbers

## How to reproduce
```bash
make setup
# Download the course Drive archive and extract data/UNSW_NB15_training-set.csv
# See data/README.md; make data is an optional mirror fallback / checksum check.
make reproduce
```
Anything non-default the grader must know (data download, runtime):

## Your implementation
- Confirm `config.yaml` has `kmeans.implementation: scratch`: [yes]
- Initialization used (`random` / `kmeans++`): tried both
- How you handle **empty clusters**: Just leave the centroid where it is
- Convergence criterion and tolerance: There are 2 convergence checks -> First, stopping when cluster assignments stop changing np.array_equal(new_labels,labels) that indicated the algorithm has reached a fixed point. Second, stopping when centroids move less than the tolerance that is specified meanaing hat furthur iterations wont significantly change the solution
- 
- Agreement with the reference (each run’s `reference_check` in metrics.json; same geometry):
  - Euclidean `inertia_ratio` / `ari_vs_reference`: 0.9993578625586387
  - Mahalanobis `inertia_ratio` / `ari_vs_reference`: 1

## Choosing k
- k you report, and the evidence (elbow / silhouette): both have k=3
- If the best silhouette k differs from the number of true classes, explain:

## Claimed results (must match `results/metrics.json`)
| Metric | Euclidean | Mahalanobis |
|---|---|---|
| Silhouette (common Euclidean) | 0.36664036985460785 | 0.3559184962714477 |
| Silhouette (configured geometry) | 0.36664036985460785 | 0.35286354022415733 |
| V-measure | 0.21793918104859775 | 0.21942165050726717 |
| Accuracy | 0.21206434316353887 | 0.2099195710455764 |
| Macro F1 | 0.1259619108618522 | 0.12142704734365761 |

- Primary comparison criterion declared before weight experiments:
- The diagonal C you chose, its feature order, and why: [1.0, 2.0, 2.0, 2.0, 2.0, 2.0, 1.0, 1.0, 2.0, 2.0, 1.0, 1.0, 2.0, 2.0, 2.0, 2.0, 1.0, 1.0, 1.0, 1.0, 2.0, 2.0, 2.0, 1.0, 1.0, 0.5, 0.5, 2.0, 2.0, 2.0, 1.0, 1.0, 1.0, 0.5, 1.0, 1.0, 1.0, 1.0, 0.5] weights were chosen to up‑weight high‑variance or high‑signal features (2.0 entries) and down‑weight noisy or low‑variance features (0.5 entries)
- Same sample, k, seed and restart budget across the primary runs: [10,030 standardized rows, k=6, seed=82, random initialization, 10 restarts, max_iter and tolerance: 300 iterations, tol = 1e‑6]
- Tradeoffs and whether any independent validation was used: Euclidean treats all features equally while Mahanlanobis reshapes features by emphasizing selected dimentions

## AI-use acknowledgment
Per the syllabus policy, briefly note any substantive use of AI assistants.
