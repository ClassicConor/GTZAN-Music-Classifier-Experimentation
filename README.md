# GTZAN Music Classifier Task

## What is GTZAN?

The GTZAN dataset is a foundational resource in the field of music information retrieval and machine learning. It contains 1,000 audio tracks, each lasting 30 seconds, evenly distributed across 10 distinct music genres: blues, classical, country, disco, hip-hop, jazz, metal, pop, reggae, and rock. Each genre is represented by 100 tracks, providing a balanced dataset for experimentation. The GTZAN challenge refers to the task of developing and evaluating algorithms that can automatically classify these audio tracks into their correct genres. This challenge serves as a standard benchmark for researchers to test new music classification methods, compare algorithmic performance, and advance the state of the art in audio analysis and genre recognition. Despite its popularity, the GTZAN dataset also presents certain challenges, such as potential duplicates and recording artifacts, which make it a realistic and instructive testbed for robust machine learning approaches.

## Background on this GTZAN task

On one of the modules for my university course, myself and others worked on creating a music classifier, based and trained on the famous GTZAN dataset. Although we were able to produce interesting results, a combination of working on additional modules, as well as additional factors meant that I felt limited by time constraints, and I was not able to take the task as far as I had initially wanted to go, or expand it into as many areas as I'd previously hoped or expected, thus my return to looking at it.

## How to analyse and train the music

There are a number of ways to work with gathering information from it. These methods include:

1. Converting the .wav files to different images representing different types of spectras, then passing the images through a CNN. The different types of images include, but are not limited to:
   - Chromagram
   - Spectrogram
   - Mel-Spectrogram
   - Tempogram
2. Convert the .wav file to different spectral types, and then directly feed them into the CNN, skipping the image
3. Pass the .wav files through a RNN (Recurrent Neural Network) - a type of neural network that's designed to handle sequential data, including audio
4. Create an ensemble, combining multiple data points, in order to produce a powerfully loaded final model
