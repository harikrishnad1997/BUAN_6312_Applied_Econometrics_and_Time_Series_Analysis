# Assignment - 2: BUAN 6312 Harikrishna Dev HXD220000

## Answers

1. Use the data in APPLE to answer this question.

* Define a binary variable as ecobuy = 1 if ecolbs > 0 and ecobuy = 0 if ecolbs = 0. In other words, ecobuy indicates whether, at the prices given, a family would buy any ecologically friendly apples. What fraction of families claim they would buy ecolabeled apples?

<p>The fraction of fammilies claim they would buy ecolabeled apples are 62.42% </p>

```{STATA}

. gen ecobuy = 0

. replace ecobuy = 1 if ecolbs > 0
(412 real changes made)

. tabulate ecobuy

     ecobuy |      Freq.     Percent        Cum.
------------+-----------------------------------
          0 |        248       37.58       37.58
          1 |        412       62.42      100.00
------------+-----------------------------------
      Total |        660      100.00

```


* Estimate the linear probability model below and and report the results in the usual form. Carefully interpret the coefficients on the price variables (*ecoprc* and  *regprc* ).

$$
ecobuy=β_0+β_1 ecoprc+β_2 regprc+β_3 faminc+β_4 hhsize+β_5 educ+β_6 age+u
$$

<p> We get the LRM equation as follows:</p>

$$ ecobuy = 0.4236865 + -0.8026219 \times ecoprc + 0.7192675 \times regprc + 0.0005518 \times faminc + 0.0238227 \times hhsize + 0.0247849 \times educ - 0.0005008 \times age + u $$

<p> From the following equation, we can see that coefficients of <i>ecoprc</i> and <i>regprc</i> are <i>0.803</i> and <i>0.719</i>. The p-values of these coefficients are less than 0.05, therefore they are statistically significant. </p>

```{STATA}

. reg ecobuy ecoprc regprc faminc hhsize educ age

      Source |       SS           df       MS      Number of obs   =       660
-------------+----------------------------------   F(6, 653)       =     13.43
       Model |  17.0019785         6  2.83366308   Prob > F        =    0.0000
    Residual |  137.810143       653  .211041566   R-squared       =    0.1098
-------------+----------------------------------   Adj R-squared   =    0.1016
       Total |  154.812121       659  .234919759   Root MSE        =    .45939

------------------------------------------------------------------------------
      ecobuy | Coefficient  Std. err.      t    P>|t|     [95% conf. interval]
-------------+----------------------------------------------------------------
      ecoprc |  -.8026219   .1094037    -7.34   0.000    -1.017447   -.5877963
      regprc |   .7192675    .131639     5.46   0.000     .4607808    .9777543
      faminc |   .0005518   .0005295     1.04   0.298     -.000488    .0015916
      hhsize |   .0238227   .0125262     1.90   0.058    -.0007739    .0484193
        educ |   .0247849   .0083743     2.96   0.003      .008341    .0412287
         age |  -.0005008   .0012499    -0.40   0.689    -.0029551    .0019536
       _cons |   .4236865   .1649674     2.57   0.010      .099756     .747617
------------------------------------------------------------------------------

```


* Are the nonprice variables jointly significant in the LPM? (Use the usual F statistic, even though it is not valid when there is heteroskedasticity.) Which explanatory variable other than the price variables seems to have the most significant effect on the decision to buy ecolabeled apples? Does this make sense to you?

<p> We can see that we conduct a hypothesis tests on the non price variables gives us a <i>p_value < 0.05</i>. Therefore, we can reject the null hypothesis i.e. non-price variables are jointly significant. As <i>t(educ) = 2.96</i> is the highest t statistic value among the non price variable, we can conclude that <i>education</i> makes most significant effect on purchase of eco-labeled apples. This makes sense that educated customers would prefer ecolabeled apples as they would be more well equipped in understanding the benefit of the consumption of them.</p>

```{STATA}

. test faminc hhsize educ age

 ( 1)  faminc = 0
 ( 2)  hhsize = 0
 ( 3)  educ = 0
 ( 4)  age = 0

       F(  4,   653) =    4.43
            Prob > F =    0.0015

```


* In the model from part (ii), replace $faminc$ with $log(faminc)$. Given the $R^2$, which model fits the data better? How many estimated probabilities are negative? How many are bigger than one? Should you be concerned? [Hint: Use command predict y to generate fitted values.]

