# Hyperparameter Tuning

This folder documents grid-search hyperparameter tuning of the SVM classifier on the combined relative abundance (RA) and MICOM feature set from the [original team project](https://github.com/haniya-naeem/AD-Microbiome-ML-Classification).

## Background

The original project evaluated four classification models using default scikit-learn parameters: SVM and Random Forest, each on RA-only features and on combined RA + MICOM features. The Random Forest (RA + MICOM) model achieved the strongest performance overall with a test accuracy of 62% and weighted F1 score of 0.62. SVM (RA + MICOM) reached the same test accuracy of 62% but with a lower weighted F1 of 0.53. This was due to the SVM failing to predict any healthy samples correctly, as shown in Section 3.5 of the original report.

## Methods

Grid-search cross-validation was performed to tune the SVM (RA + MICOM) classifier. Two hyperparameters were tuned: regularization strength (C) and the radial basis function kernel coefficient (gamma). 

A dictionary of possible hyperparameter values was defined as follows:
- C: [0.1, 1, 10, 100]
- gamma: [0.001, 0.01, 0.1, 1]

GridSearchCV was used to evaluate model performance across all combinations of C and gamma. 5-fold cross-validation was performed on the training set, and the best performing combination was selected and refit on the full training set. The tuned model was then used to classify samples in the held-out test set.

The best hyperparameter combination was C = 100 and gamma = 0.001.

## Results

Table 1 summarizes the classification metrics for the tuned SVM (RA + MICOM) model on the test set. Default SVM (RA + MICOM) results from Section 3.5 of the original report are included for comparison.

**Table 1.** Test set classification metrics for the default and tuned SVM (RA + MICOM) models. Class-specific precision and recall are reported alongside overall test accuracy and weighted F1 score.

| Metric | Default SVM | Tuned SVM |
|---|---|---|
| Test accuracy | 0.62 | 0.75 |
| Weighted F1 | 0.53 | 0.74 |
| AD precision | 0.60 | 0.75 |
| AD recall | 0.75 | 0.75 |
| Healthy precision | 0.00 | 1.00 |
| Healthy recall | 0.00 | 0.50 |
| MCI precision | 0.67 | 0.67 |
| MCI recall | 1.00 | 1.00 |

The tuned SVM model demonstrated improved test accuracy (0.75) and weighted F1 (0.74) as compared to the default SVM (0.62 and 0.53, respectively). AD precision improved from 0.60 to 0.75 while AD recall remained at 0.75. The most notable improvement was for the healthy class, where the tuned model achieved a precision of 1.00 and recall of 0.50, recovering classification ability that was absent in the default model. MCI precision and recall were unchanged across both models.

## Limitations

The reported improvement in test accuracy from 0.62 to 0.75 must be interpreted with caution due to the small size of the RA + MICOM dataset. As discussed in Section 3.2 of the original report, MICOM was only able to reconstruct communities for 25 of 93 samples due to incomplete GEM coverage. The 70/30 train-test split therefore left only 8 samples in the test set (4 AD, 2 Healthy, 2 MCI). At this sample size, an improvement from 62% to 75% test accuracy represents only one additional correctly classified sample. The tuned model results should therefore be considered a preliminary signal rather than a robust performance estimate.

The tuned SVM also exhibited a 5-fold cross-validation accuracy of approximately 42% on the training set, which is lower than its 75% test accuracy. This is the opposite of what is typically observed when a model overfits during training. The discrepancy is likely a result of the small training set size of 17 samples, which leaves very few samples per condition in each cross-validation fold. The cross-validation accuracy estimates are therefore unstable.

These limitations support the conclusion drawn in Section 4.5 of the original report. The most significant constraint on this model is the loss of samples during MICOM community reconstruction. Further hyperparameter optimization is unlikely to produce meaningful and reproducible improvements until GEM coverage can be expanded and a larger sample population is available for training and evaluation. This is the priority direction outlined in the [future work roadmap](../README.md).

## Code

The hyperparameter tuning is implemented in cells 19 and 28 of [`Machine_Learning_Analysis.ipynb`](https://github.com/haniya-naeem/AD-Microbiome-ML-Classification/blob/main/Machine_Learning_Analysis.ipynb) in the original team repository. A standalone notebook for this extension repository is planned as part of the work outlined in the [future work roadmap](../README.md).

