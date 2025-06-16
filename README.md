# GTZAN Music Classifier Task

## What is GTZAN?

The GTZAN dataset is a foundational resource in the field of music information retrieval and machine learning. It contains 1,000 audio tracks, each lasting 30 seconds, evenly distributed across 10 distinct music genres: blues, classical, country, disco, hip-hop, jazz, metal, pop, reggae, and rock. Each genre is represented by 100 tracks, providing a balanced dataset for experimentation. The GTZAN challenge refers to the task of developing and evaluating algorithms that can automatically classify these audio tracks into their correct genres. This challenge serves as a standard benchmark for researchers to test new music classification methods, compare algorithmic performance, and advance the state of the art in audio analysis and genre recognition. Despite its popularity, the GTZAN dataset also presents certain challenges, such as potential duplicates and recording artifacts, which make it a realistic and instructive testbed for robust machine learning approaches.

## Background on this GTZAN task

In one of the modules for my university course, myself and others worked on creating a music classifier, based on and trained on the famous GTZAN dataset. Although we were able to produce interesting results, a combination of working on additional modules, as well as additional factors, meant that I felt limited by time constraints, and I was not able to take the task as far as I had initially wanted to go, or expand it into as many areas as I'd previously hoped or expected, thus my return to looking at it.

## How to analyze and train the models

The two methods that I've chosen to go about finding features for this include:

1. Grab a large series of features from the .wav file, using the librosa Python library, and then passing these features directly into a series of CNNs and ensembles
2. Passing the .wav files through an RNN, a type of neural network that's designed to handle sequential data

In addition to this, I've chosen to separate the way that we work with data in a couple of ways:

1. Comparison of the full 30-second audio with segmented 3-second audio (each audio clip separated into 10 separate 3-second clips)
2. Three separate comparisons of different music genres:
   1. All 10 genres
   2. Classical vs Metal (hoping to be easier due to sharp contrast in sound difference)
   3. Disco vs Pop (hoping to be harder due to low contrast in sound difference)

The hope with these comparisons is that we would be able to compare and contrast the different methods that were used for creating the features overall, thus leading to a generalized model of how to work with audio.

Although I could have easily expanded the way that I experiment with the audio in a large number of ways, I did not want this project to go on forever, and thus I decided to present similar default values across all comparisons. For example, keeping the sr (sample rate) at a standard 22,050, keeping random_state=42 for all train-test-splits, as well as having the same design for the CNNs and RNNs throughout.

## Feature Analysis

### Findings from the features analysis

- Classical + Metal genre comparisons were much more accurate compared to Disco + Pop, as well as all ten genres, across both 3-second and 30-second plays
- Disco + Pop was more accurate than all ten genres
- 3-second plays for all ten genres were significantly more accurate than 30-second plays
- 3-second plays for Disco + Pop were slightly more accurate than 30-second plays
- 30-second plays for Classical + Metal were 100% accuracy, slightly higher accuracy than the 3-second plays
- All ensembles were generally more accurate than the individual classifiers
- In the vast majority of cases, the top ensembles were the soft voting and stack ensembles, with the weighted voting only being the strongest for Disco + Pop 30-seconds.

### Final thoughts on feature analysis

Although studying the features for these ensembles did very well in general, and particularly well with respect to comparing different genres, they still have issues which need addressing.

I was correct in predicting an increased accuracy for Classical + Metal, compared to Disco + Pop, as well as to all ten genres. This is because Classical + Metal are, by genre comparison, so different with respect to the sounds that they produce that it should be somewhat easy to make out that these would be different. By comparison, although I was expecting Disco + Pop to do worse in general because the way that they sound is quite similar in a lot of ways, I was pleasantly surprised by the accuracy that was able to be generated.

In my opinion, there are three primary questions that need to be asked with respect to feature analysis if we want to attempt a higher accuracy in the future:

