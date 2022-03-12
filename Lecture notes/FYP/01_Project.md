
Ideas for data series to add:
- control for test numbers
- airport traffic
- air pollution / PM 2.5
- 
- median age
- share of population in urban areas
- population attitude (adherence to restrictions)
- inequality


[Our World in Data](ourworldindata.com) - 
[naturalearthdata.com/](https://www.naturalearthdata.com/) - Map, Data
[GADM.org ](https://gadm.org/) - very detailed maps (data, too)
Sources
- [Pearson correlation](https://www.spss-tutorials.com/pearson-correlation-coefficient/)
- [Spearman correlation](https://www.spss-tutorials.com/spearman-rank-correlation/)
- [Bonferroni correction](https://matthew-brett.github.io/teaching/bonferroni_correction.html) (the Šidák correction here is useful for understanding but won't be part of the exam)
- [Holm-Bonferroni correction](https://stats.libretexts.org/Bookshelves/Applied_Statistics/Book%3A_Learning_Statistics_with_R_-_A_tutorial_for_Psychology_Students_and_other_Beginners_(Navarro)/14%3A_Comparing_Several_Means_(One-way_ANOVA)/14.06%3A_Multiple_Comparisons_and_Post_Hoc_Tests) (only sections 14.5.3 and 14.5.4)
- [Multivariate regression basics](https://www.w3schools.com/python/python_ml_multiple_regression.asp)
- [Fixed Effects](https://lost-stats.github.io/Model_Estimation/OLS/fixed_effects_in_linear_regression.html)
- [Clustered standard errors](https://www.statology.org/clustered-standard-errors/).

# Project 1
Open Question:
- something that you got interested in while working with on the project
- get your own data, etc
- idea: what restrictions did the country implement, how did it affect the case numbers, account for them

## Lecture 02 - Map
**Def: Cloropleth map**: A type of thematic map in which a set of predefined areas is colored or patterned in proportion to a statistical variable that represents an aggregate summary of a geographic characteristic within each area
Advantages:
- Familiarity
- Simple
- Easy to read, intuitive

Disadvantages:
-  (All visualizations) Size of bins/colors can be misused (or mishandled by mistake)
- (All visualizations: level of aggregation): If you don't use the right 'resolution' (size of areas), you loose context (e.g large city incorporated into a rural area: final value might not be representative of either)
- Size = importance?! (human perception)
- Forced location (location: one of the most important tools in visualization. Here, you loose the freedom of using it as a tool. But, exactly this is the reason for familiarity)
- Easy to misread

Binning:
- **equally spaced** (same bin size)
- '**equipopulated**': each bins have the same number of observations in them. - almost always a good choice
Algorithms exist that can find natural breaks in the data (like based on clusters, etc)

What about compensating for a variable, like population size, or density:
- A **cartogram** is a thematic map of a set of features, in which their geographic size is altered to be directly proportional to a selected ratio-level variable, such as travel time, population, or GNP. (kinda hard in python)
- Normalize the data (like cases/population)

## Lecture 03 - Associations
#### Correlations
##### Pearson correlation coefficient - r
- Sensitive to outliers
- may or may not indicate causal relationship. Causal relationship may or may not result in correlation.
- Only linear (See [Anscombe's Quartet and Dino GIF](https://www.autodesk.com/research/publications/same-stats-different-graphs))
- Slopes fon't matter: Correlation strength != scale of effect
- Significance != scale of effect
- Significance test (p-value calculation) assumes independent observations (independent and identically distributed variables)

What is a high correlation: Depends: e.g. social sciences <--> physics
Pearson correlation between variables X and Y is calculated by  

![[Pasted image 20220307195457.png]]

  
The formula basically comes down to dividing the covariance by the product of the standard deviations.

(A covariance is basically an _un_standardized correlation. That is: a covariance is a number that indicates to what extent 2 variables are _linearly_ related. In contrast to a (Pearson) correlation, however, a covariance depends on the scales of both variables involved as expressed by their standard deviations.)

#### What to do with non-linear data?:

#####  1. Spearman rank correlation coefficient
- Calculate Pearson correlation on the ranks of values (Does the highest value of X correspond the the highest value of Y? Does the 2nd highest value...)
- Shows monotonous relationships
- Can be used for data that is at least ordinal (ordinal, interval, ratio but not nominal) (ordinal data: categorical, with ordering)
- As Spearman: significance test (p-value calculation) assumes independent observations


 ##### 2. Log transformation (and take Spearman)
 - Care about order of magnitude (not precise values)
 - Get rid of skewedness
 - Can log transform one (either) or both variables (log-log)
 - Ofc check distribution (histogram) to check if it is a good solution. Plot histogram of variable and the log of the variable. If the dist. of the (unmodified) variable is normal --> don't log transform. If the the log-transformed dist. is looks more like a normal dist. --> log transform is probably a good idea


#### Significance and p-value
- The probability of obtaining test results at least as extreme as the results actually observed, under the assumption that the **null hypothesis** is correct.  
- Translation: how likely it is to see this correlation value if there is no relation between X and Y
- Suggests that no statistical relationship and significance exists in a set of given single observed variable, between two sets of observed data and measured phenomena
- Significance treshold (alpha) rule of thumb:
	- 0.05: loose, used in social science (weak, noisy effects)
	- 0.01: social science with many observations
	- 0.001: better benchmark for big data science
	- 5 sigma (3*10-7): physics
- **Related to both the strength of the relationship and the number of observations**
- **NOT** the probability that your hypothesis is untrue. It is the probability the the null hypothesis is true. It doesn't say anything about your hypothesis. The effect could be due to another reason (both the null hypothesis and your hypothesis is untrue)
- Example: h1: there is linear relationship between X and Y. h0: there is not a linear relationship. Skewed data: High p-values because h0 is correct, the relationship is not linear. --> different h1 if you need to use log-log

#### Multiple Hypotheses testing
- If you run X tests, you expect one of them to have 1/X p-value by chance (literal meaning of p-value!)
- possible names: correction for multiple comparisons, simultaneous inference
- aim: FWER, family-wise error rate to be under set treshold (alpha)

##### Bonferroni Correction
- The Bonferroni threshold is a family-wise error threshold. That is, it treats a set of tests as one _family_, and the threshold is designed to control the probability of detecting _any_ positive tests in the family (set) of tests, if the null hypothesis is true.
- if 20 tests will generate a p-value ~0.05 by chance --> that shouldn't be my treshold
- M & M's example: Do they cause cancer? --> p>0.05, no they don't. But only one color causes it? 20 colors, 20 tests, then 0.05 is not the right value. - We are not asking if the hypothesis is true for each color in isolation. We want the confidence that h0 can be rejected for all of them. - The real h0 is not linked to each color independently. h1: the green causes acne. h2: the blue causes acne... h20: the brown causes acne. h0: **None** of h1 .... h20 is true.
- It should be 0.05/20. (alpha/N)
Applies if: Questions are independent. If they aren't, it is too strict.

#### BUT
If **questions are not independent of each other: Bonferroni is too strict:**  (Like weather: temperature and UV-index are not independent)
Many alternatives, one of them:

##### Holm-Bonferroni Correction
- Sort your p-values in ascending order.
- First p-value: p_1 < alpha/N (normal Bonferroni value) (alpha: significance treshold)
- 2nd p-value: p_1 < alpha/(N-1) - Because we know that p1 passes (like we didn't run the previous test: we only care about the remaining)
- and so on ...
- the last p-value will be compared to alpha itself
- As soon as one value fails the test, you reject that, and all subsequent p-values.




## Lecture 04 - Multivariate Regression Analysis
#### OLS - general
Let's say we're interested in predicting var Y, we see strong correlation with X, but both could be dependent on Z (eg X: UV radiation up, Y: corona cases down. But both might be moderated by cultural effects: Good weather --> people go outside --> don't crowd inside). Pearson can't handle it. --> Multivariate regression: Control for Z. What is the effect of X, when X changes but Z doesn't (true effect of X). - Investigate the effect of X keeping Z constant.
- Still investigates **linear relationships**!
- Finding all confounding (Zs) factors is hard.
- Stuffing everything in the model is not a good strategy
- Some controls are bad! 
- Won't tell you the direction of causality

Select the features included in the model. Investigate correlation between variable 'taking away' the explanation power of all the other variables. With all other variables being constant, what is the effect of that variable changing. Why? Example: High correlation between UV radian and corona cases, but maybe a third effect is causing both. Taking away the effect of that, the correlation between UV and corona might be very low.

We need to specifically add constant (also in list of variables)
Constant: baseline rate. Everything else being, what is the expected number of cases. Corresponds to the intercept (where regression line crosses y axes, but we are in multi-dimensional space). (Coefficient will be the slope). (This constant is also sometimes called the intercept). R does this automatically. Statmodels in Python doesn't.

We use **Ordinary Least Squares regression** model (OLS)

Adjusted R^2: (adjusted bc we use several variables - ofc real explanation is more complicated). Estimation of how much of the variation of the y variable are we explaining. Between 0 and 1. 1 would mean that you perfectly predict the result with your variables. Impossible.
Even low R^2 can be interesting but ofc a model with higher R^2 is preferable. As long as you're not over fitting the model or include variables that have a very obvious relationship.
How well the model fits the data, not necessarily that the variables you're interested in are doing a good job.

Coefficients: Relationship of x and y variable. Sign: positive or negative relationship. Number is **not** the tightness of the relationship **but the scale of the effect** --> low value might be caused by the difference in units.

Std.Err: estimated _standard deviation_ of the error. For example if 0 is within 1 standard error (deviation) from the correlation value, we know that we can't reject h0.

t-score: How many standard errors (deviations) is the coefficient from 0? (coefficient divided by std err). The higher the t-score, the lower the p-value.

We can convert t scores to p values (Mark the values corresponding to the t score on the Student t distribution - bell curve but heavier tails than normal dist - and the area under the curve outside of the marked range - towards the tails - is the p-value. Might be a tad more complicated).

p-values: well, p-values...

About cases per capita: We could just use population as a control (variable) (and just take cases as the y variable. By instead calculating cases/capita, we say that we 'know' what the coefficient is: we fix it to be -1. Basically, we constraining our result for the sake of interpretability.

#### Fixed Effects
Sometimes you know that something affected your outcome. But you don't have any measure for it.
Example: Different local governments work differently (strategy, effectiveness, etc). Different regions have different characteristics (density, healthcare etc)

You know that observations belong to specific group -> each group has it's own baseline (the avg of each group is fixed).
Everything that this group differently is captured here.

![[Pasted image 20220310174744.png]]

Corr ~0.8, best fit, but something fishy.

Color each line based on belonging to group and implement fixed effects.
Same slope, different intercept. the real relationship is actually negative!
What is the baseline effect of belonging to that group?

![[Pasted image 20220310174640.png]]


In R, it's automatic, just pass a categorical variable to the regression function
In Python, add a dummy variable, one variable per group. 1 if observation belongs to group, 0 otherwise. Omit one group, the reference group, whose intercept will be captured by the aforementioned constant (see above).

Coefficient tells you the effect of being part of the group. Specifically, the difference between your group and the reference one. Positive coef. -> being in this group is associated with an increase in y compared to the reference group.

If it important to your research question, you can interpret it, but it absorbs everything, so you cannot be sure which characteristic is causing the difference.

BUT most often fixed effect is just a control - put it in, but ignore it's results - we're just abstracting away effects not otherwise studied.

(Is the coefficient a ratio (divide intercept of the region with the intercept of the reference region), or an absolute value? - he didn't know. If you're just using it as a control: doesn't matter.)

#### Clustered Standard Errors (CSE)
![[Pasted image 20220310181010.png]]

Here, you're lying to your model. We tell the model that we have 12 independent observations. Not true! we have 3!

Standard error: How sure are you about the estimation?
![[Pasted image 20220310181319.png]]
More observations -> more confidence
![[Pasted image 20220310181349.png]]
But not if they're part of the same group!
![[Pasted image 20220310181449.png]]

Clustering Standard Errors: doing this operation, we take belonging to group into account.
If new observations are truly independent observations -> CSE won't affect standard error.
R^2 and coefficients won't change. It changes the std.err. (and t, and p)


## Lecture 05 - Interventions

#### Contents:
- Data Scavenging: additional data sources
- Estimating intervention effects
- ??

#### Data Scavenging
Possible sources:
- Wikipedia: like GDP/capita, covid measures like lockdowns (incl. time periods), NLP crawlers etc
- Google Scholar
- Shared data ftom journals (see slides for sources)
- [globaldatalab.org](globaldatalab.org) Global Data Lab: subnational level data, too (eg HDI, health index, gender equality)
- World bank, European institutions
- ourworldindata.org (only country level :( )
- (my own note: Google Database search)
- Stringecy index: 0-100 severity of corona interventions: ourworldindata.org
- covid-19 gov. response tracker bsg.oc.ac.uk (oxford university)
- maybe office of labour statistics etc

```python
# adding stringency index (example)
# when adding database: pandas method: .dropna()
# same line: keep only the data and stringency index, while filtering for country
# how to merge our database w/ stringency database:
df = df.merge(stringency_df, on="date")

# HDI from globaldatalab.org subnational:
# we can drop unnecessary coulmns on the same line as reading the csv: just add
# .drop("coulmn_name", axis=1)

```

stringency index and case numbers: correlation might be positive: high number --> stricter restrictions, not the other way around. --> the case number is a lagging indicator of the effectiveness of the restrictions
removed fixed effect from HDI correlations: same for all dates and regional HDI is part of the fixed effect. Doing both at the same time would make the interpretation of the results extremely hard.
In DK the p for the effect of HDI is extremely low, since it's a fairly homogenous country with relatively low regional differences.

#### Estimating intervention effects
Many effects at once:
- variants
- ebb and flow of pandemics (seasonality)
- individual and collective behaviour (covid burnout)
- weather (also interacts with behaviour)
- vaccines (does not stop transmission but severity - but might have an effect - in this assignment we might omit this)

What type of effect did the intervention cause?
![[Pasted image 20220217110847.png]]

#### Interventions and fixed effects
- Uncertainty about effects: we only know if it's 'on or off', not what it actually did --> one possible implementation: fixed effects:
Dummy variable: column: 1 is when it's on, 0 when it's not
temporal lag: shift observations
How much lag? depends on Y variable (cases --> hospitalization --> deaths) and interventions.
Good testing: almost immediate recording of cases
Research the optimal lag (incubation time, hospitalization, etc)
incorporating level of intervention (like stringency index): not possible with fixed affects
Advantages of using stringency index: more info
Disadvantages: numeric variable: assert linear correlation, which is not necessarily true (spearman might be interesting), we don't know the units: is the change proportional or fixed (is going from 11 --> 12 is the same as 90 --> 91) - discouraged
Hybrid implementation: eg 10 new variables (columns), (10 buckets of stringency index) and value is 1 if the stringency index is at least that bucket. like if the index is 46, then 1, 2, 3, 4th variable is one, 5-10 is 0.
variables could be specific interventions (like offices, non-essential shop closures, restrictions on public effects, travel restrictions) - he got it from the oxford database. In the database the are numerical variables (level from 0 to 3? or 5?) --> here we convert it to 0 or 1 to handle it as fixed effect
(Note: shift weather data too)
idea: weekend or not (use .weekday() method on date formatted date --> result from 0 to 6) maybe add holidays, too

```python


```


change date format
implement lag (transform string to date and do date operation)
![[Pasted image 20220217112920.png]]

## Lecture 6 - Project runthrough

##### Open question: Research Question
- Start with it in the project - why is it useful? Prediction, Govt etc
- we might compare countries

 ##### Task 00 - Data
 
 Data sources:
 - Project Data
 - Additional Dataset(s)
 
 Sanity checks, filtering
 Data wrangling (eg. date _effect: add lag) - before actual analysis

 ##### Task 1 -Univariate / exploratory analysis

 Single variable analysis - exploratory data analysis
 maybe PDF - to check if the distribution is normal or not - if not, maybe log-transform
 (when to log transform??)

 Use PDF to check distribution - if not normal, figure out the correct transformation - if skewed --> probably log-transform
 there are other ways to transform the data
 .. or you can just use Spearman
 (other transformations: not part of curriculum)

 Problem w/ Spearman: unclear how to translate it when you do the multiple regression analysis

 Interventions: not necessarily fixed effects.
 Numeric analysis: problem: if 4 levels (0-3) is 3 3x as strict as 1? - probably they are qualitatively different, not quantitatively diff.
 Idea: transform into 3 diff  fixed effect: let's say level 1: primary schools closed level 2: secondary closed, etc, then 3 binary variable

 ##### Task 2 - Bivariate analysis

 Pairs of variables - typically correlations
 Correct for multiple hypothesis testing

![[Pasted image 20220225170156.png]]
Image: y axis:log hospitalization
x: axis: bins of weather variables
vertical lines: standard deviation or standard error

##### Task 3 - Geographical Visualization

folium or anything else
show the variable that you're using for the analysis - if you aren't using the per capita value: don't use that
Color scale: how to create bins - choose carefully
Bin type examples:
- **equally** spaced (same bin size)

if you have weirdly distributed data: then equally spaced bins might not be the best: some bins might not have any observations in it, or very low number

His color scale: '**equipopulated**': each bins have the same number of observations in them. - almost always a good choice

Algorithms exist that can find natural breaks in the data (like based on clusters, etc)

Over time - but what did he do here? dafuk is this?!
![[Pasted image 20220225172159.png]]

##### Task 4 - Multiple variable analysis

DO IT. 
he did one without one with govt intervention

Discussion: assumptions, limitations, conclusions


### plot with y error bars
During the lecture today, you were interested on how I made the plots with the y error bars in slide 14 of lecture 6.

This snippet should help you:

![Code snippet](https://learnit.itu.dk/tokenpluginfile.php/b5731dd30e42ad89bc7105c26ed12e60/295956/mod_forum/post/70893/Screenshot%20from%202022-03-03%2011-35-49.png)

The comments should be sufficient to understand what is going on. In practice, bin the data, calculate some summary statistic of it, and then use pandas.plot() to make a line chart and pass whatever uncertainty measure you have as the "yerr" argument.

("ax" is the standard variable you get from initializing a grid figure in matplotlib, e.g. "fig, ax = plt.subplots(nrows = 2, ncols = 3, figsize = (18, 8))")


Ideas:
- DONE deal with testing outliers?
- DONE cases/pop and testing comparison? --> rather cases/pop and test/pop
- DONE Fixed effects?
- DONE Clustered standard error
- DONE Bonferoni correction: both UV and log UV? (ok for Bonferroni but not ok for Holm-Bonferroni)
- standard error line plot: per population aggregated the wrong way (mean of cases/pop)
- DONE - log transform tests
- DONE - log transform Weights