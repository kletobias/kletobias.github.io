---
title: EDA - Hamburg rental apartments
date: 2019-07-28 00:00:00
description: This part of the Hamburg rental apartments, is about the visualisation of the variables in the dataset.
accent_color: '#4C60E6'
---

# EDA - Hamburg rental apartments

This part of the Hamburg rental apartments, is about the visualisation of the variables in the dataset.
It begins with an explanation of the univariate distribution for each variable in the dataset in Section 1. 
The correlations found between the variables are discussed in Section 2. In the same section, the noise data is analysed
for both day and night and its impact on base rent specifically. What follows in Section 3, is a detailed heat map
of the distribution of variable base rent by statistical area, plotted onto a map of Hamburg.
The last section is Section 4. The general preprocessing done for machine learning is explained and it discusses standardisation of the data,
for the machine learning part that follows afterwards.

* * *

In order to understand the final data better, either visualisations or summary statistics were created. 
It is about describing the distribution of the variables and about revealing the correlation between them.
Strong correlation between pairs of independent variables can be a sign of the existence of redundant variables. If the correlation is extreme, it may be a sign of collinearity. Both cases pose problems for the analysis of causal relationships between the affected variables and the dependent variable.
The figures showing histograms or bar chart type plots, often have a truncated x-axis range. This range is narrower than the true range of values between the respective minimum and maximum of the variable. This was done, since the omitted values were not visible in the original plots. 
The scale of the plots would have to be bigger, for them to be visible, with the constraint from the screen size this was not possible. 
Please refer to Table 1 for the complete range of values.


**Categorical & Numerical Variables**

There are two different types of variables in this work. Namely discrete
categorical variables with few possible values and continuous numerical
variables. The categorical variables used here are `kitchen`,
`elevator`, `balcony`, `status`, `dynamic`, `noise_day`, `noise_night`,
`smaller_0.6`, `const`, `floor`. This kind of variable has categories as
values that have no natural order or scale [kuhnAppliedPredictiveModeling2013] and each listing can fall in
exactly one of the categories for each variable. Since all, but
`noise_day`, `noise_night` were converted to a numerical categorical
variable type, only `noise_day`, `noise_night` are excluded from
Table 1. It is not possible to give the
summaries found in Table 1 for string type variables. The remaining variables have
a natural, numeric scale and are therefore continuous numerical variables [kuhnAppliedPredictiveModeling2013].

## Univariate Distributions
The variables are shown in Table 1. Here is a description from left to right of what
Table 1 shows. Count is the same for all variables, since this is the final, clean dataset. The mean, is the mean
of the values, given in the unit of the respective variable.

### Binary Categorical Variables
In the case of the binary variables (`kitchen`, `elevator`, `balcony`,
`smaller_0.6`) its value measures the percentage of listings that have
the feature within the dataset. What can be observed for these variables
is:

- `kitchen`: mean = 0.61 $\implies$ 61% of the listings have a fitted kitchen, 39% don't.

- `elevator`: mean = 0.21 $\implies$ 21% of the listings have access to an elevator, 79% don't.

- `balcony`: mean = 0.68 $\implies$ 68% of the listings have a balcony, 32% don't.

- `smaller_0.6`: mean = 0.48 $\implies$ 48% of the listings have access to either a subway or a suburban train station within a radius smaller than 600m, for 52% the distance is equal or greater than 600m.

### Continuous Categorical Variables
Continuing with the other categorical variables shown in
Figure 2, it is visible, that the distribution of `floor` has a mean of close to 2 and has a positive
skew. `floor` is for the majority of observations 1 or 2. The `status`
index is 3 for around 6000 listings and the majority of listings
therefore and is close to the actual values of the "Sozialmonitoring
Bericht 2018" [SozialmonitoringBericht2018]. The same goes for the
`dynamic` index with almost all listing being in areas that have a
stable situation in terms of their status class, again these values are
close to the ones found in the "Sozialmonitoring Bericht 2018".
Looking at `const` the bulk of buildings was built in the period after
World War II (WW II), between 1950 and 1975 roughly. During WW II
(1939-1945) large parts of the city were completely destroyed and so
during the post-war period many buildings had to be rebuilt or newly
constructed [brakmanStrategicBombingGerman2004]. It might show that
`base_rent` of apartments in buildings that were built during that time
have a low `base_rent` value compared with apartments built in different
periods, with similar features. The consideration comes from a simple
supply and demand logic.

