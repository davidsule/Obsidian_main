[Our World in Data](ourworldindata.com) - 

## Project 1
Open Question:
- something that you got interested in while working with on the project
- get your own data, etc
- idea: what restrictions did the country implement, how did it affect the case numbers, account for them

Main question:
- Is Covid a seasonal desease?

Ex_01:
- filter by iso3166-2 ??

### Lecture 04 - multivariate regression

```python
from statmodels.api as sm

# something with add constant
# then add constatnt column to df

# OLS
est = sm.OLS
```

fixed effects by region - why does it matter which region we choose as a deadline

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
- globaldatabank.org: subnational level data, too (eg HDI, health index, gender equality)
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