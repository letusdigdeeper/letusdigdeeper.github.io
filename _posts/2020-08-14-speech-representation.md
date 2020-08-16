---
layout: post
title:  "Pre-processing of Speech Signals - Only keypoints for now "
author: pranoot
categories: [ Speech, Tutorial]
image: assets/images/processing.png
tags: [Speech, Tutorial]
---


Transformation from digital representaions, we develop representations over representation.

Several represeantaions
- Engineers : MFCC, Triphones, HMM, Network
- Phonetics : Formants, IPA, Gestures, Spectrograms
- Linguistics : Phonemes, Allophones, Morphemes
 
we will discuss :
* waveforms
* FFT
* STFT
* spectrogram


##### Wave form 
- WAves is acquisition of amplitude with respect to time
- Sampling Rate 
- bits/channel

##### FFT - Fast Fourier Transform
- summation of sin waves of different frequiences
- waveform to foruier transform is power spectrum
- magnitude as function of frequency
- move from time to frequency domain
- we lose on temporal data as we calculate calculate the FFT on the whole signal 
- <photo 1> - sum of signals
- <photo 2> - fft of same signal


##### STFT - Short Time Fourier Transform
- Calculate FFT at differnt intervals
- Fixed window which moves over the signal to calculte the FFT
- 3 Dimensions time x frequency x amplitude
- we do not lose the temporal data and can leverage to calculte the change of amplitude wrt time and frequency
- <photo1 > - STFT photo for same signal


##### MFCC - Mel Frequency Cepstral Coefficients
- Its a represtation of short term power spectrum
- Capture the textural aspect of the signal
- Only in the frrequncy bins vs time vs amplitude domain
- replicates the human auditory system
- 13-40 coefficients
- Steps
 * take fft (poewr spectrum for frames)
 * map the powers to mel scale using traingular overlapping (contribution of of energy in differnt frequncy regions)
 * Take logs of poer (humans do not hear on linear scale so we convert to log scale)
 * take dct - to find what frequencies the singals belong to
 
- <photo 1> - MFCC photo for same signal

