# AD-Microbiome-ML-Extended

This repository is an individual extension of a team project on classifying Alzheimer's disease stages from gut microbiome data. The original project was completed for ENGG 680 (Digital Engineering) at the University of Calgary.

**Original team repository:** [AD-Microbiome-ML-Classification](https://github.com/haniya-naeem/AD-Microbiome-ML-Classification)

## Background

The original team project aimed to build a computational, data-driven diagnostic framework for Alzheimer's disease (AD) by combining microbiome-derived genome-scale metabolic models (GEMs) with machine learning. The main goal was to predict cognitive disease stages (Healthy, Mild Cognitive Impairment, and Alzheimer's disease) from gut microbial activity, allowing us to move towards a non-invasive and scalable approach for diagnosing AD.

The project pipeline consisted of three main stages:
1. Taxonomic preprocessing and relative abundance (RA) feature extraction using QIIME2.
2. Genome-scale metabolic modelling with MICOM and the AGORA database to derive metabolic flux features.
3. Machine learning classification using SVM and Random Forest models, trained on RA-only features and on combined RA + MICOM features.

The original project found that incorporating MICOM-derived metabolic features substantially improved classification performance as compared to using taxonomic composition alone. Full methodology, results, and discussion are available in the [final report](https://github.com/haniya-naeem/AD-Microbiome-ML-Classification/blob/main/Project%20Report_ENGG680_Group%2010.pdf)

## Purpose of This Repository

This repository contains independent continuation work on the project after the original team submission. The original team work, linked above, serves as the foundation. The work documented here aims to address the limitations identified in Section 4.5 of the original report and to develop the project into a more robust and generalizable classifier.

## Completed Work

### Hyperparameter Tuning

Grid-search hyperparameter tuning was performed on the SVM (RA + MICOM) classifier to optimize the regularization parameter (C) and the radial basis function kernel coefficient (gamma). The tuned model demonstrated improved test accuracy on the combined feature set as compared to the default SVM reported in the original team paper. Methodology, results, and limitations are documented in [`Hyperparameter Tuning/`](Hyperparameter%20Tuning/).

## Roadmap

The following extensions are planned for May 2026, after the conclusion of the current academic semester.

**Pipeline improvements to recover lost samples.** As described in Section 3.2 of the original report, MICOM was only able to reconstruct communities for 25 of 93 samples due to incomplete GEM coverage for many of the identified genera. This sample loss was the most significant constraint on the project, as it reduced statistical power and limited generalization across the AD, MCI, and healthy groups. Planned work includes investigating GEM coverage gaps for the missing genera, evaluating reconstruction strategies to fill these gaps, and benchmarking the recovered pipeline against the original 25-sample baseline.

**Cross-dataset validation.** The original project used only one cohort (NCBI PRJNA496408) collected from participants in Hangzhou, China. Validation on an independent public AD-microbiome dataset would test whether the model's findings generalize across populations and sequencing protocols. This would also address the reproducibility concerns raised in the broader literature on microbiome-based diagnostics, as referenced in Section 1.2 of the original report.

**Refined hyperparameter and feature engineering exploration.** Building on the initial hyperparameter tuning work, planned extensions include broader parameter search ranges, alternative feature selection strategies, and comparison with tree-based ensemble alternatives such as gradient boosting.

## Acknowledgments

The foundational work for this project was completed as part of ENGG 680 (Digital Engineering) at the University of Calgary's Schulich School of Engineering, taught by Dr. Hongzhou Yang, with teaching assistance from Shichuang Nie, Divya Bhavsar, and Jiageng Mi. The original team members were Haniya Naeem, Maryam Mayeli, Paula Marie Honrade, Qummar Mahmood, and Niki Mehri. This extension repository reflects independent follow-up work and does not represent the views or contributions of the original team beyond the foundational project linked above.
