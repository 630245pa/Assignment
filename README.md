# Assignment

In the assignment the scalability issue for duplicate product detection using
data coming from several Web shops is addressed using LSH.
### Key Objectives

- **Efficiency**: Reduce computational complexity using LSH
- **Accuracy**: Achieve high Pair Quality (PQ) and Pair Completeness (PC) scores
- **Robustness**: Use bootstrap evaluation for reliable performance estimation
- **Comparison**: Evaluate multiple methods (LSH+Clustering, Clustering without LSH)

## Features

### Core Components

- **MinHashing**: Creates compact signature matrices from binary product vectors (40% of vocabulary size)
- **LSH Banding**: Divides signature matrix into bands with optimized threshold to find candidate pairs
- **Model Word Extraction**: 
  - Full method: Extracts model words from title, brand names, and "1080"
  - Title-only method: Extracts model words only from titles (for comparison)
- **TMWM Similarity**: Title Model Words Method similarity metric for clustering
- **Agglomerative Clustering**: Hierarchical clustering with complete linkage and optimized distance threshold
- **Bootstrap Evaluation**: 5-fold bootstrap resampling for robust performance estimation
- **Hyperparameter Optimization**: F1-based optimization of LSH parameters and clustering thresholds on training data
- **Filtering**: Removes candidate pairs with different brands or from the same shop

### Evaluation Metrics

- **Pair Quality (PQ)**: Precision - fraction of predicted pairs that are true duplicates
- **Pair Completeness (PC)**: Recall - fraction of true duplicates found
- **F1-Score**: Harmonic mean of PQ and PC
- **Fraction of Comparisons**: Efficiency metric showing reduction in search space


**Open the main notebook**: `experiment_graph.ipynb` or `experiment_diff_extraction.ipynb`

2. **Execute cells in order**:
   - Data loading and preprocessing
   - Helper function definitions
   - Bootstrap evaluation loop
   - Visualization and analysis

3. **Key Notebooks**:
   - `experiment_graph.ipynb`: Main experiment with visualization
   - `experiment_diff_extraction.ipynb`: Comparison of different model word extraction methods
   - `Bootstrap-experiment-Copy1.ipynb`: Complete bootstrap evaluation pipeline
  
### Requirements

```bash
Python 3.7+
```

### Dependencies

```python
numpy
scikit-learn
matplotlib
scipy
pandas (for analysis tables)
```

Install dependencies:

```bash
pip install numpy scikit-learn matplotlib scipy pandas
```

### Data

The project requires a JSON file containing product data. The expected format:

```json
{
  "shop1": [
    {"title": "...", "modelID": "...", "featuresMap": {...}, ...},
    ...
  ],
  "shop2": [...],
  ...
}
```

### Example Workflow


# 1. Load and preprocess data
data = load_json_data('TVs-all-merged.json')
cleaned_data = clean_all_values_dict_advanced(data)

# 2. Run bootstrap evaluation
bootstrap_results = []
for bootstrap_idx in range(5):
    # Split into train/test
    train_indices, test_indices = bootstrap_train_test_split(n_samples)
    # Extract model words
    model_words = extract_model_words(...)
    # Apply LSH
    candidate_pairs = lsh_banding(...)
    # Apply clustering or logistic regression
    results = evaluate_method(...)
    bootstrap_results.append(results)

# 3. Visualize results
plot_results(bootstrap_results)
```


### Key Files

- **`experiment_graph.ipynb`**: Main notebook with complete pipeline and visualizations
- **`for_comparision_graph.ipynb`**: notebook with complete pipeline and visualizations but without setting seed
- **`Bootstrap-experiment-Copy1.ipynb`**: Full bootstrap evaluation with LSH and clustering

## 🔬 Methods

### 1. Locality Sensitive Hashing (LSH)

**Purpose**: Efficiently reduce candidate pair space from O(n²) to O(n)

**Process**:
1. Create binary vectors from model words
2. Compute MinHash signatures (40% of vocabulary size)
3. Divide signatures into bands
4. Hash products into buckets within each band
5. Generate candidate pairs from products in same bucket

**Optimization**: Threshold `t` is optimized on training set to maximize F1 score while maintaining constraint `n = r × b`

### 2. Agglomerative Clustering

**Purpose**: Group similar products into duplicate clusters

**Method**:
- Uses TMWM (Title Model Words Method) similarity
- Complete linkage (maximum distance between clusters)
- Distance threshold optimized on training set
- Prevents overfitting with F1 range constraints (0.1-0.2)

