
# Mod 2 Code Challenge Review

You've come a long way with this material

Close out strong

![](https://media.giphy.com/media/f8mFljwmfesZHvC0YP/giphy.gif)

# TOC:  
  - [Bayes](#bayes)  
  - [Hypothesis Tests](#hypo_test)  
  - [Regression](#regression)



<a id="bayes"></a>

# Bayes

$\large P(A|B) = \frac{P(A) \times P(B|A)}{p(B)}$

![puppy_bowl](https://media.giphy.com/media/RZtgTyrPNR9T0tN4nL/giphy.gif)


Thomas wants to get a new puppy 🐕 🐶 🐩
He can choose to get his new puppy either from the pet store or the pound. The probability of him going to the pet store is $0.2$.
He can choose to get either a big, medium or small puppy.

If he goes to the pet store, the probability of him getting a small puppy is $0.6$. The probability of him getting a medium puppy is $0.3$, and the probability of him getting a large puppy is $0.1$.

If he goes to the pound, the probability of him getting a small puppy is $0.1$. The probability of him getting a medium puppy is $0.35$, and the probability of him getting a large puppy is $0.55$.


1) What is the probability of Thomas getting a small puppy?

> Your answer here.  Write out your process in addition to your final numeric answer.



```python
'P(small_puppy) = .2*.6 + .8*.1'

p_petstore = .2
p_pound = 1-p_petstore
p_pup_petstore = .6
p_pup_pound = .1

p_small_puppy = p_petstore*p_pup_petstore + p_pound * p_pup_pound
p_small_puppy
```




    0.2



2) Given that he got a large puppy, what is the probability that Thomas went to the pet store?

Your answer here.  Write out your process in addition to your final numeric answer.


```python
p_lp_g_ps = .1
p_lp_ps = .1
p_lp_pound = .55
p_lp = p_petstore*p_lp_ps + p_pound*p_lp_pound

p_ps_given_lp = (p_petstore * p_lp_g_ps)/p_lp
p_ps_given_lp
```




    0.043478260869565216



# Z-Score

We know the average for SAT scores for math as a whole in the U.S. in 2019 is 531 with a standard deviation of 104.

Calculate the z-score associated with a math score of 650.



```python
math_mu = 527
math_std = 107
student_score = 650
z_score = (student_score - math_mu)/math_std
z_score
```




    1.1495327102803738



## Hypothesis Testing: Exercise 1

An SAT prep class of 40 students takes the SAT and gets the following math scores:


Did this SAT prep class result in a significantly greater mean score than population average?


```python
'''
Null: The scores of the prep group are less than or equal to the national average.
Alternative: The scores of the prep group are greater than the national average.
'''
```




    '\nNull: The scores of the prep group are less than or equal to the national average.\nAlternative: The scores of the prep group are greater than the national average.\n'




```python
'''
alpha = .05
'''
```




    '\nalpha = .05\n'




```python
'''
Right tailed z-test.  We know the population mean and standard deviation, and the sample count is greater than 30.
'''
```




    '\nRight tailed z-test.  We know the population mean and standard deviation, and the sample count is greater than 30.\n'




```python

critical_z = stats.norm.ppf(.95)
critical_z
```




    1.6448536269514722




```python
z = (np.mean(prep_class_scores) - math_mu)/math_std
z
```




    0.10944963655244026




```python
stats.norm.cdf(z)
# Cross check with http://www.z-table.com/
```




    0.5435770670457578




```python
# Our sample-stat is less than the critical test-statistic (the p-value is .54, much greater than our alpha), 
# and we cannot reject the null hypothesis.
```


```python
# Type I Error: We concluded that prep class scores were greater than the national mean, when in fact they were less than or equal.
```


```python
# Type II Error: We concluded that the prep-class score is not greater than the national average, when in fact it is.

```


```python
se = np.std(prep_class_scores)/np.sqrt(len(prep_class_scores))
z = stats.norm.ppf(.95)
conf_int_left  = np.mean(prep_class_scores) - z*se
conf_int_right =  np.mean(prep_class_scores) + z*se

print(conf_int_left, conf_int_right)
```

    518.2026552067983 559.2195670154239


## Hypothesis Testing: Exercise 2

You are an archeologist.  Not Indiana Jones, the non-violent kind.  And at two sites you come across a series of shards from pots.

You know from your archeologist training that different thicknesses at the lip of the pots indicate different ceremonial functions.  

You want to test the two samples of shard thickness to see if the thickness is due to chance at the two sites.

Sample 1 has slightly thinner shards overall, so you want to test if the mean of sample 1 lip thickness is less than the mean of sample 2 lip thickness.  

Assume that the two sample variances are equal.


```python
'''
Null: The mean lip thickness of shards in sample 1 are greater than or equal two the mean lip thickness of shards in sample 2.
Alternative: The mean lip thickness of shards in sample 1 are less than the mean lip thickness of shards in sample 2.
'''
```




    '\nNull: The mean lip thickness of shards in sample 1 are greater than or equal two the mean lip thickness of shards in sample 2.\nAlternative: The mean lip thickness of shards in sample 1 are less than the mean lip thickness of shards in sample 2.\n'




```python
'''
alpha = .05
'''
```




    '\nalpha = .05\n'




```python
'''
Left tailed two-sample independent t-test with equal variance assumed.

'''
```




    '\nLeft tailed two-sample independent t-test with equal variance assumed.\n\n'




```python
n = len(sample_1) + len(sample_2) - 2
stats.t.ppf(.05, n )
```




    -1.6772241953450402




```python
stats.ttest_ind(sample_1, sample_2, equal_var=True)
```




    Ttest_indResult(statistic=-1.7711939693439105, pvalue=0.08287752271565618)




```python
# Our sample-stat is less than the critical test-statistic (the p-value is .0414, which is less than our alpha), 
# and we can reject the null hypothesis.


```


```python
# We must divide the p_value by two, because by default, stats.ttest_ind returns a two tailed t-test
stats.ttest_ind(sample_1, sample_2, equal_var=True).pvalue/2
```




    0.04143876135782809




```python
"""We conclude that shard lips in sample 1 are thinner than sample 2, when in fact they are not"""
```


```python
"""We conclude that shard lips in sample 1 are equal or of greater width than sample 2, when in fact they are thinner."""
```

### Hypothesis Testing: Example 3
#### T-test question 1

Samples of diastolic blood pressure were taken from a sample of 20 female doctors

The mean female population diastolic blood pressure is 120

Are female doctor diastolic blood pressures significantly higher than the female population's?


```python
"Female doctors' dbp are less than or equal to the dbp of the greater female population"

```


```python
"Female doctors' dbp are greater than the dbp of the greater female population.
```


```python
alpha = .01
```


```python
stats.ttest_1samp(fem_docs_dbp, 120)
```




    Ttest_1sampResult(statistic=4.512403659336718, pvalue=0.00023838063630967753)




```python
'You conclude that female doctor dbp is greater than the female population at large, when in fact it is less than or equal to the female population'
```


```python
'You conclude that female dbp is less than or equal to the female population, when in fact it is greater than the female population.'
```


```python

fem_docs_mean = np.mean(fem_docs_dbp)
t_98 = stats.t.ppf(.99, len(fem_docs_dbp) - 1)

left = fem_docs_mean - t_98*np.std(fem_docs_dbp, ddof=1)/np.sqrt(len(fem_docs_dbp))
right = fem_docs_mean + t_98*np.std(fem_docs_dbp, ddof=1)/np.sqrt(len(fem_docs_dbp))

print(f"""98% Confidence interval: {left}, {right}""")
```

    98% Confidence interval: 124.39407734934214, 135.7059226506579


<a id='regression'></a>

# Linear Regression

### Statsmodels Linear Regression 

The stasmodels ols from formula.api take a formula as the first argument.  



```python
formula = 'target' + '~' + '+'.join(['sex', 'bmi','bp'])
formula
```


```python
model = ols(formula, df).fit()
```

Your answer here


```python
formula = 'target' + '~' + "+".join(df.drop('target', axis=1).columns)

ols(formula, df).fit().summary()

```

Did adding the full suite of independent features improve our model?

> Your answer here
