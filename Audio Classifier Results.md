# Audio Classifier Accuracy Results

| Data type       | Specific Model                     | Specific Data Quality | Short description      | Accuracies across all genres | Longer description/Notes                       |
| --------------- | ---------------------------------- | --------------------- | ---------------------- | ---------------------------- | ---------------------------------------------- |
| Raw waveform    | SVC                                | N/A                   | Most ineffective model | 16%                          | First model we created was purposely bad       |
| Raw waveform    | Multi-layered Dense Neural Network | N/A                   | Most ineffective model | 6.50%                        | First model we created was purposely bad       |
| Mel-Spectrogram | asdf                               | N/A                   | asdf                   | 33                           | asdf                                           |
| Multiple        | Ensemble (xgb, svm, cnn)           | N/A                   | Effective model        | 90.30%                       | Pre-built online model with very high accuracy |
| Chromogram      | Chromogram-Only CNN                | N/A                   | Reletively ineffective | 26%                          | Only takes Chromograms, it is not optimised.   |
