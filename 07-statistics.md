# Statistics

# Table of Contents

[1. Introduction](#section-a)  
[2. Why We Are Using Think Stats](#section-b)  
[3. Instructions for Cloning the Repo](#section-c)  
[4. Required Exercises](#section-d)  
[5. Optional Exercises](#section-e)  
[6. Recommended Reading](#section-f)  
[7. Resources](#section-g)

## <a name="section-a"></a>1.  Introduction

[<img src="img/think_stats.jpg" title="Think Stats"/>](http://greenteapress.com/thinkstats2/)

Use Allen Downey's [Think Stats (second edition)](http://greenteapress.com/thinkstats2/) book for getting up to speed with core ideas in statistics and how to approach them programmatically. This book is available online, or you can buy a paper copy if you would like.

Use this book as a reference when answering the 6 required statistics questions below.  The Think Stats book is approximately 200 pages in length.  **It is recommended that you read the entire book, particularly if you are less familiar with introductory statistical concepts.**

Complete the following exercises along with the questions in this file. Some can be solved using code provided with the book. The preface of Think Stats [explains](http://greenteapress.com/thinkstats2/html/thinkstats2001.html#toc2) how to use the code.  

Communicate the problem, how you solved it, and the solution, within each of the following [markdown](https://guides.github.com/features/mastering-markdown/) files. (You can include code blocks and images within markdown.)

## <a name="section-b"></a>2.  Why We Are Using Think Stats 

The stats exercises have been chosen to introduce/solidify some relevant statistical concepts related to data science.  The solutions for these exercises are available in the [ThinkStats repository on GitHub](https://github.com/AllenDowney/ThinkStats2).  You should focus on understanding the statistical concepts, python programming and interpreting the results.  If you are stuck, review the solutions and recode the python in a way that is more understandable to you. 

For example, in the first exercise, the author has already written a function to compute Cohen's D.  **You could import it, or you could write your own code to practice python and develop a deeper understanding of the concept.** 

Think Stats uses a higher degree of python complexity from the python tutorials and introductions to python concepts, and that is intentional to prepare you for the bootcamp.  

**One of the skills to learn here is to understand other people’s code.  And this author is quite experienced, so it’s good to learn how functions and imports work.**

---

## <a name="section-c"></a>3.  Instructions for Cloning the Repo 
Using the [code referenced in the book](https://github.com/AllenDowney/ThinkStats2), follow the step-by-step instructions below.  

**Step 1. Create a directory on your computer where you will do the prework.  Below is an example:**

```
(Mac):      /Users/yourname/ds/metis/metisgh/prework  
(Windows):  C:/ds/metis/metisgh/prework
```

**Step 2. cd into the prework directory.  Use GitHub to pull this repo to your computer.**

```
$ git clone https://github.com/AllenDowney/ThinkStats2.git
```

**Step 3.  Put your ipython notebook or python code files in this directory (that way, it can pull the needed dependencies):**

```
(Mac):     /Users/yourname/ds/metis/metisgh/prework/ThinkStats2/code  
(Windows):  C:/ds/metis/metisgh/prework/ThinkStats2/code
```

---


## <a name="section-d"></a>4.  Required Exercises

*Include your Python code, results and explanation (where applicable).*

### Q1. [Think Stats Chapter 2 Exercise 4](statistics/2-4-cohens_d.md) (effect size of Cohen's d)  
Cohen's D is an example of effect size.  Other examples of effect size are:  correlation between two variables, mean difference, regression coefficients and standardized test statistics such as: t, Z, F, etc. In this example, you will compute Cohen's D to quantify (or measure) the difference between two groups of data.   

You will see effect size again and again in results of algorithms that are run in data science.  For instance, in the bootcamp, when you run a regression analysis, you will recognize the t-statistic as an example of effect size.
>>> ## Problem 1 Solution
Computing the mean difference
```python
first_mean = firsts.totalwgt_lb.mean()
others_mean = others.totalwgt_lb.mean()
diff_mean = first_mean - others_mean
print(diff_mean)
```

First babies are lighter than others, with a mean difference 
around 0.125 lbs

Now computing the Cohen D we can quanitfy the variability between two groups
```python
cd = CohenEffectSize(firsts.totalwgt_lb,others.totalwgt_lb)
print(cd)
```
This turns out to be 0.08 std different, which is somewhere between small
and very small difference

### Q2. [Think Stats Chapter 3 Exercise 1](statistics/3-1-actual_biased.md) (actual vs. biased)
This problem presents a robust example of actual vs biased data.  As a data scientist, it will be important to examine not only the data that is available, but also the data that may be missing but highly relevant.  You will see how the absence of this relevant data will bias a dataset, its distribution, and ultimately, its statistical interpretation.

>>>## Problem 2 Solution 
The pmf of the biased sample versus the unbiased sample is a pretty large 
biased for surveying children under 18. Here the missing data biases the data set, 
as it doesn't account for families without children at all. 
```python
resp = nsfg.ReadFemResp()
numkdhh = resp.numkdhh
pmf = thinkstats2.Pmf(numkdhh, label='numkdhh')
biaspmf = BiasPmf(pmf,'Biased PMF')
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biaspmf])
thinkplot.Config(xlabel='# of children', ylabel='PMF')
diff_mean = 100*(pmf.Mean() - biaspmf.Mean())
print(diff_mean)
``` 
pretty large difference!
### Q3. [Think Stats Chapter 4 Exercise 2](statistics/4-2-random_dist.md) (random distribution)  
This questions asks you to examine the function that produces random numbers.  Is it really random?  A good way to test that is to examine the pmf and cdf of the list of random numbers and visualize the distribution.  If you're not sure what pmf is, read more about it in Chapter 3.  
>>>## Problem 3 Solution
The CDF should converge to linear with large enough samples, for 1000 samples it should be approximately linear. The PMF should have the same
height at every number drawn, which should look like a large block between 0 and 1. 

Plotting out the CDF and PMF confirms that pythons random number generator is sufficiently uniform.
```python
# Generate 1000 random numbers
rando = np.random.random(1000)
pmf = thinkstats2.Pmf(rando)
thinkplot.Pmf(pmf, linewidth='0.1')
thinkplot.Config(xlabel='Random numbers between 0 and 1', ylabel='PMF')
# Now a CDF
cdf = thinkstats2.Cdf(rando)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Random numbers between 0 and 1', ylabel='CDF')
```
 
### Q4. [Think Stats Chapter 5 Exercise 1](statistics/5-1-blue_men.md) (normal distribution of blue men)
This is a classic example of hypothesis testing using the normal distribution.  The effect size used here is the Z-statistic. 

As it turns out, I qualify for the blue man group at 5'11" (although I am female)
along with 34.2% of the male population. 
```python
low = 177.8
high = 185.4
diff_bound = dist.cdf(high) - dist.cdf(low)   
print(diff_bound)
```
If I recompute for females, then 2% of those will qualify for the female
blue woman group. 
```python
mu = 163
sigma = 7.3
dist = scipy.stats.norm(loc=mu, scale=sigma)
dist.mean(), dist.std()
dist.cdf(mu-sigma)
low = 177.8
high = 185.4
diff_bound_female = dist.cdf(high) - dist.cdf(low)   
print(diff_bound_female)
```

### Q5. Bayesian (Elvis Presley twin) 

Bayes' Theorem is an important tool in understanding what we really know, given evidence of other information we have, in a quantitative way.  It helps incorporate conditional probabilities into our conclusions.

Elvis Presley had a twin brother who died at birth.  What is the probability that Elvis was an identical twin? Assume we observe the following probabilities in the population: fraternal twin is 1/125 and identical twin is 1/300.  

>>> ## Problem 5 Solution
Since there are two types of twins, fraternal and identical, each with different probabilities of occurence in the population.
First compute the probability that given the twin is fraternal or identical, the twin is also a boy.
For identical it's 50-50 since the gender has to be the same. However for fraternal, it's actually 25% since the twin can be b-g, g-b, b-b, or g-g. 
Finally, this is a conditional problem, which means you need to compute the probability of identical given twin brother. This is done by computing total probability of twin (demoninator) and then dividing the probability of both identical twin and twin brother to get the probability Elvis's twin brother was identical.

```python
from IPython.display import display, Math, Latex
# Identical Twin and Twin Brother

display(Math(r'P(Identical\:Twin \:and \:Twin \:Brother) = \frac{1}{300}\cdot\frac{1}{2}'))

# Fraternal Twin and Twin Brother

display(Math(r'P(Fraternal\:Twin \:and \:Twin \:Brother) = \frac{1}{125}\cdot\frac{1}{4}'))

# Conditional probability

display(Math(r'P(Identical\:Twin \:| \:Twin \:Brother) = \frac{\frac{1}{300}\cdot\frac{1}{2}}{\frac{1}{125}\cdot\frac{1}{4} + \frac{1}{300}\cdot\frac{1}{2}} = \frac{5}{11}'))

```
---

### Q6. Bayesian &amp; Frequentist Comparison  
How do frequentist and Bayesian statistics compare?

>> ## Problem 6 Solution 
A frequentist point of view can only build up a confidence interval by repeatedly measuring large samples of data and then creating an upper and lower bound around an unknown parameter. For example, given a large enough sample size about the height of someone, there is a confidence interval that will encapsulate the parameter measured to 95%. 
This is different from Bayesian point of view, which has prior knowledge about a distrubition. The measurement h is used to adjust the prior distrubtion, resulting in a new distrubtion. 
---

## <a name="section-e"></a>5.  Optional Exercises

The following exercises are optional, but we highly encourage you to complete them if you have the time.

### Q7. [Think Stats Chapter 7 Exercise 1](statistics/7-1-weight_vs_age.md) (correlation of weight vs. age)
In this exercise, you will compute the effect size of correlation.  Correlation measures the relationship of two variables, and data science is about exploring relationships in data.    

### Q8. [Think Stats Chapter 8 Exercise 2](statistics/8-2-sampling_dist.md) (sampling distribution)
In the theoretical world, all data related to an experiment or a scientific problem would be available.  In the real world, some subset of that data is available.  This exercise asks you to take samples from an exponential distribution and examine how the standard error and confidence intervals vary with the sample size.

### Q9. [Think Stats Chapter 6 Exercise 1](statistics/6-1-household_income.md) (skewness of household income)
### Q10. [Think Stats Chapter 8 Exercise 3](statistics/8-3-scoring.md) (scoring)
### Q11. [Think Stats Chapter 9 Exercise 2](statistics/9-2-resampling.md) (resampling)

---

## <a name="section-f"></a>6.  Recommended Reading

Read Allen Downey's [Think Bayes](http://greenteapress.com/thinkbayes/) book.  It is available online for free, or you can buy a paper copy if you would like.

[<img src="img/think_bayes.png" title="Think Bayes"/>](http://greenteapress.com/thinkbayes/) 

---

## <a name="section-g"></a>7.  More Resources

Some people enjoy video content such as Khan Academy's [Probability and Statistics](https://www.khanacademy.org/math/probability) or the much longer and more in-depth Harvard [Statistics 110](https://www.youtube.com/playlist?list=PL2SOU6wwxB0uwwH80KTQ6ht66KWxbzTIo). You might also be interested in the book [Statistics Done Wrong](http://www.statisticsdonewrong.com/) or a very short [overview](http://schoolofdata.org/handbook/courses/the-math-you-need-to-start/) from School of Data.
