# Decision Trees and Nearest Neighbors



---

## Overview

This notebook implements and evaluates decision tree and K-nearest neighbors classifiers on two datasets: the UCI forest fires dataset and the Titanic survival dataset. It covers data preprocessing, model training, evaluation metrics, handling class imbalance, and feature importance analysis.

---

## Contents

- **Decision tree classifier** trained on the forest fires dataset, including a balanced variant to address class imbalance.
- **K-nearest neighbors classifier**, with circular encoding of month and day features (split into real and imaginary components since KNN cannot operate on complex numbers directly).
- **Evaluation metrics** including accuracy and F1 score, with discussion of how class imbalance affects each.
- **Titanic decision tree (extra credit)** with feature importance analysis and a visualized decision tree.

---

## Documented Fixes

This notebook was inherited in a broken state. The following issues were identified and fixed:

1. **KNN imports** — removed `from sklearn.externals.six import StringIO`, `pydotplus`, `export_graphviz`, `mpimg`, and `mpatches`. The `sklearn.externals.six` module no longer exists in modern scikit-learn, and none of these imports were actually used by the KNN code.
2. **Bar plot** — the seaborn barplot for class distribution was commented out and broken. Rewrote it so the plot renders correctly.
3. **KNN data and target** — the original code trained KNN on `df`, silently discarding the circular month/day encoding done in `knn_df`. Fixed to use `knn_df`, splitting the complex-valued `months_comp` and `days_comp` columns into real and imaginary parts.
4. **Model verification** — reran every section after each fix to confirm the decision tree, KNN, balanced decision tree, evaluation metrics, and extra credit all execute without errors.
5. **Notebook completion** — reviewed outputs for consistency and completed the required written discussion cells based on the generated results.

---

## Key Findings

- On the forest fires dataset, class imbalance causes a noticeable gap between accuracy and F1 score, since the model can score well on accuracy while performing poorly on the minority class.
- On the Titanic dataset, **Sex** is the most important feature (importance ≈ 0.61), consistent with the "women and children first" evacuation pattern. Passenger class and age contribute less. The Titanic model's F1 score is much closer to its accuracy than the forest fires model, indicating a more balanced dataset.

---
