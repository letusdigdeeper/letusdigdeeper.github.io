---
layout: post
title:  "Pre-processing of Speech Signals"
author: pranoot
categories: [ Speech, Tutorial]
image: assets/images/post_1/spectrogram.png
tags: [Speech, Tutorial]
---

The audio signal representes simply the time vs amplitude relation. For carrying of several Speech releated tasks eg. Speech Recogniton, Speaker Identification, Emotion Recognition etc. we can represent this in feature space capable of capurting the time frequencty and the energy using furthur processing on the audio signal. We as humans try to get representations by transformation over representaions and we develop representations over those representation till we get a best representaion of that signal. Here I will dicuss some of those digital representation of audio signal.

Lets have a look at few things and visualize them using python.
* waveforms
* FFT
* STFT
* spectrogram

<!-- Several represeantaions
- Engineers : MFCC, Triphones, HMM, Network
- Phonetics : Formants, IPA, Gestures, Spectrograms
- Linguistics : Phonemes, Allophones, Morphemes -->


<font size='6'>Wave form </font>
Waveform is the acquisition of audio signal strenth with respect to time. For every audio signal we define the sampling rate and bits/channel. Audio is an analog signal we convert it to digial signal for further procesing. For that we sample the analog signal at a sampling rate and for each signal acquired we store that strength of the signal in bits. Higher the bitrate quality of the audio is more. higher the sample rate more samples are caputred ina particular time frame.

```
import librosa
import matplotlib.pyplot as plt
import librosa.display
audio_path = 'audio.wav' # path-to-your-audiofile
x , sr = librosa.load(audio_path)
```
Here, <b>x</b> is the amplitudes and <b>sr</b> is sampling rate of the audio file. We can also see the visulaisation of the waveform as well.

```
plt.figure(figsize=(16, 9))
librosa.display.waveplot(x, sr=sr)
plt.show()
```
![waveform image]({{ site.baseurl }}/assets/images/post_1/waveform.png)



[logo]: assets/images/spectrogram.png
<font size='6'>Fourier Transform</font>
Fourier transform is a frequency domain representation of the original signal. We decompose a signal into all the consisting pure frequency information. We try to convert time domain waveform to a magnitude as a function of frequency data. We call it Power Spectrum. While doing this transformation from time to frequency domain we lose out on temopral data of the signal.

![fourier image]({{ site.baseurl }}/assets/images/spectrogram.png)
<!-- summation of sin waves of different frequiences -->
<!-- - waveform to foruier transform is power spectrum -->

<!-- - <photo 1> - sum of signals -->
<!-- - <photo 2> - fft of same signal -->


<font size='6'>STFT - Short Time Fourier Transform</font>
- Calculate FFT at differnt intervals
- Fixed window which moves over the signal to calculte the FFT
- 3 Dimensions time x frequency x amplitude
- we do not lose the temporal data and can leverage to calculte the change of amplitude wrt time and frequency
- <photo1 > - STFT photo for same signal

![stft image]({{ site.baseurl }}/assets/images/spectrogram.png)

<font size='6'>MFCC - Mel Frequency Cepstral Coefficients</font>
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

![mfcc image]({{ site.baseurl }}/assets/images/spectrogram.png)
