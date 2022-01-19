---
title: 'Reading in csv data' 
subtitle: 'DS - part 1'
date: 2022-01-08 00:00:00
description: 'This section is about the systemctl command, as found in CentOS 7. It describes and gives examples of its usage.'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg' 
accent_color: '#08877d'
---

# Ways to read in csv Data

After being imported, the data is then turned into a `numpy.array()`.

## Using Python's *csv* module


```python
import csv
import numpy as np
file = '/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes.csv'
raw_data = open(file,'rt')
reader = csv.reader(raw_data, delimiter=',', quoting=csv.QUOTE_NONE)
x = list(reader)
data = np.array(x).astype('float')
print(data.shape)
```

(768, 9)


From the output one can tell, that the dataset has 768 rows and 9 columns.

## Loading csv file with Numpy - 1

Here, numpy's `loadtxt` module is used to import the locally stored dataset.


```python
from numpy import loadtxt

file = '/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes.csv'
raw_data = open(file, 'rt')
data = loadtxt(raw_data,delimiter= ',')
print(data.shape)
```

(768, 9)


## Loading csv file with Numpy - 2

This time the data is downloaded directly from a *URL*, that is being
handled by the function `urlopen`, that is part of the python built in
`module urllib.request` module.

Note: *The first row has to be skipped, cause it contains strings. This is a pima indians version where headers are already added in the first row.*


```python
from numpy import loadtxt
from urllib.request import urlopen
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/diabetes.csv"
raw_data = urlopen(url)
dataset = loadtxt(raw_data,delimiter=',', skiprows=1)
print(dataset.shape)
```

(768, 9)


## The favored Way to load in *csv* Files

Since `Numpy` only accepts numerical data, that contains no strings in
any row and column its use is limited to numerical datasets only. `Pandas`
is the library used to create and manipulate data in the form of its own table
format called `DataFrame`.
Under the hood it calls `Numpy` or other highly efficient libraries to do its
computing, while it extends the tools to import and manipulate datasets from a
number of sources.

The workflow to import data using `Pandas` revolves around its `pandas.read_csv()`
function in the case of a csv file.

### Key Things to remember about *pandas.read_csv()* function

