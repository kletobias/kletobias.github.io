---
title: 'SHORT AND EZ EDA Hamburg rental apartments'
date: 2022-01-04 02:00:00
description: 'This part of the Hamburg rental apartments, is about the visualisation of the variables in the dataset.'
featured_image: '/images/putty_ssh.png'
---

# EDA - Hamburg rental apartments
This part of the Hamburg rental apartments, is about the visualisation of the variables in the dataset.
It begins with an explanation of the univariate distribution for each variable in the dataset in Section 1. 
The correlations found between the variables is discussed in Section 2. In the same section, the noise data is analysed
for both day and night and its impact on base rent specifically. What follows in Section 3, is a detailed heat map
of the distribution of variable base rent by statistical area, plotted onto a map of Hamburg.
The last section is Section 4. The general preprocessing done for machine learning is explained and it discusses standardisation of the data,
for the machine learning part that follows afterwards.
***
In order to understand the final data better, either visualisations or summary statistics were created. 
It is about describing the distribution of the variables and about revealing the correlation between them.
Strong correlation between pairs of independent variables can be a sign of the existence of redundant variables. If the correlation is extreme, it may be a sign of collinearity. Both cases pose problems for the analysis of causal relationships between the affected variables and the dependent variable.
The figures showing histograms or bar chart type plots, often have a truncated x-axis range. This range is narrower than the true range of values between the respective minimum and maximum of the variable. This was done, since the omitted values were not visible in the original plots. 
The scale of the plots would have to be bigger, for them to be visible, with the constraint from the screen size this was not possible. 
Please refer to Table 1 for the complete range of values.

### Categorical & Numerical Variables
There are two different types of variables in this work. Namely discrete
categorical variables with few possible values and continuous numerical
variables. The categorical variables used here are `kitchen`,
`elevator`, `balcony`, `status`, `dynamic`, `noise_day`, `noise_night`,
`smaller_0.6`, `const`, `floor`. This kind of variable has categories as
values that have no natural order or
scale(^1) and each listing can fall in
exactly one of the categories for each variable. Since all, but
`noise_day`, `noise_night` were converted to a numerical categorical
variable type, only `noise_day`, `noise_night` are excluded from
Table 1. It is not possible to give the
summaries found in Table 1 for string type variables. The remaining variables have
a natural, numeric scale and are therefore continuous numerical variables.


**Table 1:**

| variable           | count   | mean     | std    | min     | 10%     | 25%     | 50%     | 75%     | 90%      | max     |
|-------------------|--------|---------|-------|--------|--------|--------|--------|--------|---------|--------|
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

