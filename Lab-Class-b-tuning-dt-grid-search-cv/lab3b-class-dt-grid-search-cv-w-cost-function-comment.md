The most common standard measures (also called _scores_) for the prediction performance of a binary classifier are summarised in the document `machineLearning-classification-II.pdf`, pages 59-64.

Those measures are obtained using various combinations of the counts of correct and wrong predictions of examples of the two classes (the elements of the _confusion matrix_).
This means that the value produced by a good prediction and the cost implied by a wrong prediction have all the same "weight", regardless the class.

In cases where the problem at hand implies a ***different value or cost*** 
for the different cases of good and wrong predictions we can design a customised
scoring strategy. 

In `lab3b` we design this customised scoring strategy. The problem is to forecast if a customer of the bank asking for a credit card will be able to repay the credits obtained or will **go bankrupt**. The forecast will be made by training and optimising a classifier on the basis of the predicting attributes available. 

**Optimising** a classifier means _find the set of hyperparameters that **maximises** some score_

The exercise requires the training with parameter optimisation optimisation of a classifier using five different score function, the four classical ones, collected in the list of cell number 13, plus a _customised_ one.

The customised score is built in three steps

1. assign a _relative value_ to each of the four elements of the confusion matrix and generate a *cost matrix*
2. define a _score function_ named `cost_based_scorer` that multiplies, element by element, the cost matrix by the confusion matrix, and sums all the elements
3. using the `make_scorer` function of sklearn generate a `custom_scorer` that can be used by the GridSearchCV in the same way as it uses the standard scorers.

The *Loop on scores* implements the five experiments, showing that depending on the score used for the optimisation we obtain a different configuration of the hyperparameters of the classifier.

In each execution of the loop we do the following operations:

1. optimize the classifier model for the current scorer with `GridSearchCV`
2. test the model and show the classification report
2. compute the *value* of the current model multiplying element by element the _confusion matrix_ by the _cost matrix_ (the multiplying factor is included only as an example of real use if we have an hypotesis of the number of classification per day that we should expect)
3. show the confusion matrix

It should not be surprising that the maximum value is obtained by the model optimised with the custom scorer. 

The second maximum value is obtained by the model optimised with `recall_macro`, this is also not surprising, because recall_macro encourages solutions giving a smaller number of errors on the minority class