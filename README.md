# Breast Cancer Survival Analysis using Double Machine Learning
This project looks at the **METABRIC** dataset to see how chemotherapy affects the survival time of breast cancer patients. It combines clinical data with genetic information to get a clearer picture of patient outcomes.

## Project Overview
The goal of this analysis is to find the real impact of chemotherapy on survival. Since outcomes are influenced by thousands of genes, I used **Double Machine Learning (DoubleML)** to separate the treatment's effect from the "noise" of genetic factors.

## Research Motivation
In medicine, it’s hard to tell if a treatment like chemotherapy is the main reason a patient gets better. Every patient has a unique genetic makeup that also affects their health. 

I wanted to use data science to look past these genetic differences. By filtering out the noise from the 500 most important genes, I aimed to find the true link between chemotherapy and survival. Essentially, I'm trying to answer: **Does the treatment itself make the difference when we account for genetics?**

## Methodology 
Using the METABRIC dataset ($n = 1,964$), I implemented a Double Machine Learning (DML) framework using a Partially Linear Regression (PLR) model. To address the challenge of high dimensionality, I used Random Forest learners to model both the treatment assignment (Chemotherapy) and the outcome (Survival Months), incorporating 500 gene expression features and Age at Diagnosis as covariates. Data was preprocessed by removing duplicates and Standard Scaling to ensure model stability.

## The Results
After controlling for age and the top 500 high-variance genes, here is what the model found:

| Metric | Value | Meaning |
| :--- | :--- | :--- |
| **Coefficient (Effect)** | **-26.94** | Chemotherapy is associated with lower survival months in this dataset. |
| **P-value** | **0.000...** | The result is highly significant (not due to chance). |
| **95% Confidence Interval** | **[-35.79, -18.09]** | We are very sure the effect falls within this range. |

### **Interpreting the Result**
Our model shows a **negative coefficient of -26.94**. In simple terms, patients who received chemotherapy in this specific dataset had a shorter survival time (about 28 months less) than those who didn't, even after adjusting for genetics.

**Why is it negative?** In many real-world datasets, chemotherapy is usually given to patients who are already in a more advanced or aggressive stage of cancer. Even though we controlled for 500 genes, this "negative" result likely reflects that the sickest patients were the ones receiving the most aggressive treatment.

The negative coefficient likely indicates Selection Bias or Confounding by Indication, where chemotherapy was systematically prescribed to patients with more aggressive clinical phenotypes not fully captured by the genomic features alone.

## Conclusion
This study demonstrates the utility of DML in handling high-dimensional clinical data while highlighting the critical importance of unobserved clinical confounders in observational oncological research.

## Quick Start
If you want to replicate this study:

Data: You need the Metabric clinical_patient, clinical_sample, and mrna_illumina_microarray files.

Libraries:

```Bash
pip install pandas scikit-learn doubleml
```
Run: Simply open metabric_causal_inference.ipynb and run the cells.

## Data Source
Link: https://www.cbioportal.org/study/summary?id=brca_metabric
