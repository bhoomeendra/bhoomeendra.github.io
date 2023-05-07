---
layout: post
title: Linear and Logistic Regression
date: 2023-04-17 11:12:00-0400
description: This blog is a part of interview prepration this contain explanation and some good interview question on the topic
tags: Interview_prep
categories: ML
related_posts: false
---
# Linear Regression 
<!-- #### What is Linear Regression? -->
The linear regression establishes a relationship between the dependent variable (y) and one or more independent variables (x) using a best-fit straight line. This means relationship between the dependent and independent variables is linear in nature.
#### Checks to apply before applying Linear Regression
1. __Linearity:__ Linear relationship between dependent and independent variables that can be done using person correlation coefficient not the spearman correlation coefficient.
2. __Normality:__ The residuals are normally distributed. This means that the residuals follow a bell-shaped curve, with most of the values clustered around the mean. The normality assumption is necessary because it allows us to use the standard techniques of statistical inference, such as hypothesis testing and confidence intervals. Violations of normality can lead to biased and inefficient estimates, and incorrect conclusions about the statistical significance of the independent variables.
3. __Homoscedasticity:__ The distribution of residual should be same for all the values of independent variable because if the errors are dependent on the value of independent variable then the model is uncertain as some inputs and is certian at some inputs. This does not provide us a concrete prediction hence the model is not very reiable.
4. __No multicollinearity:__ There is no high correlation between the independent variables. This means that the independent variables are not too closely related to each other.  If there is high correlation between the independent variables, it can be difficult to separate out their individual effects on the dependent variable, leading to unstable estimates of the regression coefficients.

#### How to deal with multicollinearity?
1. __Remove one of the correlated variables:__ The simplest way to deal with multicollinearity is to remove one of the highly correlated variables from the regression model. The downside of this approach is that it reduces the degrees of freedom of the model, which can weaken the statistical power of your analysis.
2. __Combine the correlated variables:__ Another way to deal with multicollinearity is to combine the correlated variables together to form a single predictor. For example, if you had two highly correlated variables, you could combine them together to form a single predictor by taking their average.
3. __Use principal components:__ Principal components analysis (PCA) is a dimension reduction technique that can be used to reduce a large set of variables to a small set that still contains most of the information in the large set. This technique is useful when you have a large number of correlated predictors, and you want to summarize them with a smaller set of representative variables.
4. __Use regularization methods:__ Regularization methods, such as ridge (L2 regularization) regression and lasso regression( L1 Regularization), are powerful techniques that are designed to deal with multicollinearity by constraining the size of the regression coefficients. These methods work well when you have a large number of correlated predictors.
5. __Do nothing:__ If your goal is to make predictions, and not to understand the role of each individual variable, then multicollinearity might not be a problem. Multicollinearity only affects the interpretation of your model if you care about the specific role of each variable. However, multicollinearity does affect the precision of the estimated regression coefficients, which can cause your predictions to be less reliable.
6. __Use Partial Least Squares Regression:__ Partial least squares regression (PLS regression) is a regression method that is an alternative to ordinary least squares (OLS) regression. PLS regression is useful when you have a large number of correlated predictors, and you want to use them to predict an outcome, but you also want to reduce the number of predictors in your model. PLS regression is similar to principal components regression, but the key difference between the two methods is that PLS regression uses the response variable in the dimension reduction step, while principal components regression does not.

#### What is the difference between L1 and L2 regularization?
L2 regularization is also known as ridge regression. L1 also known as Lasso. The key difference between them is when we take derivative of the loss function for both, In L2 we see the update or change would be 2*coeff but in L1 it would be either 1 or -1. This is the reason why L1 regularization is used for feature selection and drives some of the coefficients to zero. 


#### What are the ways to solve the Linear Regression?
1. __Gradient Descent:__ Gradient descent is an iterative optimization algorithm that can be used to solve linear regression. It works by finding the minimum of a cost function, which is typically the sum of the squared residuals.
2. __Matrix Inversion:__ We use the matrix inversion to solve for the coefficients. For this to work, the matrix should be invertible. From here, we get the condition of multicollinearity that the determinant of the matrix should not be zero for the existence of the inverse. Visit [here](https://en.wikipedia.org/wiki/Ordinary_least_squares)

# Logistic Regression
<!-- #### What is Logistic Regression? -->
Logistic regression is linear regression over the log odds or logit of the probability of input belonging to a class. The model choice in logistic regression is the logits of the probability are linearly dependent on the independent variable. But the problem we solve with this is the __classification problem__. The output of the model is the probability of the input belonging to a class.
$$ logit(p) = log(\frac{p}{p+1}) $$

The model is as follows:

$$ logit(p) = w^Tx + b$$

$$ p = \frac{1}{1+e^{-(w^Tx+b)}}$$

$$ p = \sigma(w^Tx+b)$$

What sigmoid does is that it constrains the output between 0 and 1. This is one of the definitions of logistic regression. We can have a geometric explanation as well. We start with a classification boundary which is $$ w^Tx +b $$. We want a w such that $$ \forall i \; y_i(w^Tx_i+b)>=0  $$ this means that the predicted class and the actual class should be as for the term to be positive but using this as the objective function as some limitation. The problem is that when an outlier comes, the loss value will be very high, and the model will try to fit the outlier. To solve the problem sigmoid function is used as it constrains the values between 0 and 1.

#### Formulation of the loss function
The purpose of the loss function is to maximize the probability of the correct class. Logistic regression is a binary classification problem; hence we have two classes, 0 and 1. Higher probability is associated with class 1, and low probability is associated with class 0. The objective function is as follows:

$$ L = \prod_{i=1}^n p_i^{y_i}(1-p_i)^{1-y_i} \; where \; p = \sigma(w^Tx+b) $$

$$ L = \prod_{i=1}^n \sigma(w^Tx_i+b)^{y_i}(1-\sigma(w^Tx_i+b))^{1-y_i} $$

As all the values are always positive, taking log will not affect the optimization problem. Also will help with numerical stability as the probability values are very small and the product will be even smaller. Hence the loss function is as follows:

$$ L = \sum_{i=1}^n y_i log(\sigma(w^Tx_i+b)) + (1-y_i)log(1-\sigma(w^Tx_i+b)) $$ 

$$ w^* = argmax_w L(w)$$

But still, we have a problem which is that if when w tends to infinity, the we would have the maximum value of the objective function, which is not what we want. Hence we add a regularization term to the objective function. The objective function is as follows:

$$ L = - \sum_{i=1}^n y_i log(\sigma(w^Tx_i+b)) + (1-y_i)log(1-\sigma(w^Tx_i+b)) + \lambda ww^T$$ 

<!-- This theme supports rendering beautiful math in inline and display modes using [MathJax 3](https://www.mathjax.org/) engine. You just need to surround your math expression with `$$`, like `$$ E = mc^2 $$`. If you leave it inside a paragraph, it will produce an inline expression, just like $$ E = mc^2 $$. -->

<!-- To use display mode, again surround your expression with `$$` and place it as a separate paragraph. Here is an example: -->

<!-- $$\sum_{k=1}^\infty |\langle x, e_k \rangle|^2 \leq \|x\|^2$$ -->

# Interview Questions