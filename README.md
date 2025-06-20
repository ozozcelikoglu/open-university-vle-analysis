
# Open University VLE Analysis - Data Science Research Project

This repository contains the implementation and findings of a data science project completed as part of the MSc-level module *Data Science Research Methods (L7)*. The primary objective of the project is to investigate whether the Open University's Virtual Learning Environment (VLE) has a measurable impact on student performance and to build a predictive model to estimate students' academic success based on their interaction with the VLE and demographic characteristics.

## Project Background

The Open University is a leading institution in distance education. With the increasing use of virtual learning platforms, there is a growing need to understand how student engagement in such platforms correlates with academic success. This project aims to provide empirical evidence for two fundamental questions:

1. Does active use of the VLE lead to higher academic performance among students?
2. Can we build a statistical model that accurately predicts student outcomes (e.g., pass/fail) based on demographic information and VLE activity?

The dataset used for this project is the **Open University Learning Analytics Dataset (OULAD)**, which includes anonymized information about students, courses, assessments, and their interactions with the virtual platform.

## Repository Contents

- `ou_vle_project.ipynb`  
  A complete Jupyter Notebook including the full data pipeline: loading, cleaning, exploratory data analysis (EDA), modeling, and evaluation.

- `DSRM_Report.pdf`  
  A 25-page academic report summarizing the methodology, visualizations, statistical findings, limitations, and conclusions.

- `data/`  
  Contains the cleaned and preprocessed data files used for analysis:
  - `assessments.xlsx`
  - `courses.xlsx`
  - `studentAssessment.xlsx`
  - `studentInfo.xlsx`
  - `studentRegistration.xlsx`
  - `vle.xlsx`

## Note on Missing File

The dataset `studentVle.csv`, which logs over 10 million rows of interaction data between students and the VLE system, is **not included** in this repository due to GitHub's file size limit (100 MB maximum per file). The file size is approximately 422 MB.

To fully replicate the analysis in the notebook, please download the file directly from the OULAD project page:  
**https://analyse.kmi.open.ac.uk/open_dataset**  
After downloading, place the `studentVle.csv` file into the `/data` directory.

## Tools, Technologies and Libraries Used

This project uses the following technologies and Python libraries:

- **Python 3.9+**
- **Pandas** (data manipulation and merging)
- **NumPy** (numerical operations)
- **Matplotlib** and **Seaborn** (visualizations)
- **Statsmodels** (hypothesis testing and regression analysis)
- **Scikit-learn** (feature selection, logistic regression, model evaluation)
- **Jupyter Notebook** (interactive data science workflow)

The data analysis and modeling tasks are written entirely in Python within a single `.ipynb` notebook.

## Methodology

### 1. Data Cleaning and Preparation

The OULAD dataset consists of seven main tables. These tables were loaded, cleaned, and joined based on common keys such as `id_student`, `code_module`, and `code_presentation`. Specific cleaning steps include:

- Handling missing values (`?` replaced with appropriate defaults or dropped).
- Removing duplicate entries.
- Normalizing categorical values (e.g., age bands, IMD bands).
- Filtering and aggregating VLE clickstream data per student-course pair.

### 2. Exploratory Data Analysis (EDA)

A comprehensive EDA was performed to understand:

- The distribution of modules, assessment types, and demographics.
- Relationships between VLE activity (e.g., total clicks) and final grades.
- Weekly usage patterns across student groups.
- Performance variation across modules, age bands, and socio-economic backgrounds.

### 3. Statistical Testing

A **two-sample independent t-test** was conducted to compare average VLE interaction between students who passed and those who failed. The null hypothesis assumed no difference between groups. All modules showed statistically significant differences (p < 0.05), indicating a strong relationship between VLE usage and success.

### 4. Modeling Approaches

Two models were explored:

- **Linear Regression**: Used initially to predict continuous overall scores based on total VLE interaction. However, the model performed poorly due to low R² values and non-linear relationships.

- **Logistic Regression**: Final model used to predict binary outcomes (Pass vs. Fail). Categorical variables were one-hot encoded, and multicollinearity was managed using dummy variable exclusion.

### 5. Feature Selection and Evaluation

Recursive Feature Elimination (RFE) was applied to identify the top 10 most informative features. The final logistic regression model achieved:

- Accuracy: 77.3%
- Precision: 77.2%
- Recall: 77.4%
- F1 Score: 77.2%

These metrics indicate a well-balanced and moderately accurate model for classification tasks.

## Key Findings

- Students who interact more with the VLE tend to perform better academically.
- Demographic factors such as education level, age band, and socio-economic status significantly affect outcomes.
- Certain modules (e.g., "FFF") are associated with higher failure rates and require additional support interventions.
- Students with disabilities or lower educational backgrounds are more likely to struggle, highlighting areas for inclusive learning support.

## How to Run This Project

1. **Clone the repository**:

   ```bash
   git clone https://github.com/ozozcelikoglu/open-university-vle-analysis.git
   ```

2. **Install the required Python packages**:

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn statsmodels
   ```

3. **Download the missing file** `studentVle.csv` from [OULAD](https://analyse.kmi.open.ac.uk/open_dataset) and place it in the `/data` folder.

4. **Run the notebook**:

   Open `ou_vle_project.ipynb` in Jupyter Notebook or Google Colab and execute the cells step by step.

## Limitations

- The imbalance between Pass and Fail labels could affect model generalization.
- The interaction data (`sum_click`) does not differentiate between meaningful engagement and passive clicks.
- The project is based solely on Open University data; conclusions may not generalize to other institutions.
- Due to GitHub limitations, not all raw data can be hosted directly in the repository.

## License and Attribution

- Dataset: [Open University Learning Analytics Dataset (OULAD)](https://analyse.kmi.open.ac.uk/open_dataset)
- Author: This project was completed for academic assessment within the MSc programme.
- License: Educational/Non-commercial use.
