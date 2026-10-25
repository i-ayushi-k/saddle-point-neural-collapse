# Saddle-Point Curvature and Neural Collapse

## Overview

This project investigates the relationship between local loss-surface curvature, neural-collapse-style feature clustering, and classification performance under class imbalance.

The preliminary experiments compare three training approaches on the UCI Covertype dataset:

- Ordinary Stochastic Gradient Descent (SGD)
- Sharpness-Aware Minimization (SAM)
- Class-Targeted SAM using class-weighted cross-entropy

## Research Question

How do local curvature and neural-collapse-style feature clustering differ between standard SAM and class-targeted SAM when classification performance is evaluated under class imbalance?

## Dataset

**UCI Covertype**

- Samples: 581,012
- Input features: 54
- Target classes: 7
- Task: Multiclass classification

The dataset contains cartographic features used to predict forest cover types.

## Methodology

1. Load the Covertype dataset and create stratified training, validation, and test splits.
2. Standardize input features using training-set statistics.
3. Train an MLP classifier using ordinary SGD.
4. Train the same architecture using standard SAM.
5. Train a class-weighted SAM variant to emphasize errors on less-represented classes.
6. Compare validation accuracy, Macro-F1, Weighted-F1, per-class recall, and G-mean.
7. Estimate local loss curvature using Hessian-vector products.
8. Calculate an NC1-style feature-clustering ratio from penultimate-layer representations.

## Preliminary Results

| Model | Accuracy | Macro-F1 | Weighted-F1 | Curvature magnitude | NC1 |
|---|---:|---:|---:|---:|---:|
| Ordinary SGD | 0.7595 | 0.5559 | 0.7522 | 18.5604 | 1.2822 |
| Standard SAM | 0.7574 | 0.5533 | 0.7485 | 9.2010 | 1.2329 |
| Class-Targeted SAM | 0.6705 | 0.5604 | 0.6921 | 17.4043 | 1.4333 |

These are preliminary validation results from a single experimental run. They should not be interpreted as statistically conclusive findings.

### Initial Observations

- Ordinary SGD achieved the highest overall accuracy and Weighted-F1 in this run.
- Standard SAM produced the lowest estimated curvature magnitude and NC1-style ratio.
- Class-targeted SAM achieved the highest Macro-F1 and improved recall for several less-represented classes, with a reduction in overall accuracy.
- The results motivate further investigation into the relationship between class-wise performance, local curvature, and representation geometry.

## Limitations

- Results are based on a single random seed and a short training run.
- Curvature estimates use a limited number of power iterations on one validation batch.
- The NC1-style ratio is a preliminary representation metric, not proof of complete neural collapse.
- The class-targeted method uses class-weighted cross-entropy and is not a separate class-specific SAM perturbation algorithm.
- Class imbalance experiments and controlled comparisons require further refinement.
- No causal relationship between curvature, neural collapse, and performance has been established.

## Future Work

- Repeat experiments across multiple random seeds.
- Verify all metrics and improve experimental controls.
- Evaluate results on a held-out test set.
- Refine class-imbalance experiments while controlling for training-set size.
- Investigate class-wise curvature and more comprehensive neural-collapse metrics.
- Compare results across additional datasets.
- Add statistical significance and uncertainty analysis.

## Repository Contents

- `saddle-point-neural-collapse.ipynb` — experimental notebook, code, and available outputs.
- `review1_preliminary_results.csv` — consolidated preliminary validation metrics.

## Status

**Research prototype — preliminary experiments completed; further validation and analysis pending.**

## Dataset Source

UCI Machine Learning Repository — Covertype dataset.

https://archive.ics.uci.edu/dataset/31/covertype
