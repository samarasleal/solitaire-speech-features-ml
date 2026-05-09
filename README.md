# Speech Features and Machine Learning Pipeline for Depression Recognition in Hikikomori Patients

## Overview

This repository is part of the SOLITAIRE project. It contains the code developed for machine learning-based speech analysis in depression assessment. The package supports reproducible analysis of acoustic features and their association with depression-related clinical outcomes.

> Note: This package is associated with the broader clinical project repository in Zenodo. The main project DOI will be added once available.

The resource includes:

- Python scripts for feature processing and machine learning-based speech analysis;
- documentation describing the speech-feature columns;
- citation information for the associated publication and Zenodo record.

## Data availability

The dataset is not stored in this GitHub repository. It is available through the associated Zenodo record, subject to the license and access conditions described there.

## How to cite

If you use this resource, please cite both the associated publication and this Zenodo record.

### Associated publication

Leal, S. S., Ntalampiras, S., Rossetti, M. G., Trabacca, A., Bellani, M., & Sassi, R. (2025). Speech-Based Depression Recognition in Hikikomori Patients Undergoing Cognitive Behavioral Therapy. *Applied Sciences, 15*(21), 11750. https://doi.org/10.3390/app152111750

### Zenodo record

Leal, S. S., Ntalampiras, S., & Sassi, R. (2026). *Speech Features and Machine Learning Pipeline for Depression Recognition*. Zenodo. DOI: 10.5281/zenodo.20099145

## Code relationship

- Main clinical/project DOI: [to be added when available]
- Dataset/code DOI: 10.5281/zenodo.20099145

## File contents

```text
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

For calculating standardized clinical outcome variables from HDRS/CDI raw scores, refer to the worksheet in the data folder of the main project DOI in Zenodo. Use `Patient_ID` as the cross-reference key.

## Ethical and access notes

This package does not include raw clinical audio or directly identifiable patient information. It was designed to run using only non-identifiable derived speech features and code.

## License

- MIT License or Apache 2.0.

## Versioning

If scripts or features are updated later, a new Zenodo version can be released while preserving the same concept DOI.
