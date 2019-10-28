Introduction
============

Nowadays, having a business implies awning a website. The primary aim of
a website is to provide information, which is crucial in the modern
business world. Suppose a website owner aims at increasing the number of
visitors in order to have more views, sales or popularity. To achieve
this goal, one first needs to understand the factors affecting web
traffic. The vast majority of small businesses try to increase website
hits or visits via advertisements.

We took a look at small business website statistics and saw how
important advertising is. Let us review the artificially generated
[data](https://drive.google.com/file/d/1Yb8_vaWtkmXOWxXT2n4ENCvlalILFYUg/view?usp=sharing).
The summary of the dataset is presented below.

    web <- as.data.frame(read.csv("website.csv"))
    options(knitr.kable.NA = '')
    kable(summary(web), digits=2)%>%
     kable_styling(bootstrap_options = "striped", 
       full_width = F)

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
Company
</th>
<th style="text-align:left;">
Budget
</th>
<th style="text-align:left;">
Visits
</th>
<th style="text-align:left;">
AdType
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Min. : 1.0
</td>
<td style="text-align:left;">
Min. : 50.0
</td>
<td style="text-align:left;">
Min. :3695
</td>
<td style="text-align:left;">
Direct Mail :213
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
1st Qu.: 250.8
</td>
<td style="text-align:left;">
1st Qu.: 299.8
</td>
<td style="text-align:left;">
1st Qu.:4228
</td>
<td style="text-align:left;">
Outdoor Ads :199
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Median : 500.5
</td>
<td style="text-align:left;">
Median : 549.5
</td>
<td style="text-align:left;">
Median :4460
</td>
<td style="text-align:left;">
Radio and Podcasts:197
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Mean : 500.5
</td>
<td style="text-align:left;">
Mean : 549.5
</td>
<td style="text-align:left;">
Mean :4554
</td>
<td style="text-align:left;">
Social Media Ads :187
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
3rd Qu.: 750.2
</td>
<td style="text-align:left;">
3rd Qu.: 799.2
</td>
<td style="text-align:left;">
3rd Qu.:4799
</td>
<td style="text-align:left;">
Video Ads :204
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
Max. :1000.0
</td>
<td style="text-align:left;">
Max. :1049.0
</td>
<td style="text-align:left;">
Max. :6060
</td>
<td style="text-align:left;">
</td>
</tr>
</tbody>
</table>

The data consists of 4 variables and 1000 observations without any
missing values. The variable `Company` shows the unique number of the
company whose website is being examined, variable `Visits` is the number
of website visits per week. The variables `AdType` and `Budget` show the
**main type** of advertising done by the company and the average monthly
amount spent on this advertisement, respectively. There are the 5 types
of advertisement in the data: Radio and Podcasts, Direct Mail, Video
Ads, Social Media Ads, Outdoor Ads.

![](/2019-10-30-Weighted-Ordinary-Least-Squares_files/figure-markdown_strict/unnamed-chunk-2-1.png)

The left graph indicates that there is a positive correlation between
the money spent on advertisement and the number of website visits. The
coloring of the plot has been done based on the variable `AdType`, and
the result shows that there is no interaction effect of two explanatory
variables on the popularity of the website. In general, website owners
spend an approximately equal amount of money on different types of
advertisements. Roughly there is no multicollinearity between
explanatory variables. Based on the second graph, as the medians and
spread of data are approximately the same, we can claim that the way one
chooses to increase the visibility of a website plays no significant
role.

To understand the effect of advertising let us consider the following
multiple linear regression model:

*V**i**s**i**t**s*<sub>*i*</sub> = *β*<sub>0</sub> + *β*<sub>1</sub>*B**u**d**g**e**t*<sub>*i*</sub> + *β*<sub>2</sub>*A**d**T**y**p**e*<sub>*i*</sub> + *ϵ*<sub>*i*</sub>

The result of fitted linear regression is presented in the output below:

    model <- lm(Visits ~ Budget + AdType, data = web)

    stargazer::stargazer(model,
      title = "DID Results",
      dep.var.labels = c("Answers"),
      out="models.htm",# out.header=TRUE,
      type = "html",
      header=FALSE, 
      covariate.labels = c(
        "Budget",
        "Ad Type: Outdoor Ads",
        "Ad Type: Radio and Podcasts",
        "Ad Type: Social Media Ads",
        "Ad Type: Video Ads"
      )
      )

<table style="text-align:center">
<caption>
<strong>DID Results</strong>
</caption>
<tr>
<td colspan="2" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
<em>Dependent variable:</em>
</td>
</tr>
<tr>
<td>
</td>
<td colspan="1" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
Answers
</td>
</tr>
<tr>
<td colspan="2" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
Budget
</td>
<td>
1.017<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.032)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Outdoor Ads
</td>
<td>
17.623
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(28.957)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Radio and Podcasts
</td>
<td>
31.784
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(29.003)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Social Media Ads
</td>
<td>
-40.288
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(29.366)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Video Ads
</td>
<td>
-10.368
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(28.737)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Constant
</td>
<td>
3,995.437<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(26.096)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
</tr>
<tr>
<td colspan="2" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
Observations
</td>
<td>
1,000
</td>
</tr>
<tr>
<td style="text-align:left">
R<sup>2</sup>
</td>
<td>
0.506
</td>
</tr>
<tr>
<td style="text-align:left">
Adjusted R<sup>2</sup>
</td>
<td>
0.504
</td>
</tr>
<tr>
<td style="text-align:left">
Residual Std. Error
</td>
<td>
293.017 (df = 994)
</td>
</tr>
<tr>
<td style="text-align:left">
F Statistic
</td>
<td>
203.633<sup>\*\*\*</sup> (df = 5; 994)
</td>
</tr>
<tr>
<td colspan="2" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
<em>Note:</em>
</td>
<td style="text-align:right">
<sup>*</sup>p&lt;0.1; <sup>**</sup>p&lt;0.05; <sup>***</sup>p&lt;0.01
</td>
</tr>
</table>