There is a sharp downward trend around 1975 to 1990 in the number of
buildings built during that period with a pickup in the Late-1990s. For
several years between 2000-2010 the number decreases once again, to
reach levels as high as the ones seen around 1960 for the period
2010-2018. Right now, there is indication that a relatively high number
of residential buildings are constructed from this sample. This does not
completely align with the data in
Figure Statistikamt Nord [StatistikEinwohnerHaushalte] the maximum of
apartments built between 1990-2017 was in 1995 and the pickup in
construction after 2010 can not reach the levels of that period. The
report of the Statistikamt Nord, however, includes non residential
buildings and construction measures on existing buildings as
well [StatistikEinwohnerHaushalte]. This may hinder a direct comparison
between the here found data from the sample of all listings and their
data. The overall trend however is similar across both data sources.
There are reports that rent prices are rising at the moment in
Hamburg [ndrAktionstagWirdWohnen]. However, not as much as in other
major cities in Germany possibly. This is also due to the fact of a
relatively high number of apartments being constructed at the moment and
a stable population in Hamburg, at least according to the Deutsche Bank
German housing market 2018 (Deutscher Häuser- und Wohnungsmarkt 2018):

> In Hamburg, housing prices in the portfolio have risen by more than
> 70% since 2009. Rents are growing at a below-average rate compared
> with other major cities. The relatively brisk construction activity
> and the stable number of inhabitants are dampening rental dynamics.
> Low interest rates could therefore be the main driver for Hamburg's
> housing and house prices. Correspondingly, interest rate sensitivity
> could be higher than in other metropolises. In our baseline scenario,
> we expect mortgage rates to rise only slightly in 2018. House and
> apartment prices in Hamburg should therefore continue to rise strongly
> in the current year. [mobertDeutscherHauserUnd2018]

*Original German version was translated to English by the Author*

For the prediction important is that there might be relevant rent
increases for comparable apartments between the beginning of the
timeframe in July 2016 and the end in November 2018, that might degrade
prediction accuracy. `smaller_0.6`, the last variable in
Figure 2 is discussed at the beginning of this Section with the other binary variables. 
Continuing with the numerical variables and their histograms in
Figure 3, variable `base_rent` shows a pronounced positive skew in the data series. The mean
($\bar{x}$) of 753 Euro for the series is low considering the value
range of 149-5600 Euro. However, extreme values above 1318.37 Euro only
account for 10% of the data. The standard deviation of 447 Euro is a
better metric to show the large spread of this variable. The one Sigma
(${s}$) interval has limits (Eur.)
$[306 = \bar{x}-{s},\bar{x}+{s} = 1200]$, with the lower limit
$\approx 40\%$ of $\bar{x}$ and the upper limit $\approx 160\%$ of
$\bar{x}$. A similar pattern is observed for ancillary costs
(`ancil_costs`), with the distribution exhibiting a bit less skew and a
more linear falloff past the 130 Euro mark. Since the determination of
ancillary costs is not uniformly established regarding the costs
contained within them, it is difficult to consider them as a consistent
variable. Square meters (`sqm`) has a gaussian distribution like value
distribution with a slight positive skew. The mean is $\bar{x} = 66$
with the one Sigma interval, given in $m^2$, of $[39, 93]$. This echoes
the slight skewness for the series. The number of images that are
uploaded to describe the apartment seem to be important, since the
highest frequency found around 5 to 10 images and not zero. There are
less than 10% of observations with 0 images, as can be seen in
Table 1. The download (`dl_speed`) and upload speed (`ul_speed`) variables show that for both variables,
observations gather around a few mbit/s values. With these findings they
have to be considered categorical variables, as the value range is not
continuous for the listings in the series. For `dl_speed` these are
(mbit/s, count): (100, 6404), (50, 2105), (83, 484), (16, 453), (25,
36), (200, 5), (6, 2). For `ul_speed`: (40, 6404), (10, 2105), (31,
528), (2.4, 447), (100, 5). It is noticeable that for the majority of
observations tuples can be formed from values of both variables that
have near identical counts in the series. The variable measuring the
days a listing was online on the platform shows that there was strong
demand for the apartments in this series, since 25% of the data series
was listed and delisted within two days, thus having the `time_gap` = 1
day value. 10% have a value of 0 days, meaning that they were online for
less than 24 hours. The median is one week, see
Table 1. There are values as high as 924 days in the series, however the portion of values 59 ≤ time_gap ≤ 924 makes up the highest 10% of all values for `time_gap`.
Therefore, the impact is expected to be small on the prediction results, if there were outliers amongst these values. The minimum distance (`min_dist`) to either of subway or
suburban train station shows that for 70.5% of observations the distance
is $\leq 1$ km and the median (50% quantile) is 0.63 km. This is in
accordance with the observations described for variable `smaller_0.6`,
where 48% had a distance of less than 0.6 km. With the 50% quantile at
0.63 km it shows, that the binary variable `smaller_0.6` splits the set
of observations into two almost equal parts. The distributions of the
variables `min_train`, `min_subway` show a very similar picture. Since
the variable `min_dist` is set to the smaller value of the two, its
distribution is a concentration of the smallest values of the two. One
can see that the distance to the nearest subway station has a high
concentration of values close to zero and a sudden drop after
approximately 1 km. In the case of the nearest suburban train station
the distribution is shifted towards the mean of 2.36 km and falls off
more slowly afterwards.

