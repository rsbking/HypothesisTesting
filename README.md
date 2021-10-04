# HypothesisTesting
Notes on Hypothesis Testing from following the Codecademy course on Hypothesis Testing.

## Descriptive vs Inferential Statistics

- Descriptive statistics allow us to summarize a large amount of data into a small number of measures.
- Inferential statistics allows us to test hypotheses

## Central Limit Theorem

The sampling distribution of the mean of _any_ distribution is 
- normally distributed (as long as sample large enough)
- centered on the population mean
- has standard deviation equal to the population standard deviation divided by the square root of the sample size. This is called Standard Error.

The standard error ( AKA sample standard deviation) = population standard deviation / sqrt( sample size )

This means we can estimate the population standard deviatoin from looking at the standard deviation.

- estimate our st_error = sample_std / sqrt(sample_size)
- know from CLT that the sample_std is normally distributed
- 95% limit of a normal distribution is 1.96*st_error
- -> estimate that with 95% confidence that real population mean = sample mean +- st_error*1.96?

I found this blog post useful: https://dpananos.github.io/posts/2019/08/blog-post-23/


# Different things you might want to test

## How likely is this distibution of a binary outcome due to the same underlying probability distribution

Binomial test

## How likely is this continuous variable distribution to result in a sample average of X

ttest

## How likely are these two continuous distributions resultin from the same underlying distribution

Two sample ttest
In python we can do:
```py
from scipy.stats import ttest_ind
tstatistic, pval = ttest_ind(a_distibution, b_distribution)

```


## 
