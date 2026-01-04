# Intrusion Detection using NSL-KDD Dataset

This project implements deep learning models for network intrusion detection using the NSL-KDD dataset. The goal is to classify network traffic as either normal or one of four attack types: DOS, Probe, R2L, or U2R.

## Overview

The NSL-KDD dataset is a refined version of the KDD Cup 99 dataset, commonly used for intrusion detection research. It contains network connection records with 41 features and 5 attack categories. The main challenge here is handling severe class imbalance - some attack types have thousands of samples while others have only dozens.

## Approach

I experimented with two types of neural network architectures:

1. **Deep Neural Network (DNN)**: A simple feedforward network with dense layers
2. **Convolutional Neural Network (CNN)**: A 1D CNN that treats the feature vector as a sequence

To address the class imbalance problem, I used **Adaptive Synthetic Sampling (ADASYN)**. This technique generates synthetic samples for minority classes, focusing on harder-to-learn examples. I also tried cost-sensitive learning with sample weights, but ADASYN gave better results.

## Results

The CNN model achieved **84.27% accuracy** on the test set, outperforming the baseline DNN approach. Here's the breakdown by attack type:

- **DOS**: 97% precision, 89% recall
- **Normal**: 82% precision, 94% recall  
- **Probe**: 76% precision, 92% recall
- **R2L**: 90% precision, 34% recall
- **U2R**: 6% precision, 43% recall

The R2L and U2R classes remain challenging due to their extremely small sample sizes (995 and 52 samples respectively in the training set), but ADASYN helped improve their detection compared to the baseline.

## Dataset

You'll need the NSL-KDD dataset files:
- `KDDTrain+.txt` - Training set
- `KDDTest+.txt` - Test set

Update the file paths in the notebook to point to where you've stored these files.

## Requirements

- pandas
- tensorflow/keras
- scikit-learn
- imbalanced-learn (for ADASYN)
- numpy
- seaborn
- bioinfokit (for visualization)

## Usage

The main work is in `Intrusion_Detection.ipynb`. The notebook covers:

1. Data loading and preprocessing (one-hot encoding, normalization)
2. Baseline DNN model with sample weighting
3. DNN model with ADASYN resampling
4. CNN model with ADASYN resampling (best performing)
5. Evaluation metrics and visualizations

Run the cells sequentially. The models automatically save when validation accuracy exceeds 83%.
