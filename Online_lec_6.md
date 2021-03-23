# On-line Lecture 6

Import data from excel

```R
library("readxl")

# Specify sheet by its name
my_data <- read_excel("my_file.xlsx", sheet = "data")
  
# Specify sheet by its index
my_data <- read_excel("my_file.xlsx", sheet = 2)
```



## Lecture 6 (PPT)

```R
 + theme(axis.text.x = element_text(angle = 45, size=10))
```

Axis tick and label can be removed using `element_blank()` or `size=0` 

Legend can be removed using `legend.position="none"` 

```R
# Add the headcount for each bar in a graph which indicate proportion
ggplot(CUHKSZ_employment_survey_1,aes(fct_infreq(Occupation),y=(..count..)/sum(..count..),fill=Occupation))+
  geom_bar(alpha=0.75)+
  theme(legend.position="none",axis.text.x = element_text(angle = 45, hjust = 1,size=9))+
  geom_text(stat='count',aes(label=..count..),vjust=+1.5)+
  labs(title="Occupation of CUHK Shenzhen students after graduation",x=NULL, y="Proportion")
```

![](\Online_lec_6_img\ppt_1.png)


```R
# Make it reader oriented

+Scale_fill_manual(values=c(“color1”,”color2”…))

+geom_hline(yintercept=0.1)
```

![](\Online_lec_6_img\ppt_2.png)

```R
ggplot(CUHKSZ_employment_survey_1,aes(x=Monthly_salary_19,y=..density..))+
  geom_histogram(binwidth = 500, fill="blue",colour="black",alpha=0.5,boundary=8000)+
  geom_density(size=1, color="Blue",kernel="gaussian")
```

![](\Online_lec_6_img\ppt_3.png)

```R
ggplot(SEE_students_data_2,aes(x=BMI))+
  geom_histogram(data=subset(SEE_students_data_2,BMI<25),fill="Blue", alpha=0.5,binwidth = 1,color="Black")+
  geom_histogram(data=subset(SEE_students_data_2,BMI>25),fill="Red", alpha=0.5,binwidth = 1,color="Black")
```

![](\Online_lec_6_img\ppt_4.png)


---

## On-line Lecture 6 - Produce cutting edge visualization: ==two variable== or more

* Two continuous variables **(scatter plot)** 
* One categorical and one continuous **(Box plot)** 
* Two categorical variables **(Bar Chart)** 

### Two continuous variables (scatter plot)

Scatter plot

```R
ggplot(Student_BMI_2, aes(x=BMI,y=GPA))+geom_point()

ggplot(Student_BMI_2, aes(x=BMI,y=GPA))+geom_point(size=3) # change size of the point

#Adding extra information using color and shape
ggplot(Student_BMI_2, aes(x=BMI,y=GPA,color=Gender))+geom_point(size=2)
ggplot(Student_BMI_2, aes(x=BMI,y=GPA,color=Gender,shape=Dpt))+geom_point(size=2)
```

![](\Online_lec_6_img\1.png)
![](\Online_lec_6_img\2.png)
![](\Online_lec_6_img\3.png)
![](\Online_lec_6_img\4.png)

```R
#adding a curve showing the tendency (loess curve or linear model)
ggplot(Student_BMI_2, aes(x=BMI,y=weight))+geom_point()+geom_smooth(method="lm")
ggplot(Student_BMI_2, aes(x=BMI,y=weight))+geom_point()+geom_smooth(method="loess")
```

![](\Online_lec_6_img\5.png)
![](\Online_lec_6_img\6.png)

### One categorical and one continuous (Box plot)

Box plot

```R
ggplot(Student_BMI_2,aes(x=Gender,y=BMI,color=Gender))+geom_boxplot()
```

![](\Online_lec_6_img\7.png)

```R
summary( subset(df$BMI, df$Gender=="male") )
```



### Two categorical variables (Bar Chart)

Bar Chart

```R
Student_BMI_2$`place of birth`<-as.factor(Student_BMI_2$`place of birth`)
ggplot(Student_BMI_2,aes(fill=`place of birth`,x=Dpt))+geom_bar(position="dodge")
```

![](\Online_lec_6_img\8.png)

```R
# compare with
ggplot(Student_BMI_2,aes(fill=`place of birth`,x=Dpt))+geom_bar()
```

![](\Online_lec_6_img\9.png)

```R
# see the ggplot cheat sheet for image examples
+geom_bar(position="dodge")
+geom_bar(position="stack") # y-axis=count; # by default
+geom_bar(position="fill") # y-axis= propotion
```

![position="stack"](\Online_lec_6_img\10.png)
![position="fill"](\Online_lec_6_img\11.png)

---

## Tutorial 6

```R
summary( subset(hdro$HDI, hdro$Continent_fac == "North-America") )
```

