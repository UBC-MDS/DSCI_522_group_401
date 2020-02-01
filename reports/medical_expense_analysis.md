Medical Expense Data Analysis and Predictive Modeling
================
author: Karanpal Singh, Sreejith Munthikodu, Sirine Chahma </br>
2020/01/24

# Summary

Knowing the estimated medical expenses in advance is very critical for
insurance companies to set their yearly premiums to beneficiaries. They
should make sure that the amount they spent on beneficiaries is less
than the total premium they receive. Using a predictive model that
predicts the expected medical expense of a customer, the insurance
companies get an estimate of how much premium to charge on each segment
of customers such that the cost results in reasonable profit to the
company. Using such predictive models, they can identify potentially
high-risk customers and charge a higher premium from such customers. In
this project, we attempt to build a regression model that will help us
predict the medical expenses of a person given information such as age,
sex, number of children, smoking habits, and the region where the person
is from. In the process, we are also interested in figuring out if there
is a significant difference in expenses between smokers and non-smokers,
and between males and females. Our hypothesis tests suggest that at 0.05
significance level there is significant evidence to conclude that
smokers incur more medical expenses than non-smokers. Also, there is
statistically no significant evidence to conclude that the medical
expenses of men and women are different. For our predictive model, after
trying different regression models, we found that the decision tree
regressor performs the best on our data. Using our final tuned model, we
achieved satisfying results on the test data set, with a ￼ score of
0.894.

# Introduction

In this project, we attempt to build a predictive model that will answer
the following question : “Given a person’s information, what would be
his/her predicted medical expenses?”. Ansewering this question can be
important for insurance compagnies who wants to evaluate the risk to
insure a certain person regarding to his/her possible medical expenses.

We also wanted to figure out if there is a significant difference of
expenses between smokers and non-smokers, and between males and females.
Therefore, we led two inferential studies asside in order to find an
aswer to those questions.

# Data

