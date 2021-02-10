
# Mod 2 Code Challenge Review

You've come a long way with this material

Close out strong

![](https://media.giphy.com/media/f8mFljwmfesZHvC0YP/giphy.gif)


```python
from scipy import stats
import pandas as pd 
import numpy as np
from src.student_caller import one_random_student, three_random_students
from src.student_caller import three_random_students
```

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
#__SOLUTION__
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
#__SOLUTION__
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
# your answer here
```


```python
#__SOLUTION__
math_mu = 527
math_std = 107
student_score = 650
z_score = (student_score - math_mu)/math_std
z_score
```




    1.1495327102803738



## Hypothesis Testing: Exercise 1

An SAT prep class of 40 students takes the SAT and gets the following math scores:



```python
prep_class_scores = [434, 694, 457, 534, 720, 
                     400, 484, 478, 610, 641,
                     425, 636, 654, 514, 563, 
                     370, 499, 640, 501, 625, 
                     519, 471, 598, 509, 531, 
                     511, 675, 450, 485, 507, 
                     550, 612, 542, 633, 575, 
                     595, 508, 499, 490, 597, 
                     522, 504, 650, 430, 400]

```

Did this SAT prep class result in a significantly greater mean score than population average?


```python
# Define Null Hypothesis

```


```python
# Define Alternative Hypothesis
```


```python
#__SOLUTION__
'''
Null: The scores of the prep group are less than or equal to the national average.
Alternative: The scores of the prep group are greater than the national average.
'''
```




    '\nNull: The scores of the prep group are less than or equal to the national average.\nAlternative: The scores of the prep group are greater than the national average.\n'




```python
# Choose alpha

```


```python
#__SOLUTION__
'''
alpha = .05
'''
```




    '\nalpha = .05\n'




```python
# What test are we using?


```


```python
#__SOLUTION__
'''
Right tailed z-test.  We know the population mean and standard deviation, and the sample count is greater than 30.
'''
```




    '\nRight tailed z-test.  We know the population mean and standard deviation, and the sample count is greater than 30.\n'




```python
# What is the critical statistic?

```


```python
#__SOLUTION__

critical_z = stats.norm.ppf(.95)
critical_z
```




    1.6448536269514722




```python
# What is the sample statistic? 


```


```python
#__SOLUTION__
z = (np.mean(prep_class_scores) - math_mu)/math_std
z
```




    0.10944963655244026




```python
# What is the p-value?

```


```python
#__SOLUTION__
stats.norm.cdf(z)
# Cross check with http://www.z-table.com/
```




    0.5435770670457578




```python
# Come to a conclusion w.r.t. the null hypothesis
```


```python
#__SOLUTION__
# Our sample-stat is less than the critical test-statistic (the p-value is .54, much greater than our alpha), 
# and we cannot reject the null hypothesis.
```


```python
# What is a type I error in this example (in plain English)
```


```python
#__SOLUTION__
# Type I Error: We concluded that prep class scores were greater than the national mean, when in fact they were less than or equal.
```


```python
# What is a type II error in plain English
```


```python
#__SOLUTION__
# Type II Error: We concluded that the prep-class score is not greater than the national average, when in fact it is.

```


```python
# Create a 90% confidence interval using the sample data. 
```


```python
#__SOLUTION__
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
sample_1 = [17.4715, 20.0386, 12.6012, 20.4401, 22.4969,
            9.8613, 19.6289, 9.7741, 5.9123, 17.4448, 
            10.1237, 24.9357, 15.9265, 7.9955, 17.6675, 
            13.6029, 17.8812, 16.4178, 5.1385, 7.0984, 
            18.1181, 20.2681, 14.7372, 7.1021, 16.7546]

```


```python
sample_2 =  [19.7475, 19.8387, 12.6873, 17.6973, 19.0878, 
             30.5562, 14.5291, 14.7627, 14.3439, 12.5745, 
             11.0734, 19.4998, 18.3869, 10.7374, 18.0030, 
             18.1730, 18.8374, 17.9287, 14.3563, 18.6004, 
             11.7280, 12.2898, 21.0552, 21.4184, 25.5953]

```


```python
# Define Null/Alternative Hypotheses

```


```python
#__SOLUTION__
'''
Null: The mean lip thickness of shards in sample 1 are greater than or equal two the mean lip thickness of shards in sample 2.
Alternative: The mean lip thickness of shards in sample 1 are less than the mean lip thickness of shards in sample 2.
'''
```




    '\nNull: The mean lip thickness of shards in sample 1 are greater than or equal two the mean lip thickness of shards in sample 2.\nAlternative: The mean lip thickness of shards in sample 1 are less than the mean lip thickness of shards in sample 2.\n'




```python
# Choose alpha

```


```python
#__SOLUTION__
'''
alpha = .05
'''
```




    '\nalpha = .05\n'




```python
# What test are we using?


```


```python
#__SOLUTION__
'''
Left tailed two-sample independent t-test with equal variance assumed.

'''
```




    '\nLeft tailed two-sample independent t-test with equal variance assumed.\n\n'




```python
# What is the critical statistic?

```


```python
#__SOLUTION__
n = len(sample_1) + len(sample_2) - 2
stats.t.ppf(.05, n )
```




    -1.6772241953450402




```python
# Use statsmodels to run the appropriate test.

```


```python
#__SOLUTION__
stats.ttest_ind(sample_1, sample_2, equal_var=True)
```




    Ttest_indResult(statistic=-1.7711939693439105, pvalue=0.08287752271565618)




```python
# Come to a conclusion w.r.t. the null hypothesis

```


```python
#__SOLUTION__
# Our sample-stat is less than the critical test-statistic (the p-value is .0414, which is less than our alpha), 
# and we can reject the null hypothesis.


```


```python
#__SOLUTION__
# We must divide the p_value by two, because by default, stats.ttest_ind returns a two tailed t-test
stats.ttest_ind(sample_1, sample_2, equal_var=True).pvalue/2
```




    0.04143876135782809




```python
# What is a type I error in plain English
```


```python
#__SOLUTION__
"""We conclude that shard lips in sample 1 are thinner than sample 2, when in fact they are not"""
```


```python
# What is a type II error in plain English
```


```python
#__SOLUTION__
"""We conclude that shard lips in sample 1 are equal or of greater width than sample 2, when in fact they are thinner."""
```

### Hypothesis Testing: Example 3
#### T-test question 1

Samples of diastolic blood pressure were taken from a sample of 20 female doctors


```python

fem_docs_dbp = [128,127,118,115,144,
                142,133,140,132,131,
                111,132,149,122,139,
                119,136,129,126,128]
```

The mean female population diastolic blood pressure is 120

Are female doctor diastolic blood pressures significantly higher than the female population's?


```python
# Null Hypothesis
```


```python
#__SOLUTION__
"Female doctors' dbp are less than or equal to the dbp of the greater female population"

```


```python
# Alternative Hypothesis
```


```python
#__SOLUTION__
"Female doctors' dbp are greater than the dbp of the greater female population.
```


```python
# Choose an alpha
```


```python
#__SOLUTION__
alpha = .01
```


```python
# run the appropriate t-test in statsmodels and make a conclusion
```


```python
#__SOLUTION__
stats.ttest_1samp(fem_docs_dbp, 120)
```




    Ttest_1sampResult(statistic=4.512403659336718, pvalue=0.00023838063630967753)




```python
# Type I Error in plain English
```


```python
#__SOLUTION__
'You conclude that female doctor dbp is greater than the female population at large, when in fact it is less than or equal to the female population'
```


```python
# Type II Error in plain English
```


```python
#__SOLUTION__
'You conclude that female dbp is less than or equal to the female population, when in fact it is greater than the female population.'
```


```python
# Calculate the 98% confidence interval given the array of sample blood pressures
```


```python
#__SOLUTION__

fem_docs_mean = np.mean(fem_docs_dbp)
t_98 = stats.t.ppf(.99, len(fem_docs_dbp) - 1)

left = fem_docs_mean - t_98*np.std(fem_docs_dbp, ddof=1)/np.sqrt(len(fem_docs_dbp))
right = fem_docs_mean + t_98*np.std(fem_docs_dbp, ddof=1)/np.sqrt(len(fem_docs_dbp))

print(f"""98% Confidence interval: {left}, {right}""")
```

    98% Confidence interval: 124.39407734934214, 135.7059226506579


<a id='regression'></a>

# Linear Regression


```python
from sklearn.datasets import load_diabetes
```


```python
data = load_diabetes()
```


```python
df = pd.concat([pd.DataFrame(data.target, columns=['target']),
                pd.DataFrame(data.data, columns=data.feature_names)
               ], axis=1)
```

### Statsmodels Linear Regression 


```python
from statsmodels.formula.api import ols
```

The stasmodels ols from formula.api take a formula as the first argument.  



```python
# Create a formula which incorporates sex, bmi, and bp.
formula = None
```


```python
#__SOLUTION__
formula = 'target' + '~' + '+'.join(['sex', 'bmi','bp'])
formula
```


```python
# feed the formula and dataframe into an instance of the ols class
# chain the fit method off the end to train the model
model = None
```


```python
#__SOLUTION__
model = ols(formula, df).fit()
```


```python
# run the summary method off the end of the fit model 
model.summary()
```


```python
# Within this model, which features are statistically significant?

```

Your answer here


```python
# Which features increase results in an increase in the predicted value?
```


```python
Your answer here
```


```python
# Now, build another model using all of the available features

```


```python
#__SOLUTION__
formula = 'target' + '~' + "+".join(df.drop('target', axis=1).columns)

ols(formula, df).fit().summary()

```

Did adding the full suite of independent features improve our model?

> Your answer here


```python

```
