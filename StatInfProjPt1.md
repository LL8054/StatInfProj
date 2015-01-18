# Statistical Inference: Part 1- Comparing the exponential distribution in R and the Central Limit Theorem 
Lawrence Lau  

This is Part 1 of the peer assessment project from the Statistical Inference class in the Data Scientist Specialization course.  The objective is to explore the exponential distribution in R and compare it with the Central Limit Theorem.  

### <font color=blue> Simulations </font>

Below, we generate a histogram of 40 exponentials using rate(lambda) of 0.2.  The theoretical mean and standard deviation of an exponential distribution are 1/lambda, so we expect to see both somewhere around 5.  

```r
a <- rexp(40, rate=.2)
ma <- mean(a)
sda <- sd(a)
va <- var(a)
hist(a, main="Histogram of 40 exponentials")
abline(v=ma, col="blue", lwd=2)
```

![plot of chunk unnamed-chunk-1](./StatInfProjPt1_files/figure-html/unnamed-chunk-1.png) 

We see the **sample mean**, denoted by the vertical blue line, is **5.1012**. Remember, the theoretical mean and standard deviation of an exponential distribution are 1/lambda (1/.2 = 5). In this sample mean, we're -0.1012 off. The **sample standard deviation** is **5.1443**, which is off by -0.1443.  The variance, which is the standard deviation squared, is expected to be 25.  This population gives us a variance of 26.4642.   

Below is a histogram of the distribution of averages of 40 exponentials performed 1,000 times, commonly called the sampling distribution of the mean. Since it's taking 1,000 averages of 40 randomly drawn exponentials (affectively normalizing the distribution), we expect to see this histogram's shape take a bell-curve shape.  The mean should be the same as the population mean, 1/lambda (5). The standard deviation of the sampling distribution of the mean is the population standard deviation divided by the square root of the sample size used to compute the mean (5/sqrt(40) in this case).  That number should be 0.7906. The variance is the population standard deviation squared, divided by the sample size used to compute the mean (5^2 / 40).  We are expecting the variance to be .625. 

```r
mns=NULL
for (i in 1:1000) mns=c(mns, mean(rexp(40, rate=.2)))
hist(mns, main="Histogram of 1,000 Averages of 40 exponentials")
maa <- mean(mns)
sdaa <- sd(mns)
vaa <- var(mns)
abline(v=maa, col="blue", lwd=2)
```

![plot of chunk unnamed-chunk-2](./StatInfProjPt1_files/figure-html/unnamed-chunk-2.png) 

We see here the gaussian (bell-curved) nature of the histogram, which is a criterion of a normal distribution.^ We also see the **mean**, once again denoted by a vertical blue line, is **4.9996**. This confirms the theoretical exponential distribution mean of 1/lambda (5), which should also equal mean for the sampling distribution of the mean.  The **standard deviation** is **0.7886**;  we were expecting 0.7906.  The **variance** is **0.622**, which matches our expectation of 0.625.  



^Indeed, the Central Limit Theorem states that "the mean of any set of variates with any distribution having a finite mean and variance tends to the normal distribution". http://math.about.com/od/glossaryofterms/g/Bell-Curve-Normal-Distribution-Defined.htm