**Table 1:**

| variable          | count  | mean    | std   | min    | 10%    | 25%    | 50%    | 75%    | 90%     | max    |
| ----------------- | ------ | ------- | ----- | ------ | ------ | ------ | ------ | ------ | ------- | ------ |
| einbau_kue        | 9480.0 | 0.61    | 0.49  | 0.0    | 0.0    | 0.0    | 1.0    | 1.0    | 1.0     | 1.0    |
| lift              | 9480.0 | 0.21    | 0.41  | 0.0    | 0.0    | 0.0    | 0.0    | 0.0    | 1.0     | 1.0    |
| nebenkosten       | 9480.0 | 159.08  | 83.13 | 0.0    | 73.0   | 100.0  | 144.96 | 200.0  | 265.0   | 950.0  |
| lat               | 9480.0 | 53.57   | 0.05  | 53.4   | 53.49  | 53.55  | 53.58  | 53.6   | 53.62   | 53.71  |
| lng               | 9480.0 | 10.01   | 0.09  | 9.74   | 9.9    | 9.96   | 10.01  | 10.07  | 10.13   | 10.3   |
| kaltmiete         | 9480.0 | 752.89  | 446.9 | 148.97 | 363.23 | 451.0  | 633.0  | 906.0  | 1318.37 | 5600.0 |
| quadratmeter      | 9480.0 | 66.2    | 26.71 | 15.0   | 37.21  | 49.0   | 62.0   | 77.93  | 97.01   | 350.0  |
| anzahl_zimmer     | 9480.0 | 2.41    | 0.88  | 1.0    | 1.0    | 2.0    | 2.0    | 3.0    | 3.5     | 8.0    |
| balkon/terasse    | 9480.0 | 0.68    | 0.47  | 0.0    | 0.0    | 0.0    | 1.0    | 1.0    | 1.0     | 1.0    |
| etage             | 9480.0 | 1.98    | 1.79  | -1.0   | 0.0    | 1.0    | 1.0    | 3.0    | 4.0     | 24.0   |
| number_pics       | 9480.0 | 8.36    | 5.58  | 0.0    | 2.0    | 5.0    | 7.0    | 11.0   | 15.0    | 64.0   |
| dl_speed          | 9480.0 | 83.81   | 25.92 | 6.0    | 50.0   | 50.0   | 100.0  | 100.0  | 100.0   | 200.0  |
| ul_speed          | 9480.0 | 31.11   | 13.91 | 2.4    | 10.0   | 10.0   | 40.0   | 40.0   | 40.0    | 100.0  |
| time_gap_uncapped | 9480.0 | 12.71   | 15.62 | 0.0    | 0.0    | 1.0    | 5.0    | 21.0   | 38.0    | 63.0   |
| status            | 9480.0 | 2.84    | 0.7   | 1.0    | 2.0    | 3.0    | 3.0    | 3.0    | 4.0     | 4.0    |
| dynamic           | 9480.0 | 0.02    | 0.28  | -1.0   | 0.0    | 0.0    | 0.0    | 0.0    | 0.0     | 1.0    |
| min_dist          | 9480.0 | 0.92    | 0.84  | 0.01   | 0.23   | 0.37   | 0.63   | 1.16   | 2.06    | 9.44   |
| min_sbahn         | 9480.0 | 1.79    | 1.54  | 0.03   | 0.4    | 0.67   | 1.27   | 2.46   | 3.94    | 9.44   |
| min_ubahn         | 9480.0 | 2.36    | 3.03  | 0.01   | 0.26   | 0.44   | 0.92   | 2.99   | 7.63    | 14.17  |
| smaller_0.6       | 9480.0 | 0.48    | 0.5   | 0.0    | 0.0    | 0.0    | 0.0    | 1.0    | 1.0     | 1.0    |
| baujahr_imp       | 9480.0 | 1966.56 | 31.95 | 1850.0 | 1920.0 | 1953.0 | 1964.0 | 1992.0 | 2013.0  | 2019.0 |
