# Traffic Crash Severity Prediction
## Project Overview

This project focuses on predicting whether a traffic crash resulted in a fatality or suspected serious injury using machine learning. The goal is to support road safety analysis by identifying high-risk crashes, particularly those with severe outcomes, using historical crash data.

The model was developed using logistic regression and carefully designed to handle imbalanced data, missing values, and mixed data types, which are common challenges in real-world traffic datasets.

## Dataset

- File: traffic_case_study.xlsx

- Source: Pennsylvania Department of Transportation

- Observations: 600 crash records

- Features: 26 variables

- Target Variable: FATAL_OR_SUSP_SERIOUS_INJ

     0 – No fatal or suspected serious injury

     1 – At least one fatal or suspected serious injury

- A detailed explanation of all features is provided in:

- Traffic case study feature explanation.pdf

## Objective

To build a classification model that can accurately identify crashes likely to result in severe or fatal injuries, with particular emphasis on minimizing missed severe cases.

## Data Preprocessing

Data preprocessing was implemented using scikit-learn Pipelines and a ColumnTransformer to ensure reproducibility and prevent data leakage.

### Numerical Features

- Missing values imputed using the median

- Scaled using Min-Max Scaling

- Categorical Features

- Missing values imputed using the most frequent value

- Encoded using One-Hot Encoding

### Binary Features

- Missing values imputed using the most frequent value

- Left unscaled

### Handling Class Imbalance (SMOTE)

- The dataset is highly imbalanced, with severe crashes being much rarer than non-severe ones. To address this, SMOTE (Synthetic Minority Over-sampling Technique) was applied only to the training data.

- SMOTE generates synthetic examples of the minority class, allowing the model to better learn patterns associated with severe crashes instead of defaulting to the majority class.

### Model

- Algorithm: Logistic Regression

- Solver: liblinear

- Maximum Iterations: 1000

- Logistic regression was chosen for its interpretability and suitability for binary classification problems, particularly in safety-critical contexts.

### Hyperparameter Tuning

- Hyperparameter tuning was performed to improve model performance, especially for the minority (severe crash) class. Key parameters such as regularization strength and class weighting were optimized using cross-validation.

- The tuning process prioritized the F1-score to ensure a balanced trade-off between detecting severe crashes and limiting false alarms.

### Evaluation Metric

- Primary Metric: F1-score

- The F1-score was selected as the primary evaluation metric due to the strong class imbalance in the dataset.

#### F1-score Explained

- Instead of simply measuring how often the model is correct, the F1-score focuses on how well the model handles important mistakes.

- In simple terms, it measures:

   How many serious crashes the model correctly identifies, and

   How often it avoids incorrectly labeling non-serious crashes as severe

- This balance is important because:

   Missing a serious crash can have serious real-world consequences

   Predicting too many false severe crashes can reduce trust in the model

- The F1-score ensures the model remains both sensitive to dangerous crashes and reasonable in its predictions.

##### Optimized Model Results
Classification Report
              precision    recall  f1-score   support

           0       0.98      0.90      0.94       143
           1       0.25      0.71      0.37         7

    accuracy                           0.89       150
   macro avg       0.62      0.80      0.65       150
weighted avg       0.95      0.89      0.91       150

Confusion Matrix
[[128  15]
 [  2   5]]

### Results Interpretation

- After applying SMOTE and hyperparameter tuning:

   The model correctly identified 5 out of 7 severe crashes

   Only 2 severe crashes were missed

   Some non-severe crashes were incorrectly flagged as severe, which was an acceptable trade-off given the high cost of missing serious outcomes

   The F1-score for severe crashes improved to 0.37, demonstrating a meaningful improvement in the model’s ability to detect high-risk crashes compared to earlier versions.

### Limitations

- Severe crashes remain rare, limiting model learning despite oversampling

- Logistic regression may not capture complex, non-linear relationships

- Performance is sensitive to feature quality and class imbalance

### Future Improvements

- Explore tree-based models such as Random Forest or XGBoost

- Further tune class weighting strategies

- Perform feature selection and interaction analysis

- Increase dataset size if additional data becomes available

### Conclusion

This project demonstrates a complete and realistic machine learning workflow for predicting severe traffic crashes. By addressing class imbalance with SMOTE, tuning hyperparameters, and prioritizing the F1-score, the final model focuses on identifying high-risk outcomes rather than achieving misleadingly high accuracy, making it more suitable for real-world safety applications.