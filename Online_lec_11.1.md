# Online Lecture 11

[TOC]

## Lecture 11 - Verifying Some Assumptions on Binomial Regression

What are "**Assumptions**" (definition): 

Conditions that need to be checked to guarantee a (logit) model is reliable/unbiased



Types of **Assumptions** in logistic model (that need to be checked):

* ~~Independence of observations~~ (not covered in lecture)

* ~~Sufficient nbr of cases/rule of the ten~~ (not important)

  (Something like "we should have big enough sample size"? I am not sure. More details in ppt, Page 5)
  $$
  SampleSize = \frac{ExplanatoryVariables * 10}{ExpectedProbability} 
  $$
  (Note that a factor variable with 8 levels ==> 7 explanatory variables)

* **Linearity** of independent variables and the log odds

  Logistic regression assumes linearity of independent variables and log odds. 

* **Collinearity** 

  Little or no multicollinearity (多重共线性) among the independent variables:
  The independent variables should not be too highly correlated with each other.

* Non **additivity** 

* **Influential Cases** 

  As it is the case for linear regression, some poorly predicted case (or outliers) can eventually have an influence on the regression coefficient.

(Review the ppt)



### How to Check the 4 Assumptions

#### Linearity in the log odds

Can be tested through adding an **interaction term** x(logx) in the equation.

If the interaction term's p-value is **below 0.05** the assumption of linearity is violated (**model is not good**)

p-value < 0.05 ==> issue

```R
# use the data in online 10
# see ppt for image example
CGA_golf_train_short$logage <- log(CGA_golf_train_short$age)

model1 <- glm(Golf_club_manager ~ Handicap_5cat + Sex + age + age:logage , family = "binomial",data=CGA_golf_train_short)

summary(model1)
```



#### Collinearity

An ad-hoc test named **Variable Inflation Factor** can be easily computed.

The **package car** is required to got the GVIF^(1/(2*Df)) more straightforwardly.

```R
# see ppt for image example
library(car)

vif(modelName)
```

GVIF^(1/(2*Df)) value **below 2** indicate that no serious collinearity exist between the dependent variables (**the model is good**).

GVIF^(1/(2*Df)) > 2   ==>   issue



#### Additivity

Can be tested by adding interaction term in the regression which measure the specific effect of an association of dependent variable on the independent variable.
The interaction term is added by calling var1:var2

```R
# see ppt for image example
modelName <- glm(Golf_club_manager ~ Handicap_5cat + Year_experience_as_trainer + Handicap_5cat:Year_experience_as_trainer + Sex + diploma + Past_practice, data=CGA_golf_train_short, family="binomial")

summary(modelName)
```

If the p-value of the association between **one of the levels of var1** and **one of the level of var2** is **below 0.05**, there is additivity (**model not good**).

p-value < 0.05   ==>   issue



#### Influential cases

Two approaches to test influential cases / “outliers” 

```R
library(LogisticDx)
```

1. **Numerical approach**

   If **Δβ** **is** **greater** **than** **1**, then we must remove the influential case and or revise the model (**model not good**)

   ```R
   # see ppt for image example
   dx(glmobject, byCov=FALSE)    # always add `byCov=FALSE`
   ```

   Only need to look at `dBhat`. If none of the value > 1, the model is good.

2. **Graphical approach** 

   ```R
   plot(glmobject)
   ```

   Only need to look at `SΔβ` graph (ppt, Page 20). 

   **No SΔβ>1** ==> no influential case (**the model is good**)

(See the Summary in ppt, Page 24)