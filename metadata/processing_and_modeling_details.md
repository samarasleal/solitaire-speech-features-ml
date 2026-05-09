# Processing and Modeling Details

## Scope

This repository contains non-identifiable, pre-extracted speech features and the code used to structure these features for machine learning experiments in the SOLITAIRE project.

Raw audio files and the full audio-cleaning / feature-extraction pipeline are not included in this repository. The shared data consist of derived acoustic representations, including MFCC-based features and wav2vec 2.0 embeddings.

## Repository purpose

The code supports reproducible machine learning experiments using the provided speech-feature tables. Specifically, it includes scripts for:

1. loading the pre-extracted speech-feature tables;
2. melting the wide dataframe to restructure the data so that each row corresponds to a patient speech segment;
3. creating target variables from standardized HDRS/CDI score changes;
4. restructuring feature tables into model-ready formats;
5. preparing MFCC and wav2vec 2.0 feature representations;
6. running patient-independent Leave-One-Out cross-validation;
7. training and evaluating classification, regression, binary, and multiclass models;
8. summarizing patient-level metrics such as recall, precision, and F1-score.

## Clinical outcome construction

Clinical outcome variables are derived from pre- and post-treatment depression severity scores.

Depending on the experiment, outcomes may be based on:

- standardized change in depression scores;
- HDRS-based change for adult participants;
- CDI-based change for adolescent participants.

The scripts include procedures to define binary outcome labels such as `Better` and `Worse` using percentile-based thresholds.

For calculating standardized clinical outcome variables from raw HDRS/CDI scores, refer to the worksheet in the data folder of the main project DOI. Use `Patient_ID` as the cross-reference key.

## Feature representations

The repository contains MFCC-based features and wav2vec 2.0 embeddings.

### MFCC features

MFCC features are provided as segment-level summaries. Column names follow the structure:

```text
MFCC_Session{session}_Segment{segment}_MeanCoefficient{coeff}
MFCC_Session{session}_Segment{segment}_StdCoefficient{coeff}
```

where:

- `session` corresponds to the CBT session index [1-8];
- `segment` corresponds to a 5-second speech segment;
- `coeff` corresponds to the MFCC coefficient index [1-13].

### wav2vec 2.0 embeddings

wav2vec 2.0 features are provided as segment-level embedding summaries. Column names follow the structure:

```text
Embeddings_Session{session}_MeanSegment{segment}
Embeddings_Session{session}_StdSegment{segment}
```

## Data restructuring

The `Data_Preprocessing` scripts convert the wide feature tables into model-ready dataframes.

The code supports the following steps:

- retaining patient-level metadata and target columns;
- melting or reshaping MFCC and wav2vec 2.0 embedding features into segment-level or session-level formats;
- removing rows with missing target labels or incomplete feature representations.

## Machine learning experiments

The repository includes scripts for multiple prediction settings, including:

- binary classification;
- multiclass classification;
- regression;
- MFCC-based models;
- wav2vec 2.0-based models;
- patient-independent evaluation.

Typical models include:

- Random Forest;
- Logistic Regression;
- XGBoost;
- Multi-Layer Perceptron;

## Leave-One-Out patient-independent evaluation

Experiments are performed using a patient-independent Leave-One-Out protocol.

For each fold:

1. one patient is held out as the test subject;
2. all remaining patients are used for training;
3. model selection or grid search is performed only on the training data;
4. predictions are generated for the held-out patient;
5. patient-level metrics are computed and aggregated across folds.

This protocol ensures that data from the same patient do not appear in both training and testing sets.

## Evaluation metrics

The scripts summarize patient-level metrics, including:

- RMSE, MSE, and MAE for regression tasks;
- patient-level accuracy;
- positive-class recall;
- specificity;
- precision;
- F1-score.

## Notes on reproducibility

To reproduce the experiments:

1. place the feature file in the expected folder;
2. update input paths in the scripts if necessary;
3. update target-column values [For calculating standardized clinical outcome variables from HDRS/CDI raw scores, refer to the worksheet in the data folder of the main project DOI. Use `Patient_ID` as the cross-reference key.];
4. run the corresponding experiment script;
5. inspect generated fold-level and summary-level results.

Random seeds are set in model constructors where supported.

## Privacy and data protection

This repository should not contain identifiable patient information or raw clinical audio.

Users must not attempt to re-identify participants.

Any use of the data must comply with the license, ethics approvals, and restrictions described in the main README.
