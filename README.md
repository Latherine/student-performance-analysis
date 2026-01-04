# student-performance-analysis

Analyzing the impact of school types and OECD class sizes on student exam scores using Python and external API integration.

This repository contains a reproducible analysis and modeling workflow (primarily Jupyter notebooks and HTML output) that examines how school type and OECD-reported class sizes influence student exam performance. It includes data preparation, exploratory data analysis, statistical modeling, simple ML baselines, and examples of integrating external APIs for supplemental indicators.

---

## Table of contents
- [Project overview](#project-overview)
- [Repository composition](#repository-composition)
- [Dataset](#dataset)
- [External API integration](#external-api-integration)
- [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Install](#install)
- [Notebooks & outputs](#notebooks--outputs)
- [Reproducible analysis & scripts](#reproducible-analysis--scripts)
- [Modeling approach & evaluation](#modeling-approach--evaluation)
- [Results and deliverables](#results-and-deliverables)
- [How to cite / credit](#how-to-cite--credit)
- [Contributing](#contributing)
- [License & contact](#license--contact)

---

## Project overview
This project aims to quantify and visualize how school characteristics—especially school type (e.g., public/private) and OECD-class-size indicators—are associated with student exam scores. Use cases include:
- Descriptive comparisons across school types and countries/regions
- Regression and classification models predicting scores or pass/fail outcomes
- Sensitivity checks and simple causal-style contrasts (adjusting for covariates)
- Enriching local datasets with external indicators via APIs (e.g., OECD or other education data sources)

---

## Repository composition
This repo is implemented primarily as interactive notebooks and generated HTML outputs:
- Jupyter Notebook: ~51.5%
- HTML: ~48.5%

Expect the following high-level items:
- notebooks/: reproducible analysis and narrative (exploration → modeling → results)
- data/: raw and processed data (keep large files out of Git)
- scripts/: lightweight CLI helpers (data prep, model training, evaluation)
- outputs/: figures, reports, exported HTML
- src/ (optional): utility functions and modules used by notebooks/scripts

---

## Dataset
There are two data sources typically used in the analysis:
1. Local student-level dataset (CSV) with columns such as:
   - identifiers: `student_id` (optional)
   - demographics: `gender`, `age`
   - academic: `exam_score`, `G1`, `G2`, `G3`, or similar
   - school-level: `school_type` (public/private/other), `school_id`
   - other covariates: `absences`, `parent_education`, `study_time`
2. External indicators (optional) pulled from public APIs (OECD, World Bank, or other education statistics) to obtain country/region/class-size metrics.

Place local datasets under:
- data/raw/ (original files)
- data/processed/ (cleaned/merged files used by notebooks)

If you use a public dataset (e.g., UCI Student Performance), rename it to `data/raw/students.csv` or update notebook paths.

---

## External API integration
This project includes examples of enriching your dataset with external education indicators (OECD class sizes, country-level education spending, etc.). Notebooks/scripts expect API keys/configuration in environment variables.

Example environment variables:
- OECD_API_KEY (if required by the provider)
- OTHER_API_KEY

Usage pattern:
1. Set env vars locally (do NOT commit them).
   - Linux/macOS:
     export OECD_API_KEY="your_key"
   - Windows (PowerShell):
     $env:OECD_API_KEY="your_key"
2. Run the notebook cell or script that fetches external indicators; merged datasets are saved to data/processed/.

See notebooks/api_enrichment.ipynb (or similar) for the exact API endpoints and example calls.

---

## Getting started

### Prerequisites
- Python 3.8+ recommended
- git
- Recommended packages: pandas, numpy, scipy, scikit-learn, statsmodels, matplotlib, seaborn, jupyter, requests

### Install
1. Clone the repo:
   git clone https://github.com/Latherine/student-performance-analysis.git
   cd student-performance-analysis

2. Create and activate a virtual environment:
   python -m venv .venv
   source .venv/bin/activate   # macOS / Linux
   .venv\Scripts\activate      # Windows

3. Install dependencies:
   pip install -r requirements.txt
   (If requirements.txt does not exist yet, install the packages listed above.)

---

## Notebooks & outputs
Open and run the notebooks to reproduce the analysis. Typical notebooks include:
- notebooks/01_data_overview.ipynb — data loading & cleaning
- notebooks/02_exploratory_analysis.ipynb — EDA visualizations and summary tables
- notebooks/03_api_enrichment.ipynb — example API enrichment (OECD/class-size retrieval)
- notebooks/04_modeling_and_evaluation.ipynb — regressions and ML baselines
- notebooks/05_results_and_html_export.ipynb — final plots and HTML export

Start Jupyter:
jupyter lab
or
jupyter notebook

To reproduce published HTML outputs, open files in outputs/html/ or the HTML versions in notebooks' exported form.

---

## Reproducible analysis & scripts
For automated or command-line runs, the repository may contain scripts like:
- scripts/prepare_data.py --input data/raw/students.csv --output data/processed/students_processed.csv
- scripts/enrich_with_api.py --config conf/api_config.yml
- scripts/train_model.py --data data/processed/students_processed.csv --out outputs/models/model.joblib

Each script should provide a `--help` flag explaining required args. Use a fixed random seed (e.g., 42) for reproducibility.

---

## Modeling approach & evaluation
Suggested workflow:
1. Baseline descriptive models (group means, t-tests, ANOVA by school type)
2. Multivariable linear regression for continuous exam scores (control for covariates)
3. Classification models for pass/fail outcomes (logistic regression, random forest, simple gradient boosting)
4. Cross-validation and hyperparameter tuning (GridSearchCV or RandomizedSearchCV)
5. Evaluation metrics:
   - Regression: RMSE, MAE, R²
   - Classification: accuracy, precision, recall, F1, AUC
6. Interpretation:
   - Coefficients with confidence intervals (statsmodels)
   - Feature importance (tree-based models)
   - SHAP or partial dependence for deeper interpretation

---

## Results and deliverables
Deliverables to keep in the repository (or generated locally):
- outputs/figures/ — plots used in the report
- outputs/reports/ — JSON/CSV metrics and summary tables
- outputs/models/ — trained model artifacts (joblib/pickle)
- outputs/html/ — exported HTML notebooks and final report pages

When publishing results, avoid committing sensitive or large raw data. Prefer to commit processed sample data or an anonymized excerpt for reproducibility.

---

## How to cite / credit
If you reuse code or results from this repo in a paper or report, please include:
- A short citation to the GitHub repo URL and your name/organization
- A statement describing the data sources (local dataset + API sources like OECD or World Bank) with their original citations

---

## Contributing
Contributions, issues and feature requests are welcome. Typical workflow:
1. Fork the repo
2. Create your feature branch (git checkout -b feature-name)
3. Commit changes (git commit -m "Add feature")
4. Push to your fork and open a pull request

Add tests for functional changes and keep notebooks clear and documented.

---

## License & contact
Add a LICENSE file to the repo. If you haven't chosen a license yet, MIT is a permissive and common option.

Maintainer: Latherine  
Repo: https://github.com/Latherine/student-performance-analysis

