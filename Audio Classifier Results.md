# Audio Classifier Accuracy Results

## Feature Analysis

Statistics from features:

- 309 features (individual data points) examined
- Stacked Ensembled based off SVM, 1D CNN, Dense NN, XGBoost and Random Forest
- The test-train-split has test_size = 0.2 (80/20) and random_state = 42

Results from features:

| Genre(s)          | Length     | SVM   | 1D CNN | Dense NN | XGBoost | Random Forest | Soft Voting Ensemble | Hard Voting Ensemble | Weighted Voting Ensemble | Stacked Ensemble |
| ----------------- | ---------- | ----- | ------ | -------- | ------- | ------------- | -------------------- | -------------------- | ------------------------ | ---------------- |
| All ten genres    | 3 Seconds  | 92.3% | 91.0%  | 91.5%    | 95.0%   | 89.4%         | 95.5%                | 95.1%                | 93.8%                    | 95.4%            |
| All ten genres    | 30 Seconds | 73.0% | 73.0%  | 56.0%    | 73.0%   | 74.0%         | 79.5%                | 75.0%                | 75.5%                    | 79.5%            |
| Classical + Metal | 3 Seconds  | 98.0% | 99.8%  | 99.9%    | 99.5%   | 99.8%         | 99.8%                | 99.8%                | 99.8%                    | 99.8%            |
| Classical + Metal | 30 Seconds | 100%  | 100%   | 100%     | 100%    | 100%          | 100%                 | 100%                 | 100%                     | 100%             |
| Disco + Pop       | 3 Seconds  | 98.3% | 97.8%  | 87.5%    | 98.0%   | 98.0%         | 99.3%                | 99.0%                | 98.5%                    | 99.3%            |
| Disco + Pop       | 30 Seconds | 95.0% | 97.5%  | 87.5%    | 92.5%   | 97.5%         | 95.0%                | 95.0%                | 97.5%                    | 95.0%            |

## RNN (Recurrent Neural Network) Analysis

Statistics from RNN:

- 20 epochs
- Input shape: 1300, 13
- Layers of the RNN:
  - Masking(mask_value=0.0, input_shape=(1300, 13))
  - LSTM(128, return_sequences=True)
  - Dropout(0.2)
  - LSTM(64, return_sequences=False)
  - Dropout(0.2)
  - Dense(64, activation='relu')
  - Dense(len(GENRES), activation='softmax')

Results from RNN:

| Genre(s)          | Length     | Final accuracy |
| ----------------- | ---------- | -------------- |
| All ten genres    | 3 Seconds  | 88.61%         |
| All ten genres    | 5 Seconds  | 80.37%         |
| All ten genres    | 30 Seconds | 84.00%         |
| Classical + Metal | 3 Seconds  | 99.94%         |
| Classical + Metal | 30 Seconds | 100%           |
| Disco + Pop       | 3 Seconds  | 99.56%         |
| Disco + Pop       | 30 Seconds | 100%           |
