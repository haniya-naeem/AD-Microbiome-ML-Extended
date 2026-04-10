# AD-Microbiome-ML-Extended

An individual extension of a team project on classifying Alzheimer's disease stages from gut microbiome data, building on work originally completed for ENGG 680 (Digital Engineering) at the University of Calgary.

**Original team repository:** [AD-Microbiome-ML-Classification](https://github.com/haniya-naeem/AD-Microbiome-ML-Classification)

## Background

The original team project developed a computational diagnostic framework for Alzheimer's disease (AD) by integrating microbiome-derived genome-scale metabolic models (GEMs) with machine learning to predict cognitive disease stages (Healthy, Mild Cognitive Impairment, and Alzheimer's disease) from gut microbial activity. The pipeline combined 16S rRNA taxonomic profiling using QIIME2 with community-level metabolic modeling using MICOM and the AGORA genome-scale metabolic model database, then trained Support Vector Machine and Random Forest classifiers on two feature sets: relative abundance (RA) features alone, and RA combined with MICOM-derived metabolic flux features.

The original project found that incorporating MICOM-derived metabolic features substantially improved classification performance compared to using taxonomic composition alone. Full methodology, results, and discussion are available in [final report](https://github.com/haniya-naeem/AD-Microbiome-ML-Classification/blob/main/Project_Report_ENGG680_Group_10.pdf).

## Purpose of This Repository

This repository contains my individual continuation of the project after the course concluded. The original team work stands as the foundation; the work here represents extensions that I am pursuing on my own to address limitations identified in the original report and to develop the project into a more robust, generalizable classifier.

## Completed Work

### Hyperparameter Tuning

Grid-search hyperparameter tuning of the SVM classifier on the combined RA + MICOM feature set, improving held-out test accuracy compared to the default-parameter SVM reported in the original team paper. Full details, methodology, and a discussion of the small-sample-size considerations are documented in [`hyperparameter-tuning/`](hyperparameter-tuning/).

## Roadmap

The following extensions are planned for May 2026.

**Pipeline improvements to recover lost samples.** The original MICOM step retained only 25 of 93 samples because many genera lacked corresponding genome-scale metabolic models in the AGORA database. This sample loss was the single largest constraint on the project's statistical power. Planned work includes investigating GEM coverage gaps for the missing genera, evaluating reconstruction strategies to fill those gaps, and benchmarking the recovered pipeline against the original 25-sample baseline.

**Cross-dataset validation.** The original project used a single cohort (NCBI PRJNA496408) collected from participants in Hangzhou, China. Cross-dataset validation on an independent public AD-microbiome cohort would test whether the model's findings generalize across populations and sequencing protocols, and would directly address the reproducibility concerns raised in the literature on microbiome-based diagnostics.

**Refined hyperparameter and feature engineering exploration.** Building on the initial hyperparameter tuning work, this includes broader parameter search, alternative feature selection strategies, and possibly tree-based ensemble alternatives (gradient boosting) for comparison against the Random Forest baseline.

## Acknowledgments

The foundational work for this project was completed as part of ENGG 680 (Digital Engineering) at the University of Calgary's Schulich School of Engineering, taught by Dr. Hongzhou Yang, with teaching assistance from Shichuang Nie, Divya Bhavsar, and Jiageng Mi. The original team members were Haniya Naeem, Maryam Mayeli, Paula Marie Honrade, Qummar Mahmood, and Niki Mehri. This extension repository reflects independent follow-up work and does not represent the views or contributions of the original team beyond the foundational project linked above.
