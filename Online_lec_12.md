# Online Lecture 12 - Multinomial Logistic Regression

Multinomial Logistic Regression:

The dependent variable is categorical and has > 2 levels



```R
library(nnet)
library(stargazer)
```



```R
# determine the basic outcome
# ==> create a new variable with the desire reference level
df$dep_var_2 <- relevel(df$dep_var, ref="level_name")

ml$prog_2 <- relevel(ml$prog, ref = "academic")

# create the model
stored_model <- multinom(df$basic_outcome ~ ind_var1 + ind_var2 + ind_varn, data=data_name)

multinomial_model1 <- multinom(ml$prog_2 ~ ses + write, data = ml)
#multinomial_model1 <- multinom(prog_2 ~ ses + write, data = ml) # ???
# different from `glm()` you should define the basic outcome

summary(multinomial_model1)
stargazer(multinomial_model1,type="text")
```

The dependent variable `prog` have 3 levels: academic, vocation, general

If `academic` is your basic outcome, the model will return a comparison `academic` vs `general` and `academic` vs `vocation`.



How to read the `summary(multinomial_model1)`

==> p-value is not provided

==> use `library(stargazer)` to obtain readable outputs

==> `stargazer(multinomial_model1,type="text")`

==> How to read?

![](Online_lec_12_img/1.png)

(AIC is given at the bottom)

![](Online_lec_12_img/2.png)

![](Online_lec_12_img/3.png)

Instead of doing `exp()` manually, how to report RRR using `stargazer`?

```R
# 1. Create an object which include the RRR 
multinomial_model1_rrr <- exp( coef(multinomial_model1) )

# 2. Report RRR using stargazer
stargazer(multinomial_model1, type="text", coef=list(multinomial_model1_rrr), p.auto=FALSE)
```

![](Online_lec_12_img/4.png)



We build in total 3 models... If we simply choose the model with lowest AIC for interpretation, we may get wrong conclusion! We need to refer to the sociohistorical context to provide insightful explanation.

