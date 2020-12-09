---
date: "2020-12-05"
tags:
- uchicago
- notes
title: STAT 224 Notes
---

These are notes for STAT 224: Applied Regression Analysis, taught by James Dignam. 


## Lecture 3 

- Inference tests test the importance of the predictor 


## Lecture 4

- Can do all the regular things (confidence intervals, etc) to $\beta$s 
- $R^2$ is a measure of explained variation

## Lecture 5 

- MLR is regression with many predictors 
- Coefficients are one unit change holding all other predictors constant


## Lecture 6 

- F-Test tests whether all the coefficients are simultaneously 0 
- Standardized residuals residuals have mean 0 and variance 1 and are dependent also 
- Internally studentized residuals are approx. normal and have mean 0 and variance 1


## Lecture 7 

- Regression relies on assumptions about the model's form and about the errors 
  - Mean of response is a linear function of predictors (linearity)
  - Errors need to be normally distributed 
  - Errors need to have mean of 0
  - Errors and resposne have constant variance over predictors 
  - Errors are independent of each other


## Lecture 8 

- Ordinal and nominal categorical variables 
  - Represented in regression by dummy/indicator variables 
- Different categories need to be mutually exclusive 
- Omitted category is the base/control/reference category 
- Don't keep interactions in the model without the corresponding main effects in the model (talk about effects of both, they go together now)


## Lecture 9 

- Confounder is variable related to the predictor of interest and causally related to outcome but not in the causal pathway 
- Temporal ordering necessary in causal relationships 
- Effect modifiers are factors related to both predictors and response (they modify the strength of the association)
- Control of confounding is key in explanatory modeling 
  - positive confounders overestimates the effect and vice versa


## Lecture 10

- When linear regression assumptions violated, tranform
  - When transforming, all estimates and confidence intervals are expressed in that scale 
- Different violations call for different transformations 
  - non-normality is the least serious violation
  - log transformation works when process/relationship is on a multiplicative scale
  - square root form can have more stable variance over values 
  - Box-Cox Transformation is power transformation (find lambda)
    - Rank order preserving 
    - $\lambda = -1$ is an inverse transform etc.


## Lecture 11 

- Logit transform percentages ($\text{logit}(p)) = \log\frac{p}{1-p}$) 
- Reasons to transform: 
  - Unequal variance in the response variable 
  - Response variable not normally distributed (distribution the variable comes from has variance related to the mean)
- Weighted Lease Squares (WLS) permits differential influence of data points 
- Autocorrelation is when error terms are correlated 
  - Still apparent randomness among the residuals, but some kind of serial pattern that suggests lack of independence (implies heteroscedasticity)
  - Same observations in different time periods 
  - Spatially close observations 
  - Experiments run in batches 
- Durbin-Watson Test detects serial correlation
- Cochrane-Orcutt transformation corrects for autocorrelated errors 


## Lecture 12 

- Multicollinearity is when some or all predictors in a model are correlated with each other 
  - Not an error; arises from the lack of independent information about predictor variables in the dataset 
  - Threatens interpretation that coefficient is the incrase in the mean of Y for one-unit increase in X 
- How much can we permit, and what do we do if there's too much? 
  - All statistically independent means predictors are _orthogonal_ 
  - If collinearity is strong and ignored, all CIs become larger and $\beta$s become unstable (change substantially when other variables are added/removed)
  - Less of a concern for predictions; more of a concern for explaining a phenomenon
- Signs of multicollinearity: 
  - F test is significant but all individual t-tests are nonsignificant
  - A $\beta$ has opposite sign than expected 
  - General instability in estimates 
  - Large standard errors 
- Variance Inflation Factor (VIF), where J is a predictor $$\text{VIF} = \frac{1}{1-R_j^2}$$
  - Greater than 10 is multicollinear by convention 
- What to do: 
  - Get more / better data 
  - Omit redundant variables 
  - Constrained regression 
  - Principal Components


## Lecture 13 

- Variable selection: 
  - forward selection (add predictor with highest correlation with Y, then add highest partial correlation), 
  - backward selection (begin with all predictors, remove one with smallest t statistic), stepwise selection (add predictor as in forward selection, consider omitting based on backward), 
  - common approach (choose significant variables, put in MLR and remove non-significant, repeat until no more removing criteria)
- Residual Mean Square is related to $R^2$ \[\text{RMS} = \frac{\text{SSE}}{n - p}\] 
- Use AIC and BIC to see if models are nested or not (those metrics balance information extracted from the data and number of parameters)


## Lecture 14 

- Logistic regression is when response variable $Y$ is binary discrete variable (taking values 0 or 1)
  - The model predicts the logit of the response as a linear function of predictors
- Risk difference is the difference between one group and the other, as a proportion of the total
- Odds ratio is ratio of odds of event in each exposure group
- Difference of log odds is basic effect measure (same as log odds ratio)
- Use MLE because error structure is different 
  - Null hypothesis is independence vs. association 

## Lecture 15 

- Even in logistic regression, each covariate is an **adjusted effect** meaning hold other predictors constant 
- Coefficients are log odds ($E^\beta_1$ is odds ratio)
- Multiple logistic regression analysis: 
  - Likelihood Ratio -- like F-Test for linear model, surfaces significant predictors
    - LR has $\chi^2$ distribution with DF = # of model parameters 
    - As in SLR, redundant with test of only one predictor 
  - Hosmer-Lemeshow test measure goodness-of-fit (can id systemic variation that is not explained)
  - AIC and BIC can also be used 
  - ROC curves plots sensitivity vs false positive rate (perfect prediction has area under curve of 1, best classifier is in upper left corner)
    - Can tell you what classification threshold to use (w. validation in independent samples)

## Lecture 16 

- Generalized linear models are a framework for unifying theory and estimation models (need different: response, link function, error term, model)
  - Link function addresses how linear predictor $\chi \beta$ relates to $E(Y)$ 
- Poisson Regression (models count variables i.e. can't be negative, as outcome)
  - Assumption: conditional on the predictors the conditional mean and variance of the outcome are equal 
    - Don't use when variance exceeds the mean (overdispersed Poisson random variable) or too many zeros (zero-inflated Poisson)
  - Use goodness-of-fit test to determine whether the model form fits data
  