It is not surprising that the coefficients for the unique levels of
variable `AdType` are not significant, because there is no effect on the
response variable `Visits`. However, the coefficient for the variable
`Budget` is statistically significant and positive (see the graph). So,
the multiple regression analysis shows that with the increase in the
amount of money spent on advertising by $100 the number of visitors will
increase by, on average, 102. Thus, the number of visitors can be
predicted based on the ad budget.

And yet, this is not a reliable result, since an important factor has
been omitted. We will now discuss briefly the concepts of
heteroscedasticity, the causes and effects of nonconstant variance and
the ways of solving this problem.

The problem
===========

Nonconstant variance
--------------------

One of the Gauss–Markov conditions states that the variance of the
disturbance term in each observation should be constant. This
assumption, however, is clearly violated in most of the models resulting
in heteroscedasticity. Mathematically, homoscedasticity and
heteroscedasticity may be defined as:

-   **Homoscedasticity:**
    *σ*<sub>*ϵ*<sub>*i*</sub></sub><sup>2</sup> = *σ*<sub>*ϵ*</sub><sup>2</sup>
    the same for all observations
-   **Heteroscedasticity:** *σ*<sub>*ϵ*<sub>*i*</sub></sub><sup>2</sup>
    is not the same for all observations.

See the visual demonstration of homoscedasticity and heteroscedasticity
below:

<center>
<a href="https://towardsdatascience.com/the-concept-of-heteroscedasticity-c5652b746223" width="50%"><img src="HHSKED.png" alt="HvsH" /></a>
</center>

The left picture illustrates homoscedasticity. Let us start with the
first observation, where *X* has the value of *X*<sub>1</sub>. If there
was no disturbance term in the model, the observation would be
represented by the circle lied on line
*Y* = *β*<sub>1</sub> + *β*<sub>2</sub>*X*. The effect of the
disturbance term is to shift the observation upwards or downwards
vertically (downwards in case of *X*<sub>1</sub>). The potential
distribution of the disturbance term, before the observation was
generated, is shown by the normal distribution.