The Data we are using for this analysis is used in the book Machine
Learning with R by Brett Lantz(Lantz 2013); which is a book that
provides an introduction to machine learning using R. All of these
datasets are in the public domain. The data explain the cost of a small
sample of USA population Medical Insurance Cost based on attributes like
age, sex, number of children etc. Additional information about this data
can be found
[here](https://gist.github.com/meperezcuello/82a9f1c1c473d6585e750ad2e3c05a41).

We didn’t have to clean this data because there were no outliers or
missing values, as described in
[this](https://github.com/UBC-MDS/DSCI_522_group_401/blob/master/notebooks/EDA.ipynb)
jupyter notebook.

The R and Python programming languages (R Core Team 2019) (Van Rossum
and Drake 2009) and the following R and Python packages were used to
split the data and study the missing values and the outliers : docopt
(de Jonge 2018), tidyverse(Wickham 2017), testthat (Wickham 2011),
pandas (McKinney 2010), numpy (Walt, Colbert, and Varoquaux 2011),
matplotlib and seaborn (Hunter 2007).

# Methodology

## Exploratory analysis on the training data set

To understand the nature of predictors with respect to `Medical
Expenses` we will perform Exploratory Data Analysis and we will try to
understand if there are some interesting behaviors. To do so, we will
use the following python packages : altair (VanderPlas et al. 2018),
matplotlib and seaborn (Hunter 2007), scikit-learn (Pedregosa et al.
2011).

##### 1\. Let’s see how `Medical Expenses` are changing with `Age`

<html>

<img src = '../reports/figures/1.Expenses_VS_Age.png'>

</html>

It can be observed that the `Medical Expense` of people is increasing,
as `Age`
increases.

##### 2\. Let’s see how `Medical Expenses` are changing with `BMI (Body Mass Index)`

<html>

<img src = '../reports/figures/2.Expenses_VS_BMI.png'>

</html>

The highest expenses seem to occur for people who have a higher
BMI.

##### 3\. Let’s see how much money males and females spending on medical treatments between 18-64 Years

<html>

<img src = '../reports/figures/3.Expenses_VS_Gender.png'>

</html>

The expenses seem to grow with age for both males and females. It looks
like Males in their **20’s & 60’s** tend to pay more on their `Medical
Expenses` than Females. Females in their **40’s** are paying more than
Males on their `Medical
Expenses`.

##### 4\. Let’s see how `Smokers` and `Non-Smokers` are spending on medical treatments between 18-64 Years

We expect expenditures by smokers should be higher than non-smokers.

<html>

<img src = '../reports/figures/4.Expenses_VS_Smoker.png'>

</html>

**Interesting\!\!\!** - As expected, health expenses of smokers are a
lot higher than that of non-smokers.

##### 5\. Let’s see the male & female expenses over BMI

<html>

<img src = '../reports/figures/6.EXP_VS_BMI.png'>

</html>

The highest expenses seem to occur for people from both genders who have
a BMI that is higher than 34.

##### 6\. Correlation between the variables

<html>

<img src = '../reports/figures/0.correlation.png'>

</html>

We can notice that none of the features seem to be correlated with each
other. Hence, the features don’t seem to be relevant individually.

## Answering the Inferential Research Questions

Now, from above Exploratory Data Analysis we are interested in following
two questions:

  - Are medical expenses of smokers are statistically higher than
    non-smokers?
  - Is there a significant statistical difference in expenses between
    males and females?
<br>

##### 1\. Are medical expenses of smokers are statistically higher than non-smokers?

  
![H\_0: \\mu\_{Smokers} \\leq
\\mu\_{Non-Smokers}](https://latex.codecogs.com/png.latex?H_0%3A%20%5Cmu_%7BSmokers%7D%20%5Cleq%20%5Cmu_%7BNon-Smokers%7D
"H_0: \\mu_{Smokers} \\leq \\mu_{Non-Smokers}")  
  
![H\_1: \\mu\_{Smokers} \>
\\mu\_{Non-Smokers}](https://latex.codecogs.com/png.latex?H_1%3A%20%5Cmu_%7BSmokers%7D%20%3E%20%5Cmu_%7BNon-Smokers%7D
"H_1: \\mu_{Smokers} \> \\mu_{Non-Smokers}")  

Our null hypothesis states that the mean expense of smokers is less than
equal to the mean expense of non-smokers and alternate hypothesis states
that the expenses of smokers are higher than the expenses of
non-smokers. We have used a One Sample t-test:

<table>

<thead>

<tr>

<th style="text-align:right;">

estimate

</th>

<th style="text-align:right;">

statistic

</th>

<th style="text-align:right;">

p.value

</th>

<th style="text-align:right;">

parameter

</th>

<th style="text-align:right;">

conf.low

</th>

<th style="text-align:right;">

conf.high

</th>

<th style="text-align:left;">

method

</th>

<th style="text-align:left;">

alternative

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:right;">

32050.23

</td>

<td style="text-align:right;">

33.87013

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

273

</td>

<td style="text-align:right;">

30899.45

</td>

<td style="text-align:right;">

Inf

</td>

<td style="text-align:left;">

One Sample t-test

</td>

<td style="text-align:left;">

greater

</td>

</tr>

</tbody>

</table>

The exact p-value is
![4.6718552\\times 10^{-100}](https://latex.codecogs.com/png.latex?4.6718552%5Ctimes%2010%5E%7B-100%7D
"4.6718552\\times 10^{-100}") which is very close to 0. However, while
rendering the output to the table above it treats it as 0.

We can observe that the p-value is less than the significance level of
![5\\%](https://latex.codecogs.com/png.latex?5%5C%25 "5\\%"). Hence, we
can reject ![H\_0](https://latex.codecogs.com/png.latex?H_0 "H_0")
hypothesis and conclude that we have enough evidence to say the mean
expenses of smoker is higher than the mean expenses of
non-smokers.

##### 2\. Is there a significant statistical difference in expenses between males and females?

  
![H\_0: \\mu\_{Males} =
\\mu\_{Females}](https://latex.codecogs.com/png.latex?H_0%3A%20%5Cmu_%7BMales%7D%20%3D%20%5Cmu_%7BFemales%7D
"H_0: \\mu_{Males} = \\mu_{Females}")  
  
![H\_1: \\mu\_{Males} \\neq
\\mu\_{Females}](https://latex.codecogs.com/png.latex?H_1%3A%20%5Cmu_%7BMales%7D%20%5Cneq%20%5Cmu_%7BFemales%7D
"H_1: \\mu_{Males} \\neq \\mu_{Females}")  

Our Null hypothesis states that the mean expenses of males are equal to
mean expenses of females and Alternate hypothesis states that there is a
significant difference between these two quantities. We have used t-test
to compare the mean of two groups and test results are as following:

<table>

<thead>

<tr>

<th style="text-align:right;">

estimate

</th>

<th style="text-align:right;">

estimate1

</th>

<th style="text-align:right;">

estimate2

</th>

<th style="text-align:right;">

statistic

</th>

<th style="text-align:right;">

p.value

</th>

<th style="text-align:right;">

parameter

</th>

<th style="text-align:right;">

conf.low

</th>

<th style="text-align:right;">

conf.high

</th>

<th style="text-align:left;">

method

</th>

<th style="text-align:left;">

alternative

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:right;">

\-1387.172

</td>

<td style="text-align:right;">

12569.58

</td>

<td style="text-align:right;">

13956.75

</td>

<td style="text-align:right;">

\-2.100888

</td>

<td style="text-align:right;">

0.035841

</td>

<td style="text-align:right;">

1313.36

</td>

<td style="text-align:right;">

\-2682.489

</td>

<td style="text-align:right;">

\-91.85535

</td>

<td style="text-align:left;">

Welch Two Sample t-test

</td>

<td style="text-align:left;">

two.sided

</td>

</tr>

</tbody>

</table>

The exact p-value is
![0.035841](https://latex.codecogs.com/png.latex?0.035841 "0.035841")
which is less than the significance level of
![5\\%](https://latex.codecogs.com/png.latex?5%5C%25 "5\\%") hence, we
can reject ![H\_0](https://latex.codecogs.com/png.latex?H_0 "H_0")
hypothesis and conclude that we have enough evidence to say mean
expenses between Males and Females is not same.

## Build a predictive model

In this data analysis project, we primarily focus on predicting the
medical expenses given the details of a customer. We used Python for
building the machine learning model. The machine learning library,
`sci-kit learn` was extensively used in this project to transform the
data, feature engineering, feature selection, model selection,
hyper-parameter tuning and, model evaluation.

### Preprocessing

Firstly, the training data was loaded and the response variable was
separated from the training data. Then numerical and categorical
features in the data are identified. A summary of various feature
transformations done on the categorical and numerical features are given
below.

<table>

<thead>

<tr>

<th style="text-align:left;">

Numeric.features

</th>

<th style="text-align:left;">

Categorical.features

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

PolynomialFeatures

</td>

<td style="text-align:left;">

OneHotEncoder

</td>

</tr>

<tr>

<td style="text-align:left;">

StandardScaler

</td>

<td style="text-align:left;">

</td>

</tr>

</tbody>

</table>

### Model Selection

After preprocessing and feature transformations, various regression
models are fitted on the training data with the default parameters. A
model with the best performance on the training and validation dataset
is selected for hyper-parameter optimization. A summary of baseline
performance by various regression models is given below.

<table>

<thead>

<tr>

<th style="text-align:left;">

Error Metrics

</th>

<th style="text-align:right;">

Linear.Regression

</th>

<th style="text-align:right;">

Decision.Tree.Regressor

</th>

<th style="text-align:right;">

KNN.Regressor

</th>

<th style="text-align:right;">

Random.Forest.Regressor

</th>

<th style="text-align:right;">

SVR..Support.Vector.Regressor.

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

Mean absolute error, training

</td>

<td style="text-align:right;">

4062.5430

</td>

<td style="text-align:right;">

0.0000

</td>

<td style="text-align:right;">

2739.453

</td>

<td style="text-align:right;">

938.0060

</td>

<td style="text-align:right;">

8295.8650

</td>

</tr>

<tr>

<td style="text-align:left;">

Mean absolute error, validation

</td>

<td style="text-align:right;">

4102.0070

</td>

<td style="text-align:right;">

2808.8110

</td>

<td style="text-align:right;">

3654.221

</td>

<td style="text-align:right;">

2485.7190

</td>

<td style="text-align:right;">

8313.0090

</td>

</tr>

<tr>

<td style="text-align:left;">

training\_time(s)

</td>

<td style="text-align:right;">

0.0887

</td>

<td style="text-align:right;">

0.0736

</td>

<td style="text-align:right;">

0.082

</td>

<td style="text-align:right;">

1.3292

</td>

<td style="text-align:right;">

0.2062

</td>

</tr>

</tbody>

</table>

Based on the above scores, DecisionTreeRegressor was selected as the
final model and hyper-parameter tuning is done on it. In the data
analysis pipeline, selection of the model from the base models is
currently done manually.

### hyper-parameter tuning

Hyper-parameter optimization was performed using `GridSearchCV`. The
best parameters obtained from hyper-parameter optimization are given
below.

<table>

<thead>

<tr>

<th style="text-align:left;">

Hyper-parameter

</th>

<th style="text-align:right;">

Best.parameter

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

preprocessor\_\_num\_\_poly\_\_degree

</td>

<td style="text-align:right;">

2

</td>

</tr>

<tr>

<td style="text-align:left;">

regressor\_\_max\_depth

</td>

<td style="text-align:right;">

4

</td>

</tr>

<tr>

<td style="text-align:left;">

regressor\_\_min\_samples\_split

</td>

<td style="text-align:right;">

3

</td>

</tr>

</tbody>

</table>

# Results

### model evaluation on train and test dataset

The final tuned DecisionTreeRegressor model was evaluated on both the
training and test data using various regression metrics. A summary of
the results is shown below.

<table>

<thead>

<tr>

<th style="text-align:left;">

Evaluation Metric

</th>

<th style="text-align:right;">

training\_data

</th>

<th style="text-align:right;">

test\_data

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

Mean Absolute Error

</td>

<td style="text-align:right;">

2.336006e+03

</td>

<td style="text-align:right;">

2.780371e+03

</td>

</tr>

<tr>

<td style="text-align:left;">

Mean Squared Error

</td>

<td style="text-align:right;">

1.739013e+07

</td>

<td style="text-align:right;">

2.506713e+07

</td>

</tr>

<tr>

<td style="text-align:left;">

Root Mean Squared Error

</td>

<td style="text-align:right;">

4.170148e+03

</td>

<td style="text-align:right;">

5.006708e+03

</td>

</tr>

<tr>

<td style="text-align:left;">

R2\_score

</td>

<td style="text-align:right;">

8.821358e-01

</td>

<td style="text-align:right;">

8.261748e-01

</td>

</tr>

<tr>

<td style="text-align:left;">

Explained\_variance\_score

</td>

<td style="text-align:right;">

8.821358e-01

</td>

<td style="text-align:right;">

8.264199e-01

</td>

</tr>

</tbody>

</table>

A mean absolute error of 2780.3705362 can seem to be a very high score
for the regression model. However, considering the mean medical expense
of 1.322343110^{4}, we are not very far from predicting the accurate
expenses. Moreover, when we take a look at the
![R^2](https://latex.codecogs.com/png.latex?R%5E2 "R^2") score, which is
equal to 0.826, we realize that this score is pretty high, which means
that our model explains most of the variability of our response data
around its mean. The goodness of fit of the regression model is analzsed
in the following
section.

### Goodness of fit

![](../reports/figures/predicted_vs_actual_plot.png)<!-- -->![](../reports/figures/residual_plot.png)<!-- -->

From the predicted Vs Actual plot, we can see ther are some errors in
prediction at lower expenses. Overall the model does a pretty decent job
of predicting the medical expenses given the patient information.

# Limitations and Future Directions

The model that we built for predicting the medical expenses only serves
as a baseline. The limitations are mainly due to the data. We have a
very small dataset with very few features. For building a
deployment-ready model for practical applications we need to collect
more data. Apart from this, we can improve the model by performing
feature engineering. In this project, no new features were created apart
from polynomial features and one-hot-encoded features. With some
research on the domain, we can come up with entirely new features or we
can combine existing features to get new features. Also, we haven’t done
any feature selection in this project. Data collection and feature
engineering are the most critical steps in building any machine earning
product. However, due to the limited time available, we could not
allocate sufficient resources for feature engineering. Moreover, we
haven’t performed model selection and hyper-parameter tuning in this
project. SO there is a lot of scope for future works in this project.
Overall, this serves as a very good base model on which further
improvements can be made.

# References

<div id="refs" class="references">

<div id="ref-docopt">

de Jonge, Edwin. 2018. *Docopt: Command-Line Interface Specification
Language*. <https://CRAN.R-project.org/package=docopt>.

</div>

<div id="ref-Hunter:2007">

Hunter, J. D. 2007. “Matplotlib: A 2D Graphics Environment.” *Computing
in Science & Engineering* 9 (3). IEEE COMPUTER SOC: 90–95.
<https://doi.org/10.1109/MCSE.2007.55>.

</div>

<div id="ref-source">

Lantz, Brett. 2013. *Machine Learning with R*. PACKT Publishing.

</div>

<div id="ref-mckinney-proc-scipy-2010">

McKinney, Wes. 2010. “Data Structures for Statistical Computing in
Python.” In *Proceedings of the 9th Python in Science Conference*,
edited by Stéfan van der Walt and Jarrod Millman, 51–56.

</div>

<div id="ref-scikit-learn">

Pedregosa, F., G. Varoquaux, A. Gramfort, V. Michel, B. Thirion, O.
Grisel, M. Blondel, et al. 2011. “Scikit-Learn: Machine Learning in
Python.” *Journal of Machine Learning Research* 12: 2825–30.

</div>

<div id="ref-R">

R Core Team. 2019. *R: A Language and Environment for Statistical
Computing*. Vienna, Austria: R Foundation for Statistical Computing.
<https://www.R-project.org/>.

</div>

<div id="ref-Altair2018">

VanderPlas, Jacob, Brian Granger, Jeffrey Heer, Dominik Moritz, Kanit
Wongsuphasawat, Arvind Satyanarayan, Eitan Lees, Ilia Timofeev, Ben
Welsh, and Scott Sievert. 2018. “Altair: Interactive Statistical
Visualizations for Python.” *Journal of Open Source Software*, December.
The Open Journal. <https://doi.org/10.21105/joss.01057>.

</div>

<div id="ref-Python">

Van Rossum, Guido, and Fred L. Drake. 2009. *Python 3 Reference Manual*.
Scotts Valley, CA: CreateSpace.

</div>

<div id="ref-doi:10.1109/MCSE.2011.37">

Walt, Stefan van der, S. Chris Colbert, and Gael Varoquaux. 2011. “The
Numpy Array: A Structure for Efficient Numerical Computation.”
*Computing in Science & Engineering* 13 (2): 22–30.
<https://doi.org/10.1109/MCSE.2011.37>.

</div>

<div id="ref-testthat">

Wickham, Hadley. 2011. “Testthat: Get Started with Testing.” *The R
Journal* 3: 5–10.
<https://journal.r-project.org/archive/2011-1/RJournal_2011-1_Wickham.pdf>.

</div>

<div id="ref-tidyverse">

———. 2017. *Tidyverse: Easily Install and Load the ’Tidyverse’*.
<https://CRAN.R-project.org/package=tidyverse>.

</div>

</div>
