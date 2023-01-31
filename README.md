# Logistic Regression Model to Predict Default Probability
In this assignment, a logistic regression model is used to predict the probability of default using the income and balance on the Default data set. The results are reported using the summary function and the scatter plot of actual default and the fitted default is made.

library(ISLR2)
set.seed(312)
glm.fit = glm(default ~ income + balance, 
              data = Default, family = "binomial")
summary(glm.fit)


The summary shows that:

The coefficients for both income and balance are significant (p-value < 0.05).
The deviance residuals range from -2.4725 to 3.7245.
The residual deviance is 1579.0 on 9997 degrees of freedom and AIC is 1585.

train = sample(dim(Default)[1], dim(Default)[1] / 2)
fit.glm = glm(default ~ income + balance, 
              data = Default, family = "binomial", subset = train)
summary(fit.glm)


The summary shows that:

The coefficients for both income and balance are significant (p-value < 0.05).
The deviance residuals range from -2.6938 to 3.2917.
The residual deviance is 728.06 on 4997 degrees of freedom and AIC is 734.06.


glm.probs = predict(fit.glm, 
                    newdata = Default[-train, ], type="response")
glm.pred=rep("No",5000)
glm.pred[glm.probs>0.5] = "Yes"
mean(glm.pred != Default[-train, ]$default)

plot(x = predict(glm.fit, Default), 
     y = Default$default, 
     xlab = "Predicted", 
     ylab = "Observed", 
     main = "Predicted vs Observed")


The mean error of the prediction is 0.0296. The scatter plot of predicted vs observed shows that the model is mostly accurate in predicting the default.
