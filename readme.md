# ADHD Behavioral Modeling: Drift Diffusion & Latent State Analysis

## Overview

This project investigates behavioral markers of Attention Deficit Hyperactivity Disorder (ADHD) using Continuous Performance Task (CPT) data. The analysis focuses on reaction time dynamics, intra-individual variability, task accuracy, and latent cognitive states associated with attentional control.

The notebook combines statistical analysis, mixed-effects modeling, and cognitive performance metrics to identify behavioral differences between ADHD and control participants.

---

## Objectives

- Compare behavioral performance between ADHD and control groups.
- Quantify reaction time variability (IIV).
- Analyze task accuracy and response patterns.
- Model temporal changes in attention across trials.
- Apply mixed-effects models to account for subject-level variability.
- Explore latent cognitive states underlying attentional fluctuations.

---

## Dataset

The analysis uses:

- `long_CPT.csv` – Trial-level Continuous Performance Task data.
- `patient_info.csv` – Participant demographic and clinical information.

### Key Variables

| Variable | Description |
|-----------|------------|
| subject | Participant ID |
| ADHD | ADHD diagnosis (0 = Control, 1 = ADHD) |
| rt_sec | Reaction time (seconds) |
| correct | Response correctness |
| stimulus | Trial stimulus |
| AGE | Participant age |
| SEX | Participant sex |

---

## Methodology

### 1. Data Preprocessing

- Data cleaning and validation
- Missing value handling
- Trial-level and subject-level aggregation
- Demographic data integration

### 2. Behavioral Analysis

Computed metrics include:

- Mean Reaction Time (RT)
- RT Standard Deviation (Intra-Individual Variability)
- Task Accuracy
- Response Rate

Statistical procedures:

- Shapiro-Wilk Normality Test
- Levene's Homogeneity Test
- Mann-Whitney U Test
- Effect Size (Cohen's d)
- Bootstrap Confidence Intervals

### 3. Temporal Attention Analysis

Performance trends are examined across task progression using:

- Trial Quintile Analysis
- Reaction Time Drift
- Accuracy Dynamics

### 4. Mixed-Effects Modeling

Linear Mixed-Effects Models evaluate:

\[
RT \sim ADHD + Trial + ADHD \times Trial
\]

Covariate-adjusted models include:

\[
RT \sim ADHD + Trial + ADHD \times Trial + AGE + SEX
\]

Random intercepts account for individual participant differences.

---

## Main Findings

- ADHD participants exhibit significantly higher reaction time variability.
- Average reaction speed shows limited group differences.
- ADHD participants demonstrate lower task accuracy.
- Results support impaired attentional stability rather than generalized psychomotor slowing.

---

## Visualizations

The notebook generates:

- Group comparison plots
- Violin plots
- Distribution analyses
- Trial progression curves
- Mixed-effects model summaries

---

## Requirements

Install dependencies:

```bash
pip install numpy pandas scipy matplotlib seaborn statsmodels scikit-learn
```

---

## Project Structure

```text
├── ADHD_Behavioral_Modeling.ipynb
├── long_CPT.csv
├── patient_info.csv
└── README.md
```

---

## Running the Analysis

1. Clone the repository:

```bash
git clone https://github.com/yourusername/ADHD-Behavioral-Modeling.git
```

2. Place the dataset files in the project directory.

3. Launch Jupyter Notebook:

```bash
jupyter notebook
```

4. Open:

```text
ADHD_Behavioral_Modeling.ipynb
```

5. Run all cells sequentially.

---

## Research Applications

This framework can be extended for:

- ADHD biomarker discovery
- Cognitive neuroscience studies
- Computational psychiatry
- Digital phenotyping
- Neuropsychological assessment

---

## Author

**Abhishek Kumar**

M.S. in Artificial Intelligence & Data Science  
ABV-IIITM Gwalior

Research Interests:
- Computational Neuroscience
- Neuromorphic Computing
- Spiking Neural Networks
- Cognitive Modeling
- AI for Mental Health

---

## License

This project is released under the MIT License.