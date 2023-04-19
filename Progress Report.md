# Progress Report

## Background Information
Music source separation is the task of decomposing music into its individual components, most commonly `bass`, `drums`, `vocals`, and `other`. Whether it is done computationally or algorithmically, a necessary subtask is evaluation of separation quality. When training a deep net for music source separation, for example, we need to know how close the source separated audio is to the expected outcome.

The most ideal evaluation method would be human perception, or having a large group of people listen to the source separated audio and give it a rating of some kind. This, however, would be extremely time consuming and expensive. Instead, researchers opt for objective evaluation methods, with the most widely used metric being *signal-to-distortion ratio* (SDR) [4].

SDR is a fickle metric that can output significantly different scores depending on a variety of factors. For this project I focus on the aspect of phase and how it can affect an audio signal's SDR.

## Project Overview
I have selected a 7-second excerpt of a song from the MUSDB18 dataset [5]. I source separated this excerpt using three prominent models: Demucs [1], Hybrid Demucs (MDX) [2], and Spleeter [3]. For these experiments I only use the `bass` stem.

I removed the phase data from these separated signals and replaced it with five different phase data:
1. The ground-truth bass stem
2. The original mix
3. Phase estimated by the [Griffin-Lim phase reconstruction algorithm](https://paperswithcode.com/method/griffin-lim-algorithm)
4. Phase of a MIDI replication of the ground-truth bass stem
5. No phase data

I calculated the SDR of the resulting 15 stems using the implementation of scale-invariant SDR provided in the [NUSSL library](https://source-separation.github.io/tutorial/basics/evaluation.html). I also gathered ratings of audio quality from a few listeners. Listeners were asked to rate the recording quality of the 15 stems on a scale of 1 (Bad) to 5 (Excellent). Although the pool of respondents is not large enough to be more than anecdotal, it still could be helpful in identifying the discrepancy between objective and subjective evaluations of audio.

Code of these experiments can be found in the Google CoLab notebook here: https://colab.research.google.com/drive/18eQLeYDTLCn7xM6yV6keF5SnjPe7npMs?usp=sharing.

Within the notebook, I explain the steps I took to create the audio data. A copy of the notebook is also available in this repository, but it may not be up-to-date with the notebook hosted in CoLab.

## References
1. Défossez, A., Usunier, N., Bottou, L., and Bach, F. [Music source separation in the waveform domain](https://arxiv.org/pdf/1911.13254.pdf). arXiv preprint arXiv:1911.13254 (2019).
2. Défossez, A. [Hybrid spectrogram and waveform source separation](https://arxiv.org/pdf/2111.03600.pdf). arXiv preprint arXiv:2111.03600 (2021).
3. Hennequin, R., Khlif, A., Voituret, F., and Moussallam, M. [Spleeter: a fast and efficient music source separation tool with pre-trained models](https://joss.theoj.org/papers/10.21105/joss.02154.pdf). Journal of Open Source Software 5, 50 (2020), 2154.
4. Le Roux, J., Wisdom, S., Erdogan, H., & Hershey, J. R. (2019, May). [SDR–half-baked or well done?](https://arxiv.org/pdf/1811.02508.pdf). In ICASSP 2019-2019 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP) (pp. 626-630). IEEE.
5. Rafii, Z., Liutkus, A., Stöter, F. R., Mimilakis, S. I., & Bittner, R. (2017). [The MUSDB18 corpus for music separation](https://sigsep.github.io/datasets/musdb.html#sisec-2018-evaluation-campaign).
