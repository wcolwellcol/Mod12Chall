# Module 12 Report Template

## Overview of the Analysis

In this section, describe the analysis you completed for the machine learning models used in this Challenge. This might include:

The purpose of this exercise is to identify the creditowrthiness of borrowers, and, thus, loans that are at a high risk of defaulting. For each loan, information is given on the loan size, interest rate, borrower's income, borrower's DTI ratio, borrower's number of accounts, derogatory marks, and total debt. This information is all taken together to produce a binary "loan status" prediction of either 0 (healthy) or 1 (unhealthy). 

The main problem posed by this data set was imbalance. Specifically, there are significantly more healthy loans (75036) than unhealthy loans (2500). Initially, I ran a model in which the imbalance was not dealt with by any techniques such as undersampling or over sampling. The standard machine learning pipeline was followed, albeit at a rudimentary level, and is described bloew:

Model 1:
The prediction column and features columns were separated as X and y.
`train_test_split` was utilized to create X training, testing and y training, testing groups.
The `LogisticRegression` module from SKLearn was utilized to create a logistic regression model intended for binary prediction.
The model was then fit onto the training data, and fed X_testing data to predict y.

Model 2:
The same process as Model 1 was followed except for the fact that unhealthy loans were oversampled utilizing the `RandomOverSampler` module from the imbalanced-learn library. Oversampling made more sense as a technique to use than undersampling given the size of our datasett (< 3k in minority group). The model was then fit on this resampled data and the same process utilized in Model 1 was followed from there on out.


## Results

Below are the balanced accuracies, precision and recall scores for each of my models. Note the improved performance for Model 2 which utilized oversampled data.

* Machine Learning Model 1:
  * Balanced Accuracy: 0.9520479254722232
  * Performance on 0s:
    * Precision: 1.00 
    * Recall: 0.99 
  * Performance on 1s:
    * Precision: .85
    * Recall: .91


* Machine Learning Model 2:
  * Balanced Accuracy: 0.9936781215845847
  * Performance on 0s:
    * Precision: 1.00 
    * Recall: 0.99 
  * Performance on 1s:
    * Precision: .84
    * Recall: .99


## Summary

Summarize the results of the machine learning models, and include a recommendation on the model to use, if any. For example:
* Which one seems to perform best? How do you know it performs best?
* Does performance depend on the problem we are trying to solve? (For example, is it more important to predict the `1`'s, or predict the `0`'s? )

Summarizing the results of these models requires us to revisit the purpose of this exercise. In this particular use case, we are using machine learning to predict whether a loan has a high risk of defaulting or not. It is safe to assume that whoever utilizes this model would be far more concerned with defaults compared to healthy loans. In other words, falsely classifying a healthy loan as an unhealthy one is a less consequential mistake than falsely classifying an unhealthy loan as a healthy one. I mainly care about minimizing false negatives. For this, we must look at the recall score for the 1s group.

The second model which was fit on resampled data performed better according to the recall score for 1s. The second model has a recall of .99 for 1s, whereas the first model had a recall of .91. This does come with a marginal decrease in precision, but I am less sensitive to precision in this use case. Overall, 99/100 loans faulty loans being correctly identified seems to be strong enough to recommend implementing this model as part of the risk identification ecosystem. I would not solely rely on this model, however, if 1 defaulting loan would pose a substantial risk to the business.
