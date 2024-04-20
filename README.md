# Multi-class Classification of Bird Species based on Birdsongs

## About the Project

This is a simple, exploratory project on attempting classify bird species using birdsongs. The data set is the <a href="https://www.kaggle.com/datasets/rtatman/british-birdsong-dataset">British Birdsong dataset</a> taken from Kaggle. It has 264 samples from 88 unique bird species. 

## About the Team

You can find the commit history of each member in the repository.

## How to Use this Repository

We have two notebooks `EDA.ipynb` and `CNN.ipynb`. The order to review them is 
1. `EDA.ipynb`
2. `CNN.ipynb`

# Exploratory Data Analysis

We extracted features from the audio signals for visualisation and considered how they can help in this classification problem. The feature extraction is mainly done using the `librosa` library.

## Metadata Analysis

The distribution of classes in the sample is balanced. With 3 members per class. 

![Histogram of Class Distribution](./figures/class_distribution.png)

To listen to the audio samples, download the `EDA.ipynb` as `ipy.display` does not work when the notebook is rendered in GitHub.

## Time Domain Analysis

In time domain, we explored the amplitude envelope, root-mean-squared energy, and zero crossing rate.

![Time Domain Analysis](./figures/time_domain.png)

## Frequency Domain Analysis

In the frequency domain, we explored the frequency spectrum:

![Frequency Spectrum Analysis](./figures/frequency_spectrum.png)

as well as the spectral centroid:

![Spectral Centroid Analysis](./figures/spectral_centroid.png)

## Time-frequency Domain Analysis

In the frequency domain, we explored the spectrogram:

![Spectrogram](./figures/spectrogram.png)

the Mel spectogram:

![Mel Spectrogram](./figures/mel_spectrogram.png)

as well as the Mel-Frequency Cepstrum:

![MFCC](./figures/mfcc.png)

# Data Processing

## Reducing Noise

We used the `NoiseReduce` library to reduce background noise of signals.

![Effect of Noise Reduce](./figures/noisereduce.png)

## Standardising Duration

We used the `audiomentations` library to standardise audio duration. We chose to pad / clip to 50s based on the distribution of the audio duration:

![Audio Duration Distribution](./figures/duration_distribution.png)

# Traditional Machine Learning Model

We tested two models from the `sklearn` library: K-Nearest-Neighbour and Random Forest models. We used `GridSearch_CV` to attempt to fine tune hyperparameters. Unfortunately, the test accuracy is low, at 28%. 

We concluded that this was due to low member counts in each class, yet high number of classes. To solve this problem, we applied data augmentation and tested out a CNN model.

# Data Augmentation

We generated 528 extra samples using data augmentation, bringing the total sample size to 792. 

## Augmentation Technique

This is done by horizontal flip and noise introduction, using `skimage` library.

![Data Augmentation](./figures/data_augmentation.png)

Example of the final transformations:

![Transformation Results](./figures/transformation.png)

# Convoluted Neural Network

We attempted to use a CNN model using the `Keras` API.

## Parameters

![CNN Parameters](./figures/parameter.png)

## Train and Test Loss

![Train and Test Loss Curve](./figures/hist_train_test_loss.png)

## Train and Test Accuracy

![Train and Test Accuracy Curve](./figures/hist_train_test_accuracy.png)

## Confusion Matrix

We represent the bird species as discrete classes, represented from 0 to 87.

![Confusion Matrix](./figures/confusion_matrix_cnn.png)

## Score Metrics

- Test Accuracy score =  55.97%
- Test Precision score =  57.58%
- Test Recall score =  53.52%
- Test Set F-score score =  51.56%

# Reference

This project makes several references to different sources, including GitHub repositories. These references are detailed in the `.ipynb`. The following is just a list for overview

- [1] L. Zenkov, “sklearn-audio-classification ,” *GitHub*, 2020. https://github.com/IliaZenkov/sklearn-audio-classification/blob/master/sklearn_audio_classification.ipynb (accessed Apr. 03, 2024).
- [2] N. Agrawal, “Decoding the Symphony of Sound: Audio Signal Processing for Musical Engineering,” *Medium*, Aug. 08, 2023. https://towardsdatascience.com/decoding-the-symphony-of-sound-audio-signal-processing-for-musical-engineering-c66f09a4d0f5
- [3] Md Shahrin, Muhammad Huzaifah. (2017). Comparison of Time-Frequency Representations for Environmental Sound Classification using Convolutional Neural Networks.
- [4] Sharma, Garima & Umapathy, Kartikeyan & Krishnan, Sridhar. (2020). Trends in audio signal feature extraction methods. *Applied Acoustics*. 158. 107020. 10.1016/j.apacoust.2019.107020.
- [5] R. Vidiyala, “Normalization vs Standardization,” *Medium*, Jun. 28, 2020. https://towardsdatascience.com/normalization-vs-standardization-cb8fe15082eb
- [6] J. F. Santos, “jfsantos/keras-tutorial,” *GitHub*, Jan. 04, 2024. https://github.com/jfsantos/keras-tutorial (accessed Apr. 03, 2024).

