---
title: "Adaptive Designs"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Information function is the percentage of participants you have out of the total (400 out of 500 participants information function at .8)
Beta = type two error rate
Futility bounds are on z-score scale which means standard effect sizes should be fine

```{r}
library(rpact)
design <- getDesignGroupSequential(typeOfDesign = "OF", informationRates = c(.2,.4,.6,.8, 1), alpha = 0.025, beta = 0.2, constantBoundsHP = 3, sided = 1, tolerance = 1e-08, futilityBounds = c(rep(.1,4)))
summary(getSampleSizeMeans(design, normalApproximation = FALSE, meanRatio = FALSE, thetaH0 = 0, stDev = 1, groups = 2, allocationRatioPlanned = 1))
```
Try simulation means
Non-inferior study set h1 to the effect you expect.
```{r}
summary(getSimulationMeans(design, meanRatio = FALSE, thetaH0 = 0,
  alternative = c(0.2, 0.6, 1), stDev = 1, groups = 2, plannedSubjects = c(20,40,60,80,100)))

```
Plot the design
```{r}
plot(design)
```



```{r}
dat = data.frame(a = rnorm(20), b = rnorm(20))
write.csv(dat, "dat.csv", row.names = FALSE)
```

