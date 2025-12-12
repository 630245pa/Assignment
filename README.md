# Assignment
### Key Objectives

- **Efficiency**: Reduce computational complexity from O(n²) to O(n) using LSH
- **Accuracy**: Achieve high Pair Quality (PQ) and Pair Completeness (PC) scores
- **Robustness**: Use bootstrap evaluation for reliable performance estimation
- **Comparison**: Evaluate multiple methods (LSH+Clustering, LSH+Logistic Regression, Clustering without LSH)

## Features

### Core Components

- **MinHashing**: Creates compact signature matrices from binary product vectors (40% of vocabulary size)
- **LSH Banding**: Divides signature matrix into bands with optimized threshold to find candidate pairs
- **Model Word Extraction**: 
  - Full method: Extracts model words from title, brand names, and "1080"
  - Title-only method: Extracts model words only from titles (for comparison)
- **TMWM Similarity**: Title Model Words Method similarity metric for clustering
- **Agglomerative Clustering**: Hierarchical clustering with complete linkage and optimized distance threshold
- **Logistic Regression**: Classification-based alternative method for duplicate detection
- **Bootstrap Evaluation**: 5-fold bootstrap resampling for robust performance estimation
- **Hyperparameter Optimization**: F1-based optimization of LSH parameters and clustering thresholds on training data
- **Filtering**: Removes candidate pairs with different brands or from the same shop

### Evaluation Metrics

- **Pair Quality (PQ)**: Precision - fraction of predicted pairs that are true duplicates
- **Pair Completeness (PC)**: Recall - fraction of true duplicates found
- **F1-Score**: Harmonic mean of PQ and PC
- **Fraction of Comparisons**: Efficiency metric showing reduction in search space

