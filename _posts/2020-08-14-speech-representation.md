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


<font size='6'> Fast Fourier Transform</font>
Fourier transform is a frequency domain representation of the time domain signal. We decompose a signal into all the consisting pure frequency information. Using Fourier transform we can represent the time-domain signal as superimposition of sinusoids of varying magnitudes, frequencies and phase offsets. We convert time domain waveform to a magnitude as a function of frequency data. We call it Power Spectrum. While doing this transformation from time to frequency domain we lose out on temopral data of the signal. The only differenct in Fourier Transform and Fast Fourier Transform is Fast Fourier Transform is done on continous signal and Fast Fourier Transform is done on discrete time signal.

```
import numpy as np
 
fft = np.fft.fft(x)
mag_fft = np.abs(fft)
freq_fft = np.linspace(0, sr, len(mag_fft))
# print (freq_fft)
plt.plot(freq_fft, mag_fft)
plt.xlabel("frequency")
plt.ylabel("magnitude")
plt.show()
```

![fourier image]({{ site.baseurl }}/assets/images/post_1/fft.png)


<font size='6'>STFT - Short Time Fourier Transform</font>
As we know the we lose out on temporal relation in FFT, to retain the temporal information we can do the <b>Short time Fourier Transform </b> of the signal. We take small time interval, which we call as time frame. STFT is FFT of all succesive time frames. When we have the time interval equal to length of signal it is equivalent to having the FFT of the signal. The advantage of STFT is we do not lose the temporal data and can leverage to calculte the change of amplitude wrt time and frequency. Also we do not lose out on phase information.

<b>Spectrogram</b> on other hand is the intensity of frequencies over time. We calculate Spectrogram by taking square of magnitude of STFT.

```
X = librosa.stft(x)
X_spectrogram = librosa.amplitude_to_db(abs(X))
plt.figure(figsize=(14, 5))
librosa.display.specshow(X_spectrogram, sr=sr, hop_length=512, x_axis='time', y_axis='hz')
plt.colorbar()
plt.show()
```

![stft image]({{ site.baseurl }}/assets/images/post_1/stft.png)




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

![mfcc image]({{ site.baseurl }}/assets/images/post_1/spectrogram.png)