Although homoscedasticity is often taken for granted in regression
analysis, it is common to suppose that the distribution of the
disturbance term is different for different observations in the sample.
Suppose the variance of the distribution of the disturbance term rises
as X increases (right picture). This does not mean that the disturbance
term will necessarily have a particularly large (positive or negative)
value in an observation where X is large, but it does mean that the a
priori probability of having an erratic value will be relatively high.

The first graph of the relationship between the budget and visitors
illustrates typical scatter diagram of heteroscedastic data - there is a
tendency for their dispersion to rise as X increases. It means that even
though there is a positive relationship between the variables, starting
at a particular point large amount of money fails to imply a large
number of visitors. In other words, one can spend huge sums without the
guarantee of large traffic.

> Reasons and consequences

Heteroscedasticity is more likely to occur, for example, when

-   The values of the variables in the sample vary substantially in
    different observations.
-   The explanatory variable increases, the response tends to diverge.
    For example, families with low incomes will spend relatively little
    on luxury goods, and the variations in expenditures across such
    families will be small. But for families with large incomes, the
    amount of discretionary income will be higher.
-   The model is misspecified (using response instead of the log of
    response or instead of X^2 using X etc). Important variables may be
    omitted from the model.

Why does heteroscedasticity matter? As a matter of fact, the evidence
for the absence of bias in the OLS regression coefficients did not use
this condition. So we can be sure that the coefficients are still
unbiased.

Nevertheless, two concerns are raised:

-   *The variances of the regression coefficients*: if there is no
    heteroscedasticity, the OLS regression coefficients have the lowest
    variances of all the unbiased estimators that are linear functions
    of the observations of *Y*. If heteroscedasticity is present, the
    OLS estimators are inefficient because it is possible to find other
    estimators that have smaller variances and are still unbiased.

-   *The estimators of the standard errors of the regression
    coefficients* will be wrong and, as a consequence, the t-tests as
    well as the usual F tests will be invalid. It is quite likely that
    the standard errors will be underestimated, so the t statistics will
    be overestimated and you will have a misleading impression of the
    precision of your regression coefficients. You may be led to believe
    that a coefficient is significantly different from 0, at a given
    significance level, when, in fact, it is not.

How to detect
-------------

Since there is no limit to the possible variety of heteroscedasticity, a
large number of different tests appropriate for different circumstances
has been proposed. There are also a lot of statistical tests called to
test whether heteroscedasticity is present. The list includes but is not
limited to the following:

-   The Spearman Rank Correlation Test
-   The Goldfeld–Quandt Test
-   The Glejser Test
-   The Breusch-Pagan test
-   The White test

Despite the large number of the available tests, we will opt for a
simple technique to detect heteroscedasticity, which is looking at the
residual plot of our model. We can diagnose the heteroscedasticity by
plotting the residual against the predicted response variable.

    library(ggResidpanel)
    resid_auxpanel(residuals = resid(model), 
                   predicted = fitted(model), 
                   plots = c("resid", "index"))

![](/2019-10-30-Weighted-Ordinary-Least-Squares_files/figure-markdown_strict/unnamed-chunk-4-1.png)

In our case we can conclude that as budget increases, the website visits
tend to diverge.

The solution
============