1. Are 3 or 30-second sounds the only, and most accurate method of working with this audio? We want to try and combine a high number of examples with a high quality of data, attempting to find a sweet spot between both of these. If we increased the number of segments per song to an extreme amount, e.g. 100 segments per song, we would end up with 100 times more pieces of data, but each sound clip would only be 0.3 seconds long, which may be incredibly hard to work with, and to get more accurate. On the other hand, do we want to work with audio samples that are just 30 seconds long, but with only 100 sounds per sample?
2. Can we adjust the parameters of our various classifiers and neural networks in order to create more accurate results? Parameters such as the ratio for the test-train-split and the random state, or the structure of the neural networks, adding more or fewer layers, may make a difference. The attempt towards increasing accuracy across these fronts is an inconceivably difficult and repetitive task, thus the fact that I stuck with what I had.
3. Which of the 309 features that were used within the classifier task were more, or less relevant to producing higher quality results, and which ones may be worth keeping or removing? There are some classifiers which attempt to adjust the importance or unimportance of various features, however to know which parameters weigh more-or-less heavily on the final outcome, one may have to either adjust these manually, dropping various features, or otherwise use additional frameworks and libraries in order to find the appropriate cuts to make.

## RNN (Recurrent Neural Network)

### Findings from the RNN

- Accuracy from comparing both of the two genres was significantly higher than the accuracy from comparing all ten genres
- For Classical + Metal and Disco + Pop, the 30-second analysis both had 100% accuracy, whilst the 3-second analysis had close to 100% accuracy, either underscoring the effectiveness of using the full 30-second clips from the audio, or otherwise highlighting in general the effectiveness and accuracies of both, no matter the lengths of the audio
- Classical + Metal and Disco + Pop had similar accuracies to one another, compared to the feature analysis, possibly underlining the strong ability of RNNs to differentiate limited genres, even if they are potentially of a similar nature to the human ear
- Looking at all ten genres, the RNN did better on the 30-second audio clips, but worse on the 3-second audio clips, when compared to the feature analysis

### Final thoughts on the RNN

Although feature analysis and CNNs represent a very common way of genre analysis, recurrent neural networks are another major tool that can be utilized in this task. Recurrent neural networks are a class of neural networks that allow for previous outputs to be used as inputs, thus allowing for something like memory to occur and exist within the neural network itself. They are able to study audio in an entirely different manner to the CNN, and can thus allow for a more unique and interesting way to study music. Feature analysis may be good at picking up on one feature, and not so good on another, and vice versa, thus highlighting the potential effectiveness of RNNs.

## Additional notes

There are a variety of methods which could have potentially been implemented in order to increase the accuracy of these results. Using a larger dataset, as one example, would have allowed for a larger pool of data to work on. As it is, 100 30-second clips for ten genres is not all that much, and certainly not much if you're hoping to get highly accurate results. In addition to this, if we were to increase or adjust the number of songs within our dataset, would we have to include more genres? In addition, since some songs actually overlap different genres, or combine them, in future experiments like this, how can we work with these things in order to increase the accuracy of our classifiers? Some songs may also have similar sounds to one another, thus confusing whatever classifier/neural network is used to train on it. Say for example a section of a song contains silence, or is quieter. This may lead to accuracy issues later on down the line, as a new song with a period of silence may be interpreted as the wrong genre.

My suspicion with some of the models peaking at particular percentages, or being similar percentages across the board for the same number of genres, is that there are one or two outlier songs which may on the one hand belong to the genre, but on the other hand may be difficult to classify for the model that's being used, or otherwise may present challenges in other ways, thus leading to specific outlier cases. Otherwise, the ensembles present in the feature analysis would have perhaps reached 100% on a number of the songs overall.

Other methods of classifying music exist. One method includes using librosa again, but this time converting the chromagrams/mel-spectrograms/spectrograms into images, and then passing those images through a 2D CNN. However, this method is significantly more computationally expensive, as you're having to create 1,000s of images for all the songs, and then for all the different conversions, and then again for whether it'll be 3 or 30 seconds. Secondly, there is the potential to lose a certain amount of the detail when converting the song into an image - detail which could have been used for more data for the CNN. Finally, converting it into an image means that you use a lot more space on your computer, and thus causing a storage issue.

One final note: much of the reason that some of this code looks messy/unstructured is because it's a loose holdover from previous code from the AI Systems Implementation assignment, and I didn't necessarily want to re-write all the code that other people had produced in its entirety, although I did significantly edit it.
