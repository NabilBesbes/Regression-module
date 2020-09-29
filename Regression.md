---
title: "Project regression models"
author: "Nb"
date: "29 September 2020"
output:
  word_document: default
  pdf_document: default
  html_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
link for Coursera course [*Click here*](https://www.coursera.org/learn/regression-models)

<br>

<br>

### Inroduction
**Decription**

The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models).

**Format**

A data frame with 32 observations on 11 (numeric) variables.

[, 1]	mpg	Miles/(US) gallon

[, 2]	cyl	Number of cylinders

[, 3]	disp	Displacement (cu.in.)

[, 4]	hp	Gross horsepower

[, 5]	drat	Rear axle ratio

[, 6]	wt	Weight (1000 lbs)

[, 7]	qsec	1/4 mile time

[, 8]	vs	Engine (0 = V-shaped, 1 = straight)

[, 9]	am	Transmission (0 = automatic, 1 = manual)

[,10]	gear	Number of forward gears

[,11]	carb	Number of carburetors

**Source**

Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391–411

### Reading data
```{r}
data(mtcars)
# a brief view of data
str(mtcars)
```

### Analysing Our data
```{r}
pairs(mtcars)
#select some ones
pairs(mtcars[c("mpg","cyl","disp","wt","am")])
```
### Linear Model

```{r}
print("Number of cylinders")
fit1<-lm(cyl~., mtcars)
fit1

print("Weight")
fit2<-lm(wt~., mtcars)
fit2

print("miles / (US) gallon")
fit3<-lm(mpg~., mtcars)
fit3
```

### Searching the most p-value
```{r}
value<-names(mtcars)
p<-NULL
#append(fit_list, lm(get(value[1])~get(value[2]), mtcars))
for (i in value) {
  if (value[1]!=i){
    p[i]<-summary(lm(get(value[1])~get(i), mtcars))$coef[2,4]
  }
}

# this is the minimum p-value for mpg with wich variable
min(p)

```

Now we will search the variable wich is more correlated to the <span style="color: red;">mpg</span>	*Miles/(US) gallon*

```{r}
p[p==min(p)]
summary(lm(mpg~wt, mtcars))$coef
```

We conclude that there is relationsheep between **weigth** and mpg 
with slope equal to ** *-5.344* **

