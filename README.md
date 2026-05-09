# Speech Features and Machine Learning Pipeline for Depression Recognition in Hikikomori Patients

## Overview

This repository is part of the SOLITAIRE project. It contains a dataset package with non-identifiable speech features derived from hikikomori patients undergoing cognitive behavioral therapy (CBT), along with code developed for machine learning-based speech analysis in depression assessment. The package supports reproducible analysis of acoustic features and their association with depression-related clinical outcomes.

> Note: This package is associated with the broader clinical project repository. The main project DOI will be added once available.

The resource includes:

- segment-level acoustic features derived from speech recordings of 35 patients across 8 CBT sessions;
- Python scripts for feature processing and machine learning-based speech analysis;
- documentation describing the speech-feature columns;
- citation information for the associated publication and Zenodo record.

## How to cite

If you use this resource, please cite both the associated publication and this Zenodo record.

### Associated publication

Leal, S. S., Ntalampiras, S., Rossetti, M. G., Trabacca, A., Bellani, M., & Sassi, R. (2025). Speech-Based Depression Recognition in Hikikomori Patients Undergoing Cognitive Behavioral Therapy. *Applied Sciences, 15*(21), 11750. https://doi.org/10.3390/app152111750

### Zenodo record

Leal, S. S., Ntalampiras, S., & Sassi, R. (2026). *Speech Features and Machine Learning Pipeline for Depression Recognition*. Zenodo. DOI: [to be added]

## Dataset relationship

This dataset is associated with the main clinical project repository:

- Main clinical/project DOI: [to be added when available]
- Speech-feature/code DOI: [Zenodo DOI for this record]

## Data contents

```text
speech_features/
  EMB35.pkl
  MFCC35.pkl

code/
  Binary_emb.ipynb
  Binary_mfccs.ipynb
  Multiclass_emb.ipynb
  Multiclass_mfccs.ipynb
  Regression_emb.ipynb
  Regression_mfccs.ipynb
  Data_Preprocessing/
    DataPreprocessing_melt.ipynb
  Data_Processing/
    TargetVariables.ipynb
    DataProcessing_run.ipynb

metadata/
  data_dictionary.csv
  processing_and_modeling_details.md
```

## Expected data format

The data files are organized in wide format, with one row per anonymized patient. Acoustic features are stored as session- and segment-specific columns.

| Column pattern | Description |
|---|---|
| `Patient_ID` | Anonymized patient identifier |
| `MFCC_Session{session}_Segment{segment}_MeanCoefficient{coeff}` | Mean MFCC value for coefficient `{coeff}` extracted from a 5-second speech segment |
| `MFCC_Session{session}_Segment{segment}_StdCoefficient{coeff}` | Standard deviation of MFCC coefficient `{coeff}` extracted from a 5-second speech segment |
| `Embeddings_Session{session}_MeanSegment{segment}` | Mean wav2vec 2.0 embedding summary for a 5-second speech segment |
| `Embeddings_Session{session}_StdSegment{segment}` | Standard deviation wav2vec 2.0 embedding summary for a 5-second speech segment |

Sessions range from `Session1` to `Session8`. Segment indices vary according to the number of valid speech segments available per session. MFCC coefficients range from `Coefficient1` to `Coefficient13`.

## Code summary

The `code/` folder contains scripts used to prepare the provided feature tables and run the machine learning experiments. The repository does not include raw audio files or the full audio-cleaning pipeline; the shared data consist of non-identifiable, pre-extracted speech features.

The code supports the following steps:

1. loading the pre-extracted speech-feature tables;
2. melting the wide dataframe to restructure the data so that each row corresponds to a patient speech segment;
3. creating target variables from standardized HDRS/CDI score changes;
4. restructuring feature tables into model-ready formats;
5. preparing MFCCs and wav2vec 2.0 feature representations;
6. running patient-independent Leave-One-Out cross-validation;
7. training and evaluating classification, regression, binary, and multiclass models;
8. summarizing patient-level metrics such as recall, precision, and F1-score.

For calculating standardized clinical outcome variables from HDRS/CDI raw scores, refer to the worksheet in the data folder of the main project DOI. Use `Patient_ID` as the cross-reference key.

## Ethical and access notes

This repository does not contain raw clinical audio or directly identifiable patient information. It includes only non-identifiable derived speech features and code.

## License

- Dataset/features: CC BY 4.0;
- Code: MIT License or Apache 2.0.

## Versioning

If scripts or features are updated later, a new Zenodo version can be released while preserving the same concept DOI.
