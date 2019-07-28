---
title: EDA - Hamburg rental apartments
date: 2019-07-28 00:00:00
description: This part of the Hamburg rental apartments, is about the visualisation of the variables in the dataset.
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
a natural, numeric scale and are therefore continuous numerical variables [@kuhnAppliedPredictiveModeling2013].

We begin by loading all the neccessary libraries for the analysis.


```python
import os
print(os.getcwd())
```

    /Users/tobiasklein 1/PycharmsProjects/so_deep/theme_for_github_pages/gitub_pages_sources



```python
import geopandas
# import geoplot as gplt
import matplotlib
import matplotlib.pyplot as plt
import missingno as msno
import numpy as np
import pandas as pd
import powerlaw
import seaborn as sns
from pandas import set_option
from pandas.api.types import CategoricalDtype
from scipy import stats
from shapely.wkt import loads

pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 1000)
plt.style.use("science")
```

loading the cleaned dataset with only the final variables, that are going to be used during the machine learning process.


```python
df = pd.read_csv('/Users/tobiasklein 1/PycharmsProjects/so_deep/bachelor_thesis/interim_data/EDA_df_describe.csv')
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>10%</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>90%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>einbau_kue</td>
      <td>9480.0</td>
      <td>0.61</td>
      <td>0.49</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>lift</td>
      <td>9480.0</td>
      <td>0.21</td>
      <td>0.41</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>nebenkosten</td>
      <td>9480.0</td>
      <td>159.08</td>
      <td>83.13</td>
      <td>0.00</td>
      <td>73.00</td>
      <td>100.00</td>
      <td>144.96</td>
      <td>200.00</td>
      <td>265.00</td>
      <td>950.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>lat</td>
      <td>9480.0</td>
      <td>53.57</td>
      <td>0.05</td>
      <td>53.40</td>
      <td>53.49</td>
      <td>53.55</td>
      <td>53.58</td>
      <td>53.60</td>
      <td>53.62</td>
      <td>53.71</td>
    </tr>
    <tr>
      <th>4</th>
      <td>lng</td>
      <td>9480.0</td>
      <td>10.01</td>
      <td>0.09</td>
      <td>9.74</td>
      <td>9.90</td>
      <td>9.96</td>
      <td>10.01</td>
      <td>10.07</td>
      <td>10.13</td>
      <td>10.30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>kaltmiete</td>
      <td>9480.0</td>
      <td>752.89</td>
      <td>446.90</td>
      <td>148.97</td>
      <td>363.23</td>
      <td>451.00</td>
      <td>633.00</td>
      <td>906.00</td>
      <td>1318.37</td>
      <td>5600.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>quadratmeter</td>
      <td>9480.0</td>
      <td>66.20</td>
      <td>26.71</td>
      <td>15.00</td>
      <td>37.21</td>
      <td>49.00</td>
      <td>62.00</td>
      <td>77.93</td>
      <td>97.01</td>
      <td>350.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>anzahl_zimmer</td>
      <td>9480.0</td>
      <td>2.41</td>
      <td>0.88</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>2.00</td>
      <td>2.00</td>
      <td>3.00</td>
      <td>3.50</td>
      <td>8.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>balkon/terasse</td>
      <td>9480.0</td>
      <td>0.68</td>
      <td>0.47</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>etage</td>
      <td>9480.0</td>
      <td>1.98</td>
      <td>1.79</td>
      <td>-1.00</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>3.00</td>
      <td>4.00</td>
      <td>24.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>number_pics</td>
      <td>9480.0</td>
      <td>8.36</td>
      <td>5.58</td>
      <td>0.00</td>
      <td>2.00</td>
      <td>5.00</td>
      <td>7.00</td>
      <td>11.00</td>
      <td>15.00</td>
      <td>64.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>dl_speed</td>
      <td>9480.0</td>
      <td>83.81</td>
      <td>25.92</td>
      <td>6.00</td>
      <td>50.00</td>
      <td>50.00</td>
      <td>100.00</td>
      <td>100.00</td>
      <td>100.00</td>
      <td>200.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ul_speed</td>
      <td>9480.0</td>
      <td>31.11</td>
      <td>13.91</td>
      <td>2.40</td>
      <td>10.00</td>
      <td>10.00</td>
      <td>40.00</td>
      <td>40.00</td>
      <td>40.00</td>
      <td>100.00</td>
    </tr>
    <tr>
      <th>13</th>
      <td>time_gap_uncapped</td>
      <td>9480.0</td>
      <td>12.71</td>
      <td>15.62</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>5.00</td>
      <td>21.00</td>
      <td>38.00</td>
      <td>63.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>status</td>
      <td>9480.0</td>
      <td>2.84</td>
      <td>0.70</td>
      <td>1.00</td>
      <td>2.00</td>
      <td>3.00</td>
      <td>3.00</td>
      <td>3.00</td>
      <td>4.00</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>dynamic</td>
      <td>9480.0</td>
      <td>0.02</td>
      <td>0.28</td>
      <td>-1.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>min_dist</td>
      <td>9480.0</td>
      <td>0.92</td>
      <td>0.84</td>
      <td>0.01</td>
      <td>0.23</td>
      <td>0.37</td>
      <td>0.63</td>
      <td>1.16</td>
      <td>2.06</td>
      <td>9.44</td>
    </tr>
    <tr>
      <th>17</th>
      <td>min_sbahn</td>
      <td>9480.0</td>
      <td>1.79</td>
      <td>1.54</td>
      <td>0.03</td>
      <td>0.40</td>
      <td>0.67</td>
      <td>1.27</td>
      <td>2.46</td>
      <td>3.94</td>
      <td>9.44</td>
    </tr>
    <tr>
      <th>18</th>
      <td>min_ubahn</td>
      <td>9480.0</td>
      <td>2.36</td>
      <td>3.03</td>
      <td>0.01</td>
      <td>0.26</td>
      <td>0.44</td>
      <td>0.92</td>
      <td>2.99</td>
      <td>7.63</td>
      <td>14.17</td>
    </tr>
    <tr>
      <th>19</th>
      <td>smaller_0.6</td>
      <td>9480.0</td>
      <td>0.48</td>
      <td>0.50</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>baujahr_imp</td>
      <td>9480.0</td>
      <td>1966.56</td>
      <td>31.95</td>
      <td>1850.00</td>
      <td>1920.00</td>
      <td>1953.00</td>
      <td>1964.00</td>
      <td>1992.00</td>
      <td>2013.00</td>
      <td>2019.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



**Table 1:**

|variable                   | count  | mean    | std   | min    | 10%    | 25%    | 50%    | 75%    | 90%     | max    |
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

(^1): kuhnAppliedPredictiveModeling2013
