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


## How likely are these multiple distributions all to be from the same underlying distribution

We could do multiple two-sample ttests, comparing each pair. 
However, as we add more distributions we run the risk of false discovery.
In stead recommends the _ANOVA_ (analysis of variance) method. 
This tests the null hypothesis that all groups have the same population mean.

```py
from scipy.stats import f_oneway
fstat, pval = f_oneway(scores_mathematicians, scores_writers, scores_psychologists)
```

If the p-value is below our significance threshold then we can conclude that at least one pair of groups has different scores on average. 
To find out which group we need to investigate further.

For this problem we could use *Tukey's* range test
```py
from statsmodels.stats.multicomp import pairwise_tukeyhsd
tukey_results = pairwise_tukeyhsd(data.score, data.major, 0.05)
print(tukey_results)
```

### Assumptions of T-test, ANOVA and Tukey

1. Observations should be independently randomly sampled from the population.
2. The standard deviation of the groups should be equal
3. The data should be normaly distributed (ish)
4. The groups created by the categorical variable must be independent



## Are the outcomes of two categorical variables associated?

Chi-squared test.

e.g. A/B test where half users are shown a green button and half shown a purple button. Was one group more likely to hit the button?

```py
#create table:
import pandas as pd
table = pd.crosstab(variable_1, variable_2)
 
#run the test:
from scipy.stats import chi2_contingency
chi2, pval, dof, expected = chi2_contingency(table)
```

### Assumptions

1. Observations need to be independently sampled
2. The categories must be mututally exclusive
3. The gorups shoudl be independent

![image](https://user-images.githubusercontent.com/1227598/135826631-62c83a37-dc64-4596-b84f-da6a94a4224c.png)

## Chosing a statistical test

|  | Comparing a sample statistic to a hypothesized population value | Testing for an association between two variables at the population level | Testing for an association between three or more variables at the population level |
| --- | --- | --- |
| Quantitive value | one sample t-test |   two sample t-test  | ANOVA and Tukey’s range test |
| Categorical variable   | Binomial test | Chi-2 test | Chi-2 test|


