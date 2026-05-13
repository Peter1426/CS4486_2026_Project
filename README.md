# CS4486 - YouTube Spam Comment Classification

## Overview

This is an individual project for **CS4486 Artificial Intelligence** at City University of Hong Kong. The project builds a machine learning classifier to automatically detect spam comments on YouTube.

Four classification algorithms are implemented and compared using Scikit-learn:

| Algorithm | Test Accuracy | Training Time |
|-----------|---------------|----------------|
| Logistic Regression | 84.65% | 0.03s |
| Naive Bayes | 82.67% | 0.00s |
| Random Forest (default) | 85.64% | 0.22s |
| **Random Forest (optimized)** | **86.63%** | - |

## Key Findings

- **Best Model:** Optimized Random Forest achieved **86.63%** test accuracy
- **Overfitting Reduced:** Training-test accuracy gap decreased from 12% to 2.5% after hyperparameter tuning
- **Top Spam Indicators:** 'check', 'subscribe', 'channel', 'views', 'money'
- **Speed Alternative:** Logistic Regression trains in 0.03s with 84.65% accuracy, suitable for real-time applications

## Quick Start

### Prerequisites
- Python 3.8+
- 4GB RAM recommended

### Installation

```bash
# Clone the repository
git clone https://github.com/Peter1426/CS4486_2026_Project.git
cd CS4486_2026_Project

# Install dependencies
pip install -r requirements.txt
```

### Run the Notebook

Make sure the data files are in the data folder:

- `Topic1-youtube_spam_train.csv` (training data, 798 samples)
- `Topic1-youtube_spam_test.xlsx` (test data, 202 samples)

Then run the Jupyter notebook:

```bash
jupyter notebook src/YouTube_Spam_Classifier.ipynb
```

## Results

### Model Comparison

| Model | CV Accuracy | Train Accuracy | Test Accuracy | F1-Score | Time (s) |
|-------|-------------|----------------|---------------|----------|----------|
| Logistic Regression | 79.20% | 95.36% | 84.65% | 0.842 | 0.03 |
| Naive Bayes | 82.84% | 95.49% | 82.67% | 0.821 | 0.00 |
| Random Forest (default) | 81.08% | 97.62% | 85.64% | 0.853 | 0.22 |
| MLP | 83.09% | 97.62% | 84.16% | 0.839 | 3.86 |
| **Random Forest (optimized)** | 80.94% | 84.09% | **86.63%** | **0.866** | - |

### Hyperparameter Tuning Results (Random Forest)

| Parameter | Default | Best Found |
|-----------|---------|-------------|
| n_estimators | 100 | 50 |
| max_depth | None | 15 |
| min_samples_split | 2 | 20 |
| min_samples_leaf | 1 | 4 |
| max_features | sqrt | None |

**Improvement:** +0.99% test accuracy, overfitting reduced from 12% to 2.5%

### Top 10 Most Important Words for Spam Detection

| Rank | Word | Importance |
|------|------|------------|
| 1 | check | 20.31% |
| 2 | subscribe | 18.54% |
| 3 | channel | 7.99% |
| 4 | views | 6.31% |
| 5 | money | 6.10% |
| 6 | help | 5.14% |
| 7 | song | 3.98% |
| 8 | free | 3.73% |
| 9 | video | 3.72% |
| 10 | love | 2.49% |

### Confusion Matrix (Optimized Random Forest)

```
                Predicted Ham    Predicted Spam
Actual Ham          87                5
Actual Spam         22               88
```

- **Ham Recall:** 94.6% (87/92)
- **Spam Recall:** 80.0% (88/110)
- **Overall Accuracy:** 86.63% (175/202)

## Project Structure

```
CS4486_2026_Project/
├── README.md                              # Project documentation
├── requirements.txt                       # Python dependencies
├── CS4486_Project.pdf                     # Project report
│
├── src/
│   └── YouTube_Spam_Classifier.ipynb     # Jupyter notebook
│
├── data/
│   ├── Topic1-youtube_spam_train.csv     # Training data (798 samples)
│   └── Topic1-youtube_spam_test.xlsx     # Test data (202 samples)
│
└── output/
    ├── predictions.csv                   # Test set predictions
    └── model_comparison.png              # Model comparison chart
```

### Data Structure

Each file contains:
- **VIDEO:** YouTube video ID
- **AUTHOR:** Comment author name
- **DATE:** Comment timestamp
- **TEXT:** Comment content
- **CLASS:** Label (0 = not spam, 1 = spam)

| Dataset | Size | Format |
|---------|------|--------|
| Training | 798 samples | CSV (UTF-8) |
| Test | 202 samples | Excel (.xlsx) |

## Parameter Impact (Random Forest)

| Parameter | Values Tested | Best Value |
|-----------|---------------|------------|
| n_estimators | 50, 100, 150, 200, 300 | 50 |
| max_depth | 5, 10, 15, 20, 25, 30, None | 15 |
| min_samples_split | 2, 5, 10, 15, 20 | 20 |
| min_samples_leaf | 1, 2, 3, 4, 5 | 4 |
| max_features | 'sqrt', 'log2', None | None |

**Key Findings:**
- Smaller `n_estimators` (50) performed better than larger values
- Restricting `min_samples_split` to 20 helped reduce overfitting
- Using all features (`max_features=None`) worked best for this dataset

## Technologies Used

| Category | Technologies |
|----------|--------------|
| **Language** | Python 3.8+ |
| **Core Libraries** | Scikit-learn, Pandas, NumPy |
| **Visualization** | Matplotlib |
| **Development** | Jupyter Notebook |


## Notes on Reproducibility

All random operations are fixed with `random_state=42` to ensure reproducibility. The results shown above were obtained by running the notebook on a standard CPU. Minor variations in training time may occur depending on system load, but all accuracy and F1-score results remain consistent.
