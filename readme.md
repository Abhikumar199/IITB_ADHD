# ADHD Behavioral Modeling: Drift Diffusion & Latent State Analysis

## Overview

This repository contains an analysis of adult ADHD-related behavioral differences using Continuous Performance Test II (CPT-II) data from the publicly available HYPERAKTIV dataset. The workflow combines trial-level behavioral analysis, drift diffusion modeling (DDM), statistical testing, mixed-effects modeling, clinical symptom analysis, and machine-learning classification.

The central question is whether ADHD-related performance differences are better characterized by inconsistent responding than by generally slower reaction times, and whether DDM parameters provide complementary information about decision-making processes.

> **Research note:** These analyses are intended for research and computational phenotyping. Model outputs are not a standalone diagnostic tool.

## Study Sample and Data

The manuscript reports 99 participants in the behavioral analysis: 50 adults with ADHD and 49 clinical controls. After predefined trial-level preprocessing for DDM, two participants were excluded, leaving 97 participants (50 ADHD and 47 controls) and 30,433 valid Go-trial observations.

The analysis uses CPT-II performance and participant-level clinical/demographic measures, including:

- **ASRS** — Adult ADHD Self-Report Scale
- **WURS** — Wender Utah Rating Scale, including retrospective childhood symptoms
- **MADRS** — Montgomery–Åsberg Depression Rating Scale
- **CPT-II behavioral measures** — reaction time, reaction-time variability, accuracy, response rate, omission errors, commission errors, and detectability (*d′*)

The repository is currently organized into these top-level folders:

```text
.
├── Analysis/       # Analysis materials
├── Data/           # Data files used by the project
├── Plots & Tables/ # Figures and tabular outputs
├── code/           # Scripts and generated analysis tables
└── readme.md       # Project documentation
```

Check the folders for the current notebooks, scripts, data files, figures, and tables; exact file names and contents may change as the analysis develops.

## Research Questions

1. Do adults with ADHD show greater reaction-time variability than clinical controls?
2. Do DDM parameters indicate differences in evidence accumulation, decision caution, or non-decision processes?
3. Are DDM parameters associated with current or retrospective ADHD symptom severity?
4. How do behavioral-only, DDM-only, and combined features compare for ADHD classification?
5. How stable is feature selection when evaluated using nested cross-validation?

## Methods

### 1. Data preparation

The workflow includes data cleaning and validation, trial-level filtering, participant-level aggregation, and integration of behavioral, demographic, and clinical measures. The DDM analysis uses valid Go-trial observations remaining after the specified preprocessing criteria.

### 2. Behavioral analysis

Behavioral outcomes include mean hit reaction time, reaction-time standard deviation (as a measure of intra-individual variability), accuracy, response rate, omission-error rate, commission-error rate, and detectability (*d′*).

Statistical procedures described in the analysis include:

- Shapiro–Wilk normality testing
- Levene's test for homogeneity of variance
- Independent-group comparisons, including Mann–Whitney U tests where appropriate
- Effect-size estimates
- Bootstrap confidence intervals
- False-discovery-rate (FDR) correction for multiple comparisons where specified

### 3. Temporal attention analysis

Reaction-time patterns are examined across five trial-progress quintiles. Linear mixed-effects models assess the effects of ADHD group, trial progression, and their interaction, with participant-level random intercepts to account for repeated observations.

The manuscript describes models of the form:

```text
RT ~ ADHD + Trial + ADHD × Trial
RT ~ ADHD + Trial + ADHD × Trial + AGE + SEX
```

### 4. Drift diffusion modeling

The DDM decomposes response-time behavior into three interpretable parameters:

- **Drift rate (*v*):** efficiency of evidence accumulation
- **Boundary separation (*a*):** response caution or decision threshold
- **Non-decision time (*t*):** time associated with processes outside the core evidence-accumulation decision, such as stimulus encoding and motor response execution

The estimated parameters are compared across groups and examined in relation to clinical symptom scores. A multivariable logistic regression evaluates whether DDM parameters independently predict diagnostic group after accounting for age and sex.

