[Reference Link](https://dcase.community/challenge2025/task-low-complexity-acoustic-scene-classification-with-device-information)
### Info of Dataset

- Data is based in 12 European cities. 
- Data is taken from 10 different acoustic scenes using 4 different devices
- Synthetic data for 11 mobile devices was created based on the original recordings
- Out 12 cities only 2 are in evaluation set
- The 4 devices used are:
	- Device A: a Soundman OKM II Klassik/studio A3, an electret binaural microphone, and a Zoom F8 audio recorder using a 48kHz sampling rate and 24-bit resolution
	- Device B: Samsung Galaxy S7
	- Device C: iPhone SE
	- Device D: GoPro Hero5 Session
- Cities name are: Amsterdam, Barcelona, Helsinki, Lisbon, London, Lyon, Madrid, Milan, Prague, Paris, Stockholm, and Vienna.

[^1]: Note: 10 mobile devices S1-S10 are simulated using the audio recorded with device A, impulse responses recorded with real devices, and additional dynamic range compression, in order to simulate realistic recordings. [Learn more](https://chatgpt.com/share/6937e104-dc8c-8009-842d-860fc47e7846).  A recording from device A is processed through convolution with the selected impulse response, then processed with a selected set of parameters for dynamic range compression (device-specific).

The complete development dataset comprises 40 hours of data from device A and smaller amounts from the other devices

We are only allowed to use the subset specified in the [Task Setup section](https://dcase.community/challenge2025/task-low-complexity-acoustic-scene-classification-with-device-information#task-setup) below. Audio is provided in a single-channel, 44.1 kHz, 24-bit format.

Acoustic scenes (10):

- Airport - `airport`
- Indoor shopping mall - `shopping_mall`
- Metro station - `metro_station`
- Pedestrian street - `street_pedestrian`
- Public square - `public_square`
- Street with medium level of traffic - `street_traffic`
- Travelling by a tram - `tram`
- Travelling by a bus - `bus`
- Travelling by an underground metro - `metro`
- Urban park - `park`

## Development Dataset

DCASE 2025 development set reuses the 25% train split and the test split of [Task 1](https://dcase.community/challenge2024/task-data-efficient-low-complexity-acoustic-scene-classification#development-dataset) in the DCASE Challenge 2024.

It contains recordings from **10 cities and 9 devices: 3 real devices (A, B, and C) and 6 simulated devices (S1-S6). Data from devices B, C, and S1-S6 consists of randomly selected segments from the simultaneous recordings;** therefore, all overlap with the data from device A, but not necessarily with each other. The total amount of audio in this year's training set is around **18 hours.**


## Evaluation Dataset

The evaluation dataset is used for ranking submissions.
- Data based in 12 cities
- 10 acoustic scenes(including devices A,B,C,S1-S3 in the development dataset) marked with respective device IDs
- New devices include: Device D and simulated devices S7-S10, marked with 'unknown' device IDs.
- The evaluation data contains approximately 37 hours of audio recorded at different locations than the development data
- City information is _not_ provided here

#### Solution by Ranker 1:
- [Inference Code](https://github.com/turquenite/malach25_task1_inference.git)
- [[DCASE2023_Karasin_54_t1.pdf]]

#### Baseline Solution:
- [Github](https://github.com/CPJKU/dcase2025_task1_baseline.git)
- Highlights: 
	- The training loop is implemented using [PyTorch](https://pytorch.org/) and [PyTorch Lightning](https://lightning.ai/).
    - Logging is implemented using [Weights and Biases](https://wandb.ai/site).
	- The neural network architecture is a simplified version of [CP-Mobile](https://dcase.community/documents/workshop2023/proceedings/DCASE2023Workshop_Schmid_1.pdf), the architecture used in the top-ranked system of Task 1 in the DCASE 2023 challenge.
	- The model has 61,148 parameters and consumes 29.42 million MACs for the inference of a 1-second audio snippet. MACs are counted using [torchinfo](https://github.com/TylerYep/torchinfo). The model's test step converts model parameters to 16-bit floats to meet the memory complexity constraint of 128 kB for model parameters.
	- The baseline implements simple data augmentation mechanisms: time rolling of the waveform and masking of frequency bins and time frames.
	- To enhance the generalization across different recording devices, the baseline implements [Frequency-MixStyle](https://dcase.community/documents/workshop2022/proceedings/DCASE2022Workshop_Schmid_27.pdf).


