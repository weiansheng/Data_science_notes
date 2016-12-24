*     Cross-validation is a procedure for estimating the test performance of a method of producing a model, rather than of the model itself. So the best thing to do is to perform k-fold cross-validation to determine the best hyper-parameter settings, e.g. number of hidden units, values of regularization parameters etc.

    the purpose of cross-validation is not to come up with our final model. We don't use these 5 instances of our trained model to do any real prediction. For that we want to use all the data we have to come up with the best model possible. The purpose of cross-validation is model checking, not model building.

    once we have used cross-validation to select the better performing model, we train that model (whether it be the linear regression or the neural network) on all the data.

cross-validation is to help dealing with overfit; we use cross-validation to evaluate our model, not to build a better model

A typical cross validation steps:
1. Train-test split
2. With train data, Built several model with different hyper parameters
(or build different models with different features, or use different ml algorithms)

3. Split Train data into train and validation data (train-validation split)

4. For each model, get an average score from k-fold cross-validation
(use cross-validation to compare/evaluate different models)
train and validate k times, get k instances for each model, get an average of score

5. Select the best model hyper-parameter (or features)
6. use the hyper-parameter (or the features) to build a final model, with both train and validation data together
7. Use the final model on test data to get test error

* Ridge and Lasso
Ridge regression does have one obvious disadvantage. Unlike best subset,
forward stepwise, and backward stepwise selection, which will generally
select models that involve just a subset of the variables, ridge regression
will include all p predictors in the final model.

ridge is beta**2, L2
lasso is abs(beta), could penalize to 0, L1
larger lambda: penalize more
lambda is a number not an array;
we can choose lambda for the bias-variance trade-off
normalization/standardization: (x-u)/std before add lambda for parameter tuning
after normalization, no constant or intercept anymore

A good way to handle this problem is to standardize the data so that all
standardize variables are given a mean of zero and a standard deviation of one

interpretation: beta - with the features, assuming everything else same
after ridge/lasso, very hard to interpret linear regression



In ridge/lasso what happens to the beta coefficients as you increase lambda,
the regularization parameter
most/all the beta coefficients decrease (sometimes it could increase for a while), if super high value, push to zero

The Lasso estimator is useful for imposing sparsity on the coefficients. In other words, it is generally preferred if we believe many of the features are not relevant.

bias-variance trade-off:
total error = bias + variance
bias: how model performance
if high bias: add more data, improve model
variance: how model variation with test data
if high variance: add regularization

* Logistic regression:
beta coefficients explanation:
predict college admit or not: with rank of school, gre score and gpa
gre: 0.0019 exp: 1.001918
gpa: 0.2154 exp: 1.240313
rank: -0.5984 exp: 0.549688
with the increase of GPA from 1 to 2, (same for 2 to 3, 3 to 4) the odds ratio increased by a factor of 1.24, odds of admit (gpa1)/odds of admit (gpa2)=1.24
with the rank change from 1 to 2, odds ratio is 0.55, change from 2 to 1,
odds ratio is 1/0.55 = 1.8
rank: 1, probability: 0.517493, odds: 1.072509
rank: 2, probability: 0.370889, odds: 0.589546
rank: 3, probability: 0.244751, odds: 0.324066
rank: 4, probability: 0.151201, odds: 0.178135
print 0.178135 / 0.324066 0.549687409355
print 0.324066 / 0.589546 0.549687386565
print 0.589546 / 1.072509 0.549688627322

ROC curve: TPR (sensitivity/recall) vs FPR (1-specificity); we can choose a trade-off point
but we cannot get threshold directly from ROC, need go back to model and check where we are

LogisticRegression().predict_proba returns 2 columns of values, if two classes, probability for 0 and 1, complementary to each other
AUC: represents accuracy
