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