### 5. Machine-learning classification

The analysis compares Logistic Regression, Support Vector Machine (RBF kernel), and Random Forest classifiers using behavioral features, DDM parameters, and combined feature sets. Evaluation includes ROC-AUC, accuracy, sensitivity, specificity, precision, negative predictive value, and F1-score, with cross-validation and bootstrap confidence intervals as described in the manuscript.

An exhaustive feature-subset procedure evaluates all 511 non-empty subsets of nine candidate features (six behavioral measures and three DDM parameters). Feature selection is carried out inside the inner cross-validation loop, and performance is evaluated on held-out outer folds to reduce selection-induced optimism.

## Main Findings Reported in the Manuscript

- **Reaction-time variability:** ADHD participants showed higher reaction-time variability than controls (0.130 s vs. 0.098 s; *p* = 0.0026; Cohen's *d* = 0.62).
- **Average reaction time:** Mean hit reaction time was similar between groups (approximately 0.39 s; *p* = 0.882), consistent with the interpretation that inconsistency was more prominent than generalized slowing in this sample.
- **DDM parameters:** Drift rate was lower in the ADHD group (*p* = 0.0224), and non-decision time was shorter (*p* = 0.0033). Boundary separation did not differ significantly between groups.
- **Clinical association:** Drift rate was negatively correlated with WURS scores after FDR correction (*r* = −0.302; corrected *p* = 0.016). In the reported adjusted logistic regression, non-decision time was the only DDM parameter independently associated with diagnostic group (*p* = 0.0073).
- **Classification:** The behavioral SVM model achieved a reported ROC-AUC of 0.784 and accuracy of 74.2%. A combined-feature Random Forest model achieved a ROC-AUC of 0.808, with accuracy of 71.1%.
- **Nested feature selection:** Across all outer folds, nested evaluation yielded 72.2% accuracy, 72.3% balanced accuracy, and ROC-AUC of 0.772. Selected feature subsets varied by fold, indicating that no single subset was consistently optimal in this sample.

These results should be interpreted in the context of the sample size, preprocessing choices, modeling assumptions, and validation design. Classification performance does not establish clinical diagnostic utility.

## Visualizations and Outputs

The project includes analysis outputs such as group-comparison plots, violin plots, reaction-time distributions, trial-progress curves, DDM parameter comparisons, clinical association plots, feature-importance plots, classification comparisons, and result tables. See `Plots & Tables/` and the relevant notebooks or scripts in `Analysis/` and `code/` for available outputs.

## Requirements

The documented Python dependencies include:

```bash
pip install numpy pandas scipy matplotlib seaborn statsmodels scikit-learn
```

Some scripts or notebooks may require additional packages depending on the current implementation. Install any extra dependencies shown in the relevant file or notebook before running it.

## Running the Analysis

1. Clone the repository:

   ```bash
   git clone https://github.com/Abhikumar199/IITB_ADHD.git
   cd IITB_ADHD
   ```

2. Create and activate a Python environment if needed.
3. Install the dependencies listed above and any additional dependencies required by the selected notebook or script.
4. Review the `Data/`, `Analysis/`, `code/`, and `Plots & Tables/` folders to identify the relevant inputs and analysis entry point.
5. Open Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

6. Open the relevant notebook or script and run the analysis in order, ensuring the expected data paths are correct for your local setup.

## Reproducibility and Data Use

Results depend on the input data, preprocessing criteria, package versions, and random seeds used by each analysis. Where possible, record these details when reproducing results. Respect the HYPERAKTIV dataset's access conditions and terms of use, and do not add identifiable participant data or other sensitive information to public commits.

## Research Applications

This framework may support further research in:

- Computational psychiatry and computational phenotyping
- Behavioral markers of attentional instability
- Decision-process modeling in adult ADHD
- Interpretable machine-learning analysis of cognitive-task data
- Follow-up studies that combine behavioral measures with neural or physiological data

## License

The previous README stated that the project is released under the MIT License. Ensure that a valid `LICENSE` file is present in the repository before relying on that license statement.