The two most common strategies for dealing with the possibility of
heteroskedasticity is heteroskedasticity-consistent standard errors (or
[robust errors](http://afhayes.com/public/BRM2007.pdf)) developed by
White and **Weighted Ordinary Least Squares**.

WOLS
----

OLS does not discriminate between the quality of the observations,
giving equal weight to each, irrespective of whether they are good or
poor guides to the location of the line. Thus, it may be concluded that
if we can find a way of assigning more weight to high-quality
observations and less to the unreliable ones, we are likely to obtain a
better fit. In other words, our estimators of *β*<sub>1</sub> and
*β*<sub>2</sub> will be more efficient. WOLS works by incorporating
extra nonnegative constants (weights) associated with each data point
into the fitting criterion. We shall see how to do this below. Suppose
the true relationship is
<pre>
$$Y_i = \beta_1+\beta_2X_i + \epsilon_i$$
</pre>

and

*v**a**r*(*ϵ*<sub>*i*</sub>) = *σ*<sub>*ϵ*<sub>*i*</sub></sub><sup>2</sup>

So we have a heteroscedastic model. We could eliminate the
heteroscedasticity by dividing each observation by its value of
*σ*<sub>*ϵ*<sub>*i*</sub></sub>. The model becomes

<pre>
$$\frac{Y_i}{\sigma_{\epsilon_i}} = \beta_1\frac{1}{\sigma_{\epsilon_i}}+\beta_2\frac{X_i}{\sigma_{\epsilon_i}} + \frac{\epsilon_i}{\sigma_{\epsilon_i}}$$
</pre>
The disturbance term $\\frac{\\epsilon\_i}{\\sigma\_{\\epsilon\_i}}$ is
homoscedastic because
<pre>
$$E[(\frac{\epsilon_i}{\sigma_{\epsilon_i}})^2] = \frac{1}{\sigma_{\epsilon_i}^2}E(\epsilon_i^2)=\frac{1}{\sigma_{\epsilon_i}^2}\sigma_{\epsilon_i}^2=1$$
</pre>
Therefore, every observation will have a disturbance term drawn from a
distribution with population variance 1, and the model will be
homoscedastic. By rewriting the model, we will have
<pre>
$$Y_i' = \beta_1h_i + \beta_2X_i'+\epsilon_i',$$
</pre>

where $Y\_i'=\\frac{Y\_i}{\\sigma\_{\\epsilon\_i}}$,
$h\_i=\\frac{1}{\\sigma\_{\\epsilon\_i}}$,
$X\_i'=\\frac{X\_i}{\\sigma\_{\\epsilon\_i}}$,
$\\epsilon\_i'=\\frac{\\epsilon\_i}{\\sigma\_{\\epsilon\_i}}$

**Note** that there should not be a constant term in the equation. By
regressing $Y'$

on *h* and *X*′, we will obtain efficient estimates of *β*<sub>1</sub>
and *β*<sub>2</sub> with unbiased standard errors. The general solution
to this is

*β̂* = (*X*<sup>*T*</sup>*W**X*)<sup> − 1</sup>(*X*<sup>*T*</sup>*W**Y*),

where *W* is the diagonal martrix with diagonal entries equal to weights
and *V**a**r*(*ϵ*) = *W*<sup> − 1</sup>*σ*<sup>2</sup>.

In some cases, the values of the weights may be based on theory or prior
research. In our model, the standard deviations tend to increase as the
value of `Budget` increases, so the weights tend to decrease as the
value of `Budget` increases, thus the weights are known. Where the
weights are unknown, we can try different models and choose the best one
based on, for instance, the distribution of the error term. There are
the following common types of situations and weights:

-   When the variance is proportional to some predictor
    *x*<sub>*i*</sub>, then
    *V**a**r*(*y*<sub>*i*</sub>) = *x*<sub>*i*</sub>*σ*<sup>2</sup> thus
    we set *w*<sub>*i*</sub> = 1/*x*<sub>*i*</sub>

-   When the *i*<sup>*t**h*</sup> value of y is an average of
    *n*<sub>*i*</sub> observations $var(y\_i)=\\frac{\\sigma^2}{n\_i}$,
    thus we set *w*<sub>*i*</sub> = *n*<sub>*i*</sub> (this situation
    often occurs in cluster surveys).

-   When the *i*<sup>*t**h*</sup> value of y is a total of
    *n*<sub>*i*</sub> observations
    *v**a**r*(*y*<sub>*i*</sub>) = *σ*<sup>2</sup>*n*<sub>*i*</sub>,
    thus we set *w*<sub>*i*</sub> = 1/*n*<sub>*i*</sub>.

If the structure of weights is unknown, we have to perform a two-stage
estimation procedure. We need to estimate an ordinary least squares
regression to obtain the estimate of *σ*<sub>*i*</sub><sup>2</sup> for
*i*<sup>*t**h*</sup> squared residual and the absolute value of standard
deviation (in case of outliers). Thus, we can have different weights
depending on *σ*<sub>*i*</sub><sup>2</sup>. Often the weights are
determined by fitted values rather than the independent variable. Let us
show these different models via statistical package R. Fortunately, the
R function `lm()` ,which is used to perform the ordinary least squares,
provides the argument `weights` to perform WOLS. By default the value of
weights in `lm()` is `NULL`, weighted least squares are used with
weights `weights`, minimizing the sum of *w* \* *e*<sup>2</sup>.

Suppose we do not know the pattern of weights, and we want to fit the
models with the following weights $w\_i=\\frac{1}{x\_i}$,
$w\_i=\\frac{1}{x\_i^2}$, $w\_i=\\frac{1}{y\_i^2}$,
$w=\\frac{1}{y\_{hat}^2}$, $w\_i=\\frac{1}{\\sigma\_i^2}$,
$w\_i=\\frac{1}{|\\sigma\_i|}$.

    wols1 <- lm(Visits ~ Budget + AdType, data = web, weights = 1/Budget)
    wols2 <- lm(Visits ~ Budget + AdType, data = web, weights = 1/Budget^2)
    wols3 <- lm(Visits ~ Budget + AdType, data = web, weights = 1/fitted(model))
    wols4 <- lm(Visits ~ Budget + AdType, data = web, weights = 1/fitted(model)^2)
    wols5 <- lm(Visits ~ Budget + AdType, data = web, weights = 1/resid(model)^2)
    wols6 <- lm(Visits ~ Budget + AdType, data = web, weights = 1/abs(resid(model)))

The result of fitted models will be:

    stargazer::stargazer(model, wols1, wols2, wols3, wols4, wols5, wols6,
      title = "WOLS Results",
      dep.var.labels = c("Visits"),
      column.labels = c("-","1/Budget", "1/Budget\\^2", "1/y", "1/y\\^2", "1/e\\^2","1/|e|"),
      out="models.htm",
      type = "html",
      header=FALSE, 
      covariate.labels = c(
        "Budget",
        "Ad Type: Outdoor Ads",
        "Ad Type: Radio and Podcasts",
        "Ad Type: Social Media Ads",
        "Ad Type: Video Ads"
      )
      )

<table style="text-align:center">
<caption>
<strong>WOLS Results</strong>
</caption>
<tr>
<td colspan="8" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td colspan="7">
<em>Dependent variable:</em>
</td>
</tr>
<tr>
<td>
</td>
<td colspan="7" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td colspan="7">
Visits
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
\-
</td>
<td>
1/Budget
</td>
<td>
1/Budget^2
</td>
<td>
1/y
</td>
<td>
1/y^2
</td>
<td>
1/e^2
</td>
<td>
1/|e|
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(1)
</td>
<td>
(2)
</td>
<td>
(3)
</td>
<td>
(4)
</td>
<td>
(5)
</td>
<td>
(6)
</td>
<td>
(7)
</td>
</tr>
<tr>
<td colspan="8" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
Budget
</td>
<td>
1.017<sup>\*\*\*</sup>
</td>
<td>
1.014<sup>\*\*\*</sup>
</td>
<td>
1.018<sup>\*\*\*</sup>
</td>
<td>
1.015<sup>\*\*\*</sup>
</td>
<td>
1.014<sup>\*\*\*</sup>
</td>
<td>
1.018<sup>\*\*\*</sup>
</td>
<td>
1.014<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(0.032)
</td>
<td>
(0.024)
</td>
<td>
(0.022)
</td>
<td>
(0.031)
</td>
<td>
(0.031)
</td>
<td>
(0.001)
</td>
<td>
(0.008)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Outdoor Ads
</td>
<td>
17.623
</td>
<td>
9.016
</td>
<td>
1.778
</td>
<td>
17.291
</td>
<td>
16.927
</td>
<td>
18.380<sup>\*\*\*</sup>
</td>
<td>
16.810<sup>\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(28.957)
</td>
<td>
(19.540)
</td>
<td>
(10.354)
</td>
<td>
(28.251)
</td>
<td>
(27.531)
</td>
<td>
(1.405)
</td>
<td>
(8.426)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Radio and Podcasts
</td>
<td>
31.784
</td>
<td>
15.184
</td>
<td>
1.457
</td>
<td>
30.884
</td>
<td>
29.894
</td>
<td>
31.647<sup>\*\*\*</sup>
</td>
<td>
28.276<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(29.003)
</td>
<td>
(19.823)
</td>
<td>
(10.732)
</td>
<td>
(28.302)
</td>
<td>
(27.591)
</td>
<td>
(1.562)
</td>
<td>
(9.309)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Social Media Ads
</td>
<td>
-40.288
</td>
<td>
-10.390
</td>
<td>
-0.402
</td>
<td>
-36.504
</td>
<td>
-32.869
</td>
<td>
-39.380<sup>\*\*\*</sup>
</td>
<td>
-36.515<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(29.366)
</td>
<td>
(19.315)
</td>
<td>
(10.069)
</td>
<td>
(28.470)
</td>
<td>
(27.571)
</td>
<td>
(1.498)
</td>
<td>
(9.223)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Ad Type: Video Ads
</td>
<td>
-10.368
</td>
<td>
3.876
</td>
<td>
11.703
</td>
<td>
-7.915
</td>
<td>
-5.622
</td>
<td>
-8.910<sup>\*\*\*</sup>
</td>
<td>
-8.182
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(28.737)
</td>
<td>
(20.532)
</td>
<td>
(12.335)
</td>
<td>
(27.977)
</td>
<td>
(27.217)
</td>
<td>
(1.597)
</td>
<td>
(9.493)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td style="text-align:left">
Constant
</td>
<td>
3,995.437<sup>\*\*\*</sup>
</td>
<td>
3,993.525<sup>\*\*\*</sup>
</td>
<td>
3,992.827<sup>\*\*\*</sup>
</td>
<td>
3,995.256<sup>\*\*\*</sup>
</td>
<td>
3,995.106<sup>\*\*\*</sup>
</td>
<td>
3,994.459<sup>\*\*\*</sup>
</td>
<td>
3,996.948<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
(26.096)
</td>
<td>
(14.600)
</td>
<td>
(7.216)
</td>
<td>
(24.978)
</td>
<td>
(23.908)
</td>
<td>
(1.388)
</td>
<td>
(7.472)
</td>
</tr>
<tr>
<td style="text-align:left">
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
<td>
</td>
</tr>
<tr>
<td colspan="8" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
Observations
</td>
<td>
1,000
</td>
<td>
1,000
</td>
<td>
1,000
</td>
<td>
1,000
</td>
<td>
1,000
</td>
<td>
1,000
</td>
<td>
1,000
</td>
</tr>
<tr>
<td style="text-align:left">
R<sup>2</sup>
</td>
<td>
0.506
</td>
<td>
0.645
</td>
<td>
0.691
</td>
<td>
0.517
</td>
<td>
0.528
</td>
<td>
1.000
</td>
<td>
0.940
</td>
</tr>
<tr>
<td style="text-align:left">
Adjusted R<sup>2</sup>
</td>
<td>
0.504
</td>
<td>
0.644
</td>
<td>
0.689
</td>
<td>
0.515
</td>
<td>
0.526
</td>
<td>
1.000
</td>
<td>
0.939
</td>
</tr>
<tr>
<td style="text-align:left">
Residual Std. Error (df = 994)
</td>
<td>
293.017
</td>
<td>
11.263
</td>
<td>
0.492
</td>
<td>
4.242
</td>
<td>
0.061
</td>
<td>
1.000
</td>
<td>
14.521
</td>
</tr>
<tr>
<td style="text-align:left">
F Statistic (df = 5; 994)
</td>
<td>
203.633<sup>\*\*\*</sup>
</td>
<td>
361.792<sup>\*\*\*</sup>
</td>
<td>
444.545<sup>\*\*\*</sup>
</td>
<td>
213.209<sup>\*\*\*</sup>
</td>
<td>
222.603<sup>\*\*\*</sup>
</td>
<td>
585,907.100<sup>\*\*\*</sup>
</td>
<td>
3,091.199<sup>\*\*\*</sup>
</td>
</tr>
<tr>
<td colspan="8" style="border-bottom: 1px solid black">
</td>
</tr>
<tr>
<td style="text-align:left">
<em>Note:</em>
</td>
<td colspan="7" style="text-align:right">
<sup>*</sup>p&lt;0.1; <sup>**</sup>p&lt;0.05; <sup>***</sup>p&lt;0.01
</td>
</tr>
</table>

Weighted least squares estimates of the coefficients will usually be
nearly the same as the “ordinary” unweighted estimates. In the models
with explanatory variables such as weight `weights = 1/Budget^2`
produces the smallest standard errors. The summary of models shows that
the fitted equations are highly similar yet again. Overall, the smallest
standard errors are presented by the model with
`weights = 1/resid(model)^2`.

> Inverse of x and residuals with weights

However, as we know the pattern of weight allows to examine the residual
plots for the first two weighted OLS models.

    resid_compare(models = list(wols1, 
                                wols2),
                  plots = c("resid", "index"),
                  title.opt = FALSE)

![](/2019-10-30-Weighted-Ordinary-Least-Squares_files/figure-markdown_strict/unnamed-chunk-7-1.png)

Apparently, the nonconstant variance of the residuals still results in
heteroscedasticity. The issue is that the plots above use unweighted
residuals; whereas, with weighted least squares, we need to use weighted
residuals to evaluate the suitability of the model since these take into
account the weights which change variance. The usual residuals fail to
do this and will maintain the same non-constant variance pattern
irrelevant to the weights used in the analysis.

    # Weighted residuals by corresponding weight
    resid_auxpanel(residuals = sqrt(1/web$Budget)*resid(wols1), 
                   predicted = fitted(wols1), 
                   plots = c("resid", "index"))

![](/2019-10-30-Weighted-Ordinary-Least-Squares_files/figure-markdown_strict/unnamed-chunk-8-1.png)

    resid_auxpanel(residuals = sqrt(1/web$Budget^2)*resid(wols2), 
                   predicted = fitted(wols2), 
                   plots = c("resid", "index"))

![](/2019-10-30-Weighted-Ordinary-Least-Squares_files/figure-markdown_strict/unnamed-chunk-8-2.png)

It seems that the second WOLS model with the following weights
$w\_i=\\frac{1}{x\_i^2}$, because the variability of residuals is the
same for all predicted values. We can now be more confident in results
and state that with every $100 increase in the amount of money spent on
advertising the number of website visitors will rise by, on average,
102. The absence of heteroscedasticity and the fact that the standard
deviation of coefficient is less than in the original model allow to
make predictions with higher level of certainty.

Conclusion
==========

Overall, the weighted ordinary least squares is a popular method of
solving the problem of heteroscedasticity in regression models, which is
the application of the more general concept of **generalized least
squares.** WOLS implementation in R is quite simple because it has a
distinct argument for weights. As we saw, weights can be estimated
directly from sample variances of the response variable at each
combination of predictor variables. WOLS can sometimes be used where
different observations have been measured by various instruments,
importance or accuracy, and where weights are used to take these
circumstances into account.

The disadvantage of weighted least squares is that the theory behind
this method is based on the assumption that exact weight sizes are
known. However, when it comes to practice, it can be quite difficult to
determine weights or estimates of error variances. Note that WOLS is
neither the only nor the best method of addressing the issue of
heteroscedasticity. The alternative methods include estimating
heteroskedasticity-consistent standard errors, and other types of WOLS
(e.g. iteratively reweighted least squares).

------------------------------------------------------------------------

Reference List
==============

> *Oscar L. Olvera, Bruno D. Zumb, Heteroskedasticity in Multiple
> Regression Analysis: What it is, How to Detect it and How to Solve it
> with Applications in R and SPSS.*

> *R. Williams,
> [“Heteroskedasticity”](https://www3.nd.edu/~rwilliam/stats2/l25.pdf).*
