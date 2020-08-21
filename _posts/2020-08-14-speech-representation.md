---
layout: post
title:  "Pre-processing of Speech Signals"
author: pranoot
categories: [ Speech, Tutorial]
image: assets/images/spectrogram.png
tags: [Speech, Tutorial]
---

The audio signal representes simply the time vs amplitude relation. For carrying of several Speech releated tasks eg. Speech Recogniton, Speaker Identification, Emotion Recognition etc. we can represent this in feature space capable of capurting the time frequencty and the energy using furthur processing on the audio signal. We as humans try to get representations by transformation over representaions and we develop representations over those representation till we get a best representaion of that signal. Here I will dicuss some of those digital representation of aaudio signal.

* waveforms
* FFT
* STFT
* spectrogram

<!-- Several represeantaions
- Engineers : MFCC, Triphones, HMM, Network
- Phonetics : Formants, IPA, Gestures, Spectrograms
- Linguistics : Phonemes, Allophones, Morphemes -->


##### Wave form 
Waveform is the acquisition of audio signal strenth with respect to time. For every audio signal we define the sampling rate and bits/channel. Audio is an analog signal we convert it to digial signal for further procesing. For that we sample the analog signal at a sampling rate and for each signal acquired we store that strength of the signal in bits. Higher the bitrate quality of the audio is more. higher the sample rate more samples are caputred ina particular time frame.


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

