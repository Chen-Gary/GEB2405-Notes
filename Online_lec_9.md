# Online Lecture 9 - Local correlation in cross tables

Packages used

```R
# same packages as last week
library(gmodels) # for `CrossTable()`
library(sjstats) # for cramer'V test - `crosstable_statistics()`
library(sjPlot) # for `sjPlot::sjt.xtab()`

library(GDAtools) # for `pem()`
```

---

## Expected Frequency + Chi-square contribution

Chi-square contribution in `CrossTable(data$x, data$y)` 



**expected**: If `TRUE`, chisq will be set to `TRUE` and expected cell counts from the chisq will be included **(this lec)** 

**prop.r**: If `TRUE`, row proportions will be included

**prop.c**: If `TRUE`, column proportions will be included

**prop.t**: If `TRUE`, table proportions will be included

**prop.chisq**: If `TRUE`, chi-square contribution of each cell will be included **(this lec)** 



Expected Frequency = (Row Total * Column Total) / N

```R
CrossTable(data$x, data$y, expected=TRUE)
```



We can also show **Expected Frequency** in `sjPlot::sjt.xtab()` by adding `showExpected=TRUE` 

```R
sjPlot::sjt.xtab(df$var1, df$var2, showExpected=TRUE)
```



## PEM (Percentage of Maximum Deviation)

See video 28:56 for details of PEM => between -100 and 100, where "0" shows that there is no statistical correlation.



See video 32:45 + 33:51 for an example of how to calculate **expected frequency** and **PEM**.



How to calculate PEM by R?

```R
library(GDAtools)

x <- table(df$var1, df$var2) # create an object and saved as a table
pem(x)
```

About PEM value:

* < 10%: not a significant deviation
* 10% ~ 15%: a small but significant deviation
* 15% ~ 30%: strong deviation
* more than 30%: very strong deviation

