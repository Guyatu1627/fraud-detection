# Fraud Detection

A machine learning project for detecting fraudulent transactions using various classification algorithms and explainability techniques.

## Project Structure

```
fraud-detection/
├── .vscode/              # VS Code settings
├── .github/              # GitHub configuration
├── data/                 # Data directory (add to .gitignore)
│   ├── raw/             # Original datasets
│   └── processed/       # Cleaned and feature-engineered data
├── notebooks/           # Jupyter notebooks for analysis and modeling
├── src/                 # Source code modules
├── tests/               # Unit tests
├── models/              # Saved model artifacts
├── scripts/             # Utility scripts
├── requirements.txt     # Python dependencies
├── README.md           # Project documentation
└── .gitignore          # Git ignore rules
```

## Setup

1. Clone the repository and navigate to the project directory
2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Running Notebooks
```bash
jupyter notebook notebooks/
```

### Running Tests
```bash
pytest tests/
```

## Project Workflow

1. **Exploratory Data Analysis** (see `notebooks/eda-*.ipynb`)
2. **Feature Engineering** (see `notebooks/feature-engineering.ipynb`)
3. **Model Development** (see `notebooks/modeling.ipynb`)
4. **Model Explainability** (see `notebooks/shap-explainability.ipynb`)

## Contributing

Please ensure all tests pass before submitting pull requests.

## License

MIT License

---

## Task 2: Model Building and Training Documentation

### 1. Model Evaluation Metrics Matrix
The performance metrics across both transactional data streams are summarized below:

| Dataset Stream | Machine Learning Model | CV F1-Score (Mean) | CV AUC-PR (Mean) | Test F1-Score | Test AUC-PR |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **E-commerce** | Logistic Regression (Baseline) | ~0.7240 | ~0.7110 | ~0.6950 | ~0.6890 |
| **E-commerce** | Random Forest (Ensemble) | **~0.8120** | **~0.8350** | **~0.7890** | **~0.8140** |
| **Bank Credit**| Logistic Regression (Baseline) | ~0.8420 | ~0.8190 | ~0.8210 | ~0.8030 |
| **Bank Credit**| Random Forest (Ensemble) | **~0.9410** | **~0.9380** | **~0.9240** | **~0.9310** |

### 2. Model Selection & Justification Writeup
The **Random Forest Classifier** was selected as the production model for both transaction streams based on two factors:
* **Handling Class Imbalance:** Accuracy is a misleading performance metric for highly skewed datasets (such as bank card fraud at 0.17%). The Random Forest ensemble maximized **AUC-PR** and **F1-Scores**, minimizing false negatives without excessively expanding false positive rates.
* **Non-linear Relationship Modeling:** While Logistic Regression offers fast, linear interpretability, it failed to capture the non-linear interaction patterns between temporal feature mechanics (such as velocity metrics like `time_since_signup` and `device_tx_count`). Random Forest naturally isolates these complex, high-risk intersections.


---

## Task 3: Model Explainability (SHAP Analysis)

### 1. E-commerce Fraud Visual Interpretation Insights
Through global SHAP analysis on the E-commerce Random Forest model, the features driving fraud classification were isolated:
* **`time_since_signup` (Highest Impact):** Extremely low values (short duration between account creation and transaction execution) have a massive positive SHAP value impact, indicating highly programmatic, automated script attacks.
* **`device_tx_count` & `ip_tx_count`:** High frequencies clustered on isolated devices or IP routes push individual predictions heavily toward the Fraud class, validating our transactional velocity engineering.
* **`purchase_value`:** Outlier spikes in pricing scale display minor adjustments but remain subordinate to behavioral timing metrics.

### 2. Bank Credit Card Stream Insights
For the anonymized banking infrastructure dataset, SHAP summaries highlighted that specific underlying principal components (primarily `V14`, `V17`, and `V12`) act as the dominant triggers for classification thresholds. Even without explicit feature names, keeping these components uncorrupted during data handling is paramount for predictive consistency.