- By default, the function will process any column `names` present in the dataset.
That means headers only get specified, if they are missing by adding `headers=0`
usually.
- It is safe practice adding `index_col=None` as an option to the function call, if one does not
want there to be any column that gets used as a column index or several ones. Like that only
the row index gets built by `pandas`
- It is a common thing for the resulting `pandas.DataFrame` to be named *df* and
so can be found in many data science source code project files (*like found on [kaggle.com](https://www.kaggle.com/) for example*)

In the following example, there are some `.set_option()` to be found. These have no
effect for the import of the data. They are needed to make the output of the
`.describe()` statement more readable.

The actual import statement looks like this:



```python
import pandas as pd
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 1000)
df = pd.read_csv(filepath_or_buffer='/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes-with_headers.csv', index_col=None)
print(df.describe())
```

```
Pregnancies     Glucose  BloodPressure  SkinThickness     Insulin         BMI  DiabetesPedigreeFunction         Age     Outcome
count   768.000000  768.000000     768.000000     768.000000  768.000000  768.000000                768.000000  768.000000  768.000000
mean      3.845052  120.894531      69.105469      20.536458   79.799479   31.992578                  0.471876   33.240885    0.348958
std       3.369578   31.972618      19.355807      15.952218  115.244002    7.884160                  0.331329   11.760232    0.476951
min       0.000000    0.000000       0.000000       0.000000    0.000000    0.000000                  0.078000   21.000000    0.000000
25%       1.000000   99.000000      62.000000       0.000000    0.000000   27.300000                  0.243750   24.000000    0.000000
50%       3.000000  117.000000      72.000000      23.000000   30.500000   32.000000                  0.372500   29.000000    0.000000
75%       6.000000  140.250000      80.000000      32.000000  127.250000   36.600000                  0.626250   41.000000    1.000000
max      17.000000  199.000000     122.000000      99.000000  846.000000   67.100000                  2.420000   81.000000    1.000000
```


```python
df.info()
```
```log
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 768 entries, 0 to 767
Data columns (total 9 columns):
#   Column                    Non-Null Count  Dtype  
---  ------                    --------------  -----  
0   Pregnancies               768 non-null    int64  
1   Glucose                   768 non-null    int64  
2   BloodPressure             768 non-null    int64  
3   SkinThickness             768 non-null    int64  
4   Insulin                   768 non-null    int64  
5   BMI                       768 non-null    float64
6   DiabetesPedigreeFunction  768 non-null    float64
7   Age                       768 non-null    int64  
8   Outcome                   768 non-null    int64  
dtypes: float64(2), int64(7)
memory usage: 54.1 KB
```


# Ways to read in csv Data

After being imported, the data is then turned into a `numpy.array()`.

## Importing Libraries, Modules and Functions


```python
import pandas as pd
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 70)
```

## Using Python's *csv* module


```python
import csv
import numpy as np
file = '/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes.csv'
raw_data = open(file,'rt')
reader = csv.reader(raw_data, delimiter=',', quoting=csv.QUOTE_NONE)
x = list(reader)
data = np.array(x).astype('float')
print(data.shape)
```

(768, 9)


From the output one can tell, that the dataset has 768 rows and 9 columns.

## Loading csv file with Numpy - 1

Here, numpy's `loadtxt` module is used to import the locally stored dataset.


```python
from numpy import loadtxt

file = '/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes.csv'
raw_data = open(file, 'rt')
data = loadtxt(raw_data,delimiter= ',')
print(data.shape)
```

(768, 9)


## Loading csv file with Numpy - 2

This time the data is downloaded directly from a *URL*, that is being
handled by the function `urlopen`, that is part of the python built in
`module urllib.request` module.

Note: *The first row has to be skipped, cause it contains strings. This is a pima indians version where headers are already added in the first row.*


```python
from numpy import loadtxt
from urllib.request import urlopen
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0101EN-SkillsNetwork/labs/Module%205/data/diabetes.csv"
raw_data = urlopen(url)
dataset = loadtxt(raw_data,delimiter=',', skiprows=1)
print(dataset.shape)
```

(768, 9)


## The favored Way to load in *csv* Files

Since `Numpy` only accepts numerical data, that contains no strings in
any row and column its use is limited to numerical datasets only. `Pandas`
is the library used to create and manipulate data in the form of its own table
format called `DataFrame`.
Under the hood it calls `Numpy` or other highly efficient libraries to do its
computing, while it extends the tools to import and manipulate datasets from a
number of sources.

The workflow to import data using `Pandas` revolves around its `pandas.read_csv()`
function in the case of a csv file.

### Key Things to remember about *pandas.read_csv()* function

- By default, the function will process any column `names` present in the dataset.
That means headers only get specified, if they are missing by adding `headers=0`
usually.
- It is safe practice adding `index_col=None` as an option to the function call, if one does not
want there to be any column that gets used as a column index or several ones. Like that only
the row index gets built by `pandas`
- It is a common thing for the resulting `pandas.DataFrame` to be named *df* and
so can be found in many data science source code project files (*like found on [kaggle.com](https://www.kaggle.com/) for example*)

In the following example, there are some `.set_option()` to be found. These have no
effect for the import of the data. They are needed to make the output of the
`.describe()` statement more readable.

The actual import statement looks like this:



```python
import pandas as pd
from pprint import pprint
df = pd.read_csv(filepath_or_buffer='/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes-with_headers.csv', index_col=None)
pprint(df.describe())
```

Pregnancies     Glucose  BloodPressure  SkinThickness  \
count   768.000000  768.000000     768.000000     768.000000   
mean      3.845052  120.894531      69.105469      20.536458   
std       3.369578   31.972618      19.355807      15.952218   
min       0.000000    0.000000       0.000000       0.000000   
25%       1.000000   99.000000      62.000000       0.000000   
50%       3.000000  117.000000      72.000000      23.000000   
75%       6.000000  140.250000      80.000000      32.000000   
max      17.000000  199.000000     122.000000      99.000000   

Insulin         BMI  DiabetesPedigreeFunction         Age  \
count  768.000000  768.000000                768.000000  768.000000   
mean    79.799479   31.992578                  0.471876   33.240885   
std    115.244002    7.884160                  0.331329   11.760232   
min      0.000000    0.000000                  0.078000   21.000000   
25%      0.000000   27.300000                  0.243750   24.000000   
50%     30.500000   32.000000                  0.372500   29.000000   
75%    127.250000   36.600000                  0.626250   41.000000   
max    846.000000   67.100000                  2.420000   81.000000   

Outcome  
count  768.000000  
mean     0.348958  
std      0.476951  
min      0.000000  
25%      0.000000  
50%      0.000000  
75%      1.000000  
max      1.000000  



```python
pprint(df.info())
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 768 entries, 0 to 767
Data columns (total 9 columns):
#   Column                    Non-Null Count  Dtype  
---  ------                    --------------  -----  
0   Pregnancies               768 non-null    int64  
1   Glucose                   768 non-null    int64  
2   BloodPressure             768 non-null    int64  
3   SkinThickness             768 non-null    int64  
4   Insulin                   768 non-null    int64  
5   BMI                       768 non-null    float64
6   DiabetesPedigreeFunction  768 non-null    float64
7   Age                       768 non-null    int64  
8   Outcome                   768 non-null    int64  
dtypes: float64(2), int64(7)
memory usage: 54.1 KB
None
```




|       |   Pregnancies |   Glucose |   BloodPressure |   SkinThickness |   Insulin |       BMI |   DiabetesPedigreeFunction |      Age |    Outcome |
|:------|--------------:|----------:|----------------:|----------------:|----------:|----------:|---------------------------:|---------:|-----------:|
| count |     768       |  768      |        768      |        768      |  768      | 768       |                 768        | 768      | 768        |
| mean  |       3.84505 |  120.895  |         69.1055 |         20.5365 |   79.7995 |  31.9926  |                   0.471876 |  33.2409 |   0.348958 |
| std   |       3.36958 |   31.9726 |         19.3558 |         15.9522 |  115.244  |   7.88416 |                   0.331329 |  11.7602 |   0.476951 |
| min   |       0       |    0      |          0      |          0      |    0      |   0       |                   0.078    |  21      |   0        |
| 25%   |       1       |   99      |         62      |          0      |    0      |  27.3     |                   0.24375  |  24      |   0        |
| 50%   |       3       |  117      |         72      |         23      |   30.5    |  32       |                   0.3725   |  29      |   0        |
| 75%   |       6       |  140.25   |         80      |         32      |  127.25   |  36.6     |                   0.62625  |  41      |   1        |
| max   |      17       |  199      |        122      |         99      |  846      |  67.1     |                   2.42     |  81      |   1        |



<table border="0" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Pregnancies</th>
      <th>Glucose</th>
      <th>BloodPressure</th>
      <th>SkinThickness</th>
      <th>Insulin</th>
      <th>BMI</th>
      <th>DiabetesPedigreeFunction</th>
      <th>Age</th>
      <th>Outcome</th>
  </tr>
</thead>
<tbody>
    <tr>
      <th>count</th>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
      <td>768.000000</td>
  </tr>
  <tr>
      <th>mean</th>
      <td>3.845052</td>
      <td>120.894531</td>
      <td>69.105469</td>
      <td>20.536458</td>
      <td>79.799479</td>
      <td>31.992578</td>
      <td>0.471876</td>
      <td>33.240885</td>
      <td>0.348958</td>
  </tr>
  <tr>
      <th>std</th>
      <td>3.369578</td>
      <td>31.972618</td>
      <td>19.355807</td>
      <td>15.952218</td>
      <td>115.244002</td>
      <td>7.884160</td>
      <td>0.331329</td>
      <td>11.760232</td>
      <td>0.476951</td>
  </tr>
  <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.078000</td>
      <td>21.000000</td>
      <td>0.000000</td>
  </tr>
  <tr>
      <th>25%</th>
      <td>1.000000</td>
      <td>99.000000</td>
      <td>62.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>27.300000</td>
      <td>0.243750</td>
      <td>24.000000</td>
      <td>0.000000</td>
  </tr>
  <tr>
      <th>50%</th>
      <td>3.000000</td>
      <td>117.000000</td>
      <td>72.000000</td>
      <td>23.000000</td>
      <td>30.500000</td>
      <td>32.000000</td>
      <td>0.372500</td>
      <td>29.000000</td>
      <td>0.000000</td>
  </tr>
  <tr>
      <th>75%</th>
      <td>6.000000</td>
      <td>140.250000</td>
      <td>80.000000</td>
      <td>32.000000</td>
      <td>127.250000</td>
      <td>36.600000</td>
      <td>0.626250</td>
      <td>41.000000</td>
      <td>1.000000</td>
  </tr>
  <tr>
      <th>max</th>
      <td>17.000000</td>
      <td>199.000000</td>
      <td>122.000000</td>
      <td>99.000000</td>
      <td>846.000000</td>
      <td>67.100000</td>
      <td>2.420000</td>
      <td>81.000000</td>
      <td>1.000000</td>
  </tr>
</tbody>
</table>
