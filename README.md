
# User Behavior Prediction Using LSTM

## Project Overview

This project focuses on predicting the next user interaction in an e-commerce environment using sequential user behavior data.

The main model used in the project is a Long Short-Term Memory (LSTM) neural network, which is designed to learn patterns from sequences of user interactions. Two traditional machine learning models, Logistic Regression and Decision Tree, are also implemented as baseline models for comparison.

The prediction task consists of predicting the next user interaction as one of three event types:

- `view`
- `cart`
- `purchase`

The implementation is provided in a Jupyter Notebook using Python and machine learning and deep learning libraries.

## Objective

The main objective of this project is to investigate whether previous user interactions within a user session can be used to predict the user's next action.

The project also investigates the effect of class imbalance on model performance by comparing the models before and after applying Random UnderSampling to the training data.

## Dataset

The project uses the **E-Commerce Behavior Data from Multi-Category Store** dataset.

The experiment uses the `2019-Oct.csv` file. Since the original October dataset contains more than 42 million records, the notebook processes **6,000,000 records** using chunks of **500,000 records**.

The dataset contains information about user interactions, including:

- event timestamp
- event type
- product ID
- category ID
- category code
- brand
- price
- user ID
- user session

The main event types used for prediction are:

- `view`
- `cart`
- `purchase`

The raw dataset is not included in the repository because of its large size.

## Technologies and Libraries

The project is implemented using:

- Python
- Jupyter Notebook
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- Imbalanced-learn
- TensorFlow / Keras

## Machine Learning Models

Three classification models are implemented and compared.

### Logistic Regression

Logistic Regression is used as a traditional machine learning baseline for predicting the next user interaction.

### Decision Tree

Decision Tree is used as a second baseline model for classifying the next user interaction.

### LSTM

Long Short-Term Memory (LSTM) is the main deep learning model used in the project.

The model uses sequences of **five previous user interaction events** to predict the following event.

## Main Steps

The main workflow of the project is:

1. Load 6,000,000 records from the October 2019 dataset using chunks.
2. Perform exploratory data analysis.
3. Check duplicate records and missing values.
4. Remove duplicate records and handle missing categorical values.
5. Convert timestamps and organize events chronologically within user sessions.
6. Encode the event types:
   - `view = 0`
   - `cart = 1`
   - `purchase = 2`
7. Create sequences of five events to predict the next event.
8. Sort the generated sequences chronologically.
9. Split the data into training and testing sets using an 80/20 chronological split.
10. Train Logistic Regression, Decision Tree, and LSTM models.
11. Evaluate the models using accuracy, precision, recall, F1-score, Macro F1-score, and confusion matrices.
12. Apply Random UnderSampling to balance the training data.
13. Retrain the models using the balanced training data.
14. Compare model performance before and after class balancing.

## Results

The dataset is highly imbalanced, with `view` representing the majority of user interactions.

Before balancing, the models achieve high overall accuracy, but the minority classes (`cart` and `purchase`) are more difficult to predict.

After applying Random UnderSampling to the training data, overall accuracy decreases, while the models achieve better recognition of the minority classes.

### Model Comparison

| Model | Accuracy Before Balancing | Accuracy After Balancing | Macro F1 Before | Macro F1 After |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.9541 | 0.9043 | 0.3614 | 0.5122 |
| Decision Tree | 0.9590 | 0.9176 | 0.4728 | 0.5540 |
| LSTM | 0.9591 | 0.9102 | 0.4767 | 0.5399 |

The results show that class balancing reduces overall accuracy, but improves
the models' ability to recognize the less frequent `cart` and `purchase`
interactions. Based on Macro F1, the Decision Tree achieves the highest
performance after balancing, followed by LSTM and Logistic Regression.

### Minority Class Recall

For the LSTM model, minority-class recall improves after balancing:

| Event | Before Balancing | After Balancing |
|---|---:|---:|
| `cart` | 0.12 | 0.52 |
| `purchase` | 0.16 | 0.52 |

These results show that Random UnderSampling improves the recognition of
the less frequent `cart` and `purchase` interactions, although this
improvement is accompanied by a decrease in overall accuracy.

### Visual Results

The repository can also include selected figures generated during the experiments.

### Shpërndarja e klasave para dhe pas balancimit

![Shpërndarja e klasave para dhe pas balancimit](figures/Figure_5_Class_Distribution_Before_After_Balancing.png)

### Krahasimi i modeleve para dhe pas balancimit

![Krahasimi i modeleve para dhe pas balancimit](figures/Figure_6_Final_Model_Comparison_Before_After_Balancing.png)

### Recall i klasave më pak të përfaqësuara

![Recall i klasave cart dhe purchase para dhe pas balancimit](figures/Figure_7_Minority_Class_Recall_Before_After_Balancing.png)

## How to Run
The complete implementation is available in the Jupyter Notebook:

**[Open the Jupyter Notebook](user_behavior_prediction_lstm.ipynb)**

### Using Kaggle

The notebook can be executed in a Kaggle environment.

1. Open the project notebook.
2. Add the **E-Commerce Behavior Data from Multi-Category Store** dataset.
3. Make sure the `2019-Oct.csv` file is available.
4. Run the notebook cells from top to bottom.

### Using Jupyter Notebook Locally

Clone the repository:

```bash
git clone <repository-url>
cd user-behavior-prediction-lstm
