
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


2) Given that he got a large puppy, what is the probability that Thomas went to the pet store?

Your answer here.  Write out your process in addition to your final numeric answer.

# Z-Score

We know the average for SAT scores for math as a whole in the U.S. in 2019 is 531 with a standard deviation of 104.

Calculate the z-score associated with a math score of 650.



```python
# your answer here
```

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
# Choose alpha

```


```python
# What test are we using?


```


```python
# What is the critical statistic?

```


```python
# What is the sample statistic? 


```


```python
# What is the p-value?

```


```python
# Come to a conclusion w.r.t. the null hypothesis
```


```python
# What is a type I error in this example (in plain English)
```


```python
# What is a type II error in plain English
```


```python
# Create a 90% confidence interval using the sample data. 
```

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
# Choose alpha

```


```python
# What test are we using?


```


```python
# What is the critical statistic?

```


```python
# Use statsmodels to run the appropriate test.

```


```python
# Come to a conclusion w.r.t. the null hypothesis

```


```python
# What is a type I error in plain English
```


```python
# What is a type II error in plain English
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
# Alternative Hypothesis
```


```python
# Choose an alpha
```


```python
# run the appropriate t-test in statsmodels and make a conclusion
```


```python
# Type I Error in plain English
```


```python
# Type II Error in plain English
```


```python
# Calculate the 98% confidence interval given the array of sample blood pressures
```

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
# feed the formula and dataframe into an instance of the ols class
# chain the fit method off the end to train the model
model = None
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

Did adding the full suite of independent features improve our model?

> Your answer here


```python

```
