# STATISTICAL INFERENCE COURSE PROJECT: PART 2- ANALYZING TOOLGROWTH DATA
Lawrence Lau  

**<font color=blue> Overview </font>**<br>
This report provides basic data exploratory and statistical analysis of the ToothGrowth dataset.  The [dataset's infosheet](http://www.inside-r.org/r-doc/datasets/ToothGrowth) states ToothGrowth measures the length (len) of teeth in each of 30 guinea pigs after three dose (dose) levels of Vitaminc C (.5, 1, and 2 mg) with each of two delivery methods (supp), Orange Juice (OJ) and Ascorbic Acid (VC).

**<font color=blue> Loading and Exploring Data </font>**<br>
Loading and viewing the structure of the ToolGrowth dataset.

```r
data(ToothGrowth)
str(ToothGrowth)
```

```
## 'data.frame':	60 obs. of  3 variables:
##  $ len : num  4.2 11.5 7.3 5.8 6.4 10 11.2 11.2 5.2 7 ...
##  $ supp: Factor w/ 2 levels "OJ","VC": 2 2 2 2 2 2 2 2 2 2 ...
##  $ dose: num  0.5 0.5 0.5 0.5 0.5 0.5 0.5 0.5 0.5 0.5 ...
```
We see there are 60 observations (rows) of 3 variables (columns), 2 numeric (len and dose) and 1 factor(supp).


Viewing a summary of ToothGrowth.

```r
summary(ToothGrowth)
```

```
##       len        supp         dose      
##  Min.   : 4.20   OJ:30   Min.   :0.500  
##  1st Qu.:13.07   VC:30   1st Qu.:0.500  
##  Median :19.25           Median :1.000  
##  Mean   :18.81           Mean   :1.167  
##  3rd Qu.:25.27           3rd Qu.:2.000  
##  Max.   :33.90           Max.   :2.000
```


Viewing the first few lines of ToothGrowth.

```r
head(ToothGrowth)
```

```
##    len supp dose
## 1  4.2   VC  0.5
## 2 11.5   VC  0.5
## 3  7.3   VC  0.5
## 4  5.8   VC  0.5
## 5  6.4   VC  0.5
## 6 10.0   VC  0.5
```
The three variables are length of teeth (len), dose levels of Vitamin C (dose), and delivery method (supp).  

Let's visualize the data.

```r
library(ggplot2)
g <- ggplot(ToothGrowth, aes(x = dose, y = len, color = supp))
g <- g + geom_point()
g <- g + stat_summary(aes(group = 1), geom = "line", fun.y = mean, size = 1, col = "black")
g <- g + facet_grid(. ~ supp)
g <- g + ggtitle("ToothGrowth, length vs dose per supplement")
g
```

![](StatInfProjPt2_files/figure-html/unnamed-chunk-4-1.png) 
<br>
The length of the teeth increases the higher the doses of given Vitamin C.  For doses of .5 and 1.0 mg it seems as if OJ is the more affective delivery method.  

**<font color=blue> Basic Summary of Data </font>**<br>

```r
library("lattice")
a <- aggregate(ToothGrowth$len, list(ToothGrowth$dose,ToothGrowth$supp),FUN=function(x) c(mean = mean(x), sd = sd(x)))
colnames(a)[c(1:3)] <- c("Dose", "Method", "Length")
a
```

```
##   Dose Method Length.mean Length.sd
## 1  0.5     OJ   13.230000  4.459709
## 2  1.0     OJ   22.700000  3.910953
## 3  2.0     OJ   26.060000  2.655058
## 4  0.5     VC    7.980000  2.746634
## 5  1.0     VC   16.770000  2.515309
## 6  2.0     VC   26.140000  4.797731
```
OJ's superior effectiveness in the .5 and 1.0 dosage amounts is obvious.



