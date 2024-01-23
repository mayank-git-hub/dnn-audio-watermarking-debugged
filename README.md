# I have solved the bugs present in the code to make it runnable.

A working encoder-decoder code is available in run.ipynb
I have made some assumptions in the code.

1. Repeated the message to match it to the required shape as specified in the config file.
2. used euclidean distance to find closest message from the Pool
   

# DNN-audio-watermarking
We implemented a robust DNN-based audio watermarking system. It contains two neural networks. One for embedding the watermark (Embedder), and the other for detecting watermarks in watermarked audio signals (Detector).\
The system has been trained against following watermarking attacks:
- Additive noise
- Low pass filtering (cut-off frequency at 4kHz)
- Sample suppression (setting a random set of 1000 samples to zero) \

This work has been published in the DSP Journal: https://www.sciencedirect.com/science/article/abs/pii/S1051200421004206.

You can use our pretrained models with the provided samples.
For start, restore the embedder and the detector models:
```
from evaluation import restore_model
embedder = restore_model("embedder_model")
detector = restore_model("detector_model")
```
To test embedding process call:
```
import librosa
from main import embed
signal, sr = librosa.load('samples/example1.wav', sr=16000)
watermarked_signal = embed(embedder, signal)
```
To test detection call:
```
from main import detect
watermark = detect(detector, watermarked_signal)
```
To train your own model using this architecture, you can use provided functions stored in python files like models, train, etc.
## Prerequisites
- tensorflow==2.4.1
- librosa==0.7.2
- pypesq==1.2.4
