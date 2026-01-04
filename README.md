# Student Performance Analysis — Multi-Source Educational Study
An end-to-end data science project investigating the determinants of student success. This study evolves from local exploratory analysis to global structural context by integrating external OECD API data to account for institutional variables like class size.

Repository: https://github.com/Latherine/student-performance-analysis

---

## Contents (Project Structure)
- `.gitignore` — (Excludes __pycache__, .ipynb_checkpoints, and local CSVs)

- `data/`

  - `StudentPerformanceFactors.csv` — Primary dataset (6,000+ student records).

  - `oecd_class_size_by_school_type_api.csv` — External data retrieved via the OECD API.

- `results/`

  - `api_summary.pdf` — Formatted final research paper.

  - `api_summary.html` — Interactive export of the final analysis.

- `notebooks/`

  - `01_exploratory_analysis.ipynb` — Phase 1: Initial EDA, Tidy Data cleaning, and hypothesis generation.

  - `02_api_integration_analysis.ipynb`— Phase 2: API integration, data merging, and structural comparison.

---

## Quick Setup
1. Clone the repository
   ```bash
   git clone https://github.com/Latherine/student-performance-analysis.git
   cd student-performance-analysis
   ```
2. Create & activate virtual environment
   ```bash
   python -m venv .venv
   source .venv/bin/activate    # macOS / Linux
   .venv\Scripts\activate       # Windows
   ```
3. Install required packages
   ```bash
   pip install pandas numpy matplotlib seaborn requests
   ```

---

## Research Narrative
#### Phase 1: Exploratory Analysis 
Initially, I analyzed the correlation between study habits and exam scores. While the data identified key drivers, the "School Type" variable showed significant score overlap between Public and Private institutions. This led to a hypothesis that secondary structural factors—like class size—were missing from the local dataset.

#### Phase 2: API Integration 
To resolve this, I engineered a web scraper/API function to fetch instructional data from the OECD database. By integrating real-world average class sizes, I was able to contextualize why public school performance might show higher variability compared to private institutions.

---

## Data Integration Logic
The analysis utilizes a two-pronged data approach:

1. Primary Dataset (`StudentPerformanceFactors.csv`):

  - Attributes: `Hours_Studied`, `Parental_Involvement`, `School_Type`, `Exam_Score`.
  - Used for individual-level correlation analysis.

2. External API (`OECD API`):

  - Attribute: `Average Class Size` by institution type.
  - Used to provide structural benchmarks.

__Key Insight__: The API data confirms public schools manage larger class sizes (~21.87) compared to private schools (~20.07). Despite this structural hurdle, the performance overlap suggests that student-level factors like motivation and study time effectively mitigate the challenges of larger classroom environments.

---

## How to Run
- Place the required CSVs in the data/ folder.
- Run the executable notebooks from the /notebooks directory.
- Note on Paths: The code uses relative pathing to ensure portability:
  ```bash
  import os
  data_path = os.path.join('..', 'data', 'StudentPerformanceFactors.csv')
  df = pd.read_csv(data_path)
  ```

---

## Expected Outputs
The notebooks generate three core visual suites:

  - Categorical Distributions: Boxplots showing the overlap of scores between institution types.
  - API Comparative Tables: Summary statistics of OECD class size data.
  - Correlation Heatmaps: Identifying the strongest predictors of Exam_Score across all variables.

---

## Contact
Maintainer: Latherine Vo

Repo: https://github.com/Latherine/student-performance-analysis
