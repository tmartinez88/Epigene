# Epigene
## A Spectral Filter VST built with Juce.

## Download

You will find the built VST in the Plugin folder

### Description

Epigene is an FFT based audio filtering effect. The plugin allows for a bin-wise attenuation of spectra. It uses the overlap-add processing technique translated from Bela Online Course Lecture 18 taught by Dr. Andrew McPherson at The Queen Mary University of London. You can find the original lecture notes and video here, which includes an expert explanation on how the time to frequency domain, and inverse algorithm works: https://github.com/BelaPlatform/bela-online-course/tree/master/lectures/lecture-18

The translated code is provided here in the Juce audio development framework, with the added functionality of stereo input processing and bin-wise filtering (the Bela Lecture provides a more complex phase vocoding algorithm and I've opted to illustrate a more straight forward example of frequency domain processing). Why Juce? Juce allows us to build our plugin for different hosts such as DAWs, game engines (Unity), standalone applications, and through a relatively painless transpiling process, in Web Assembly for use on the World Wide Web. It is a very well documented and supported tool with a large and active user community.

### Inspiration

Having developed a number of spectral processing techniques for software pieces and music in the past, I was hoping to bring some of that sonic material practice to the web where my more recent interests lie. I had up until then built my algorithms in the programming language Max (www.cycling74.com), and because of that there wasn't a clear path for me to embed those projects in a web safe/Javascript environment. With that in mind, I began to search for implementations of FFT processing in the standard Web Audio API and web technologies more generally. 

There have been several successful attempts at providing methods for spectral processing on the web. Sebastian Piquemal's paulstretch.js (2014, https://github.com/sebpiq/paulstretch.js) repo provided cloner's with a phase-vocoder time stretching algorithm. Additionally Nevo Segal's fft.js (2017, https://github.com/nevosegal/fftjs) and Oleksii Trekhleb's "javascript-algorithms" repo (2019, https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/math/fourier-transform) brilliantly abstracted the forward and inverse FFT math in a library that would allow programmers to use in a their own web based audio environments. 

And though these libraries provided useful tools for solving the STFT of an incoming audio signal, nothing I found provided a simple and educational top to bottom (that is audio input to audio output) method for Cooley-Tukey spectral processing that could be used in a plug and play style on the web, much less additional audio hosts. Additionally, nothing I found was built to be used with the Web Audio API in mind. The Audio Working Group at the W3C, stewards of the Web Audio API, address the need for an official inverse FFT AudioNode on a number of occasions (here https://github.com/WebAudio/web-audio-api/issues/248, and here https://github.com/WebAudio/web-audio-api/issues/468). These discussions reach a kind of consensus that recognizes the existence of Javascript libraries which could be implemented in an AudioWorker (now Audio Worklets) node, a JS scripting environment that enables custom sample level DSP programming. 

Current thinking and approaches for IFFT processing includes that Audio Worklet method, which of course necessitates the use of external complex math JS libraries, but also includes the use of Web Assembly modules made compatible for use in the Web Audio audio graph (https://madewithwebassembly.com/showcase/web-audio-modules/). I've opted for the second method using Web Assembly, as code made in C++ and in the Juce framework gives us additional options for export (vsts, Unity plugins, etc...). I have attempted to provide code in a vanilla state, so that it may be used as a boiler plate example for others to experiment within the frequency domain. In open-sourcing this repo I hope that others may find the joy in spectral audio processing and build processors that were hitherto incompatible or scarce in existing web and interactive technologies.