```{STATA}

. gen lfaminc = ln(faminc)

. reg ecobuy ecoprc regprc lfaminc hhsize educ age

      Source |       SS           df       MS      Number of obs   =       660
-------------+----------------------------------   F(6, 653)       =     13.67
       Model |   17.278689         6   2.8797815   Prob > F        =    0.0000
    Residual |  137.533432       653  .210617813   R-squared       =    0.1116
-------------+----------------------------------   Adj R-squared   =    0.1034
       Total |  154.812121       659  .234919759   Root MSE        =    .45893

------------------------------------------------------------------------------
      ecobuy | Coefficient  Std. err.      t    P>|t|     [95% conf. interval]
-------------+----------------------------------------------------------------
      ecoprc |  -.8006664   .1092981    -7.33   0.000    -1.015285   -.5860482
      regprc |    .721377   .1315196     5.48   0.000     .4631247    .9796294
     lfaminc |   .0445162   .0287239     1.55   0.122    -.0118861    .1009185
      hhsize |   .0227002    .012543     1.81   0.071    -.0019294    .0473297
        educ |    .023093   .0084508     2.73   0.006      .006499     .039687
         age |  -.0003865   .0012517    -0.31   0.758    -.0028444    .0020713
       _cons |   .3037519   .1789605     1.70   0.090    -.0476555    .6551593
------------------------------------------------------------------------------

```

2. Use the data in EZANDERS for this exercise. The data are on monthly unemployment claims in Anderson Township in Indiana, from January 1980 through November 1988. In 1984, an enterprise zone (EZ) was located in Anderson (as well as other cities in Indiana). 

* Regress log(uclms) on a monthly linear time trend and 11 monthly dummy variables. [Hint: Use jan as the base month for the monthly dummy variables.]What was the overall trend in unemployment claims over this period? (Interpret the coefficient on the time trend.) Is there evidence of seasonality in unemployment claims?

<p> Answer here </p>

* Add ez, a dummy variable equal to one in the months Anderson had an EZ, to the regression in part (i). Does having the enterprise zone seem to decrease unemployment claims? By how much?

<p> Answer here </p>

* 	Now use Δlog⁡(invpc_t) as the dependent variable. Re-run the equation and report the results in standard form. How do your results of the coefficient β ̂_1 change from part (ii)? Is the time trend still significant? Why or why not?

<p> Answer here </p>


4. Recall that in the example of testing Efficient Markets Hypothesis, it may be that the expected value of the return at time t, given past returns, is a quadratic function of $return_{t-1}$. 

* To check this possibility, use the data in NYSE to estimate

$$ return_t=β_0+β_1 return_{t-1}+β_2 return_{t-1}^2+u_t $$

report the results in standard form.

<p> Answer here</p>


* State and test the null hypothesis that E(return_t |return_(t-1)) does not depend on returnt-1. [Hint: There are two restrictions to test here.] What do you conclude?

<p> Answer here </p>

* Drop $return_{t-1}^2$ from the model, but add the interaction term $return_{t-1} \times return_{t-2}$. Now test the efficient markets hypothesis. [Hint: stata can create lag (or lead) variables using subscripts conveniently. For example, you can use the command gen return_2 = return[_n-2] to create $return_{t-2}$ fast.]

<p> Answer here </p>

* What do you conclude about predicting weekly stock returns based on past stock returns?

<p> Answer here </p>

5. Use the data in KIELMC for this exercise.

* The variable dist is the distance from each home to the incinerator site, in feet. Consider the model

$$ log⁡(price)=β_0+δ_0 y_81 +\beta_1  log⁡(dist)+δ_1 y_81⋅log⁡(dist)+u.$$

If building the incinerator reduces the value of homes closer to the site, what is the sign of δ1? What does it mean if β1 > 0?

<p> Answer here </p>

* 	Estimate the model from part (i) and report the results in the usual form. Interpret the coefficient on $y_81⋅log⁡(dist)$. What do you conclude?

<p> Answer here </p>

* What do you conclude about predicting weekly stock returns based on past stock returns?

<p> Answer here </p>

* Add $age, age^2, rooms, baths, log(intst), log(land), and log(area)$ to the equation. Now, what do you conclude about the effect of the incinerator on housing values?

<p> Answer here </p>

* Why is the coefficient on $log(dist)$ positive and statistically significant in part (ii) but not in part (iii)? What does this say about the controls used in part (iii)?

<p> Answer here </p>

6. Use the data in PHILLIPS for this exercise. As we mentioned in Lecture 7, instead of the static Phillips curve model, we can estimate an expectations-augmented Phillips curve of the form

$$ Δinf_t=β_0+β_1 unem_t+e_t $$

where $Δinf_t=inf_t-inf_{t-1}$

* Estimate this equation by OLS and report the results in the usual form. In estimating this equation by OLS, we assumed that the supply shock, et, was uncorrelated with unemt. If this is false, what can be said about the OLS estimator of β1?

<p> Answer here </p>

* 	Suppose that et is unpredictable given all past information: $E(e_t│inf_(t-1),unem_(t-1),…)=0$. Explain why this makes $unem_t-1$ a good IV candidate for $unem_t$.

<p> Answer here </p>

* Does $unem_t-1$ satisfy the instrument relevance assumption? [Hint: You need to run a regression to answer this question.]

<p> Answer here </p>

* Estimate the expectations augmented Phillips curve by 2SLS using $unem_t-1$ as an IV for $unem_t$. Report the results in the usual form and compare them with the OLS estimates from (i).