---
title: 'Reading in csv data'
subtitle: 'DS - part 1'
date: 2022-01-08 00:00:00
description: 'This section is about the systemctl command, as found in CentOS 7. It describes and gives examples of its usage.'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

::: {.cell .markdown collapsed="true" pycharm="{\"name\":\"#%% md\\n\"}"}
# Ways to read in csv Data

After being imported, the data is then turned into a `numpy.array()` or a
`pandas.DataFrame()` in the last option covered here.

## Import

Importing Libraries, Modules and Functions

In the following import section, `pandas` is imported using the alias `pd`.
There are some `pd.set_option()` statements to be found in the import section.
These have no effect on the import of the data. They are needed to make the console
output of some commands, such as the descriptive `df.describe()` command more readable.

The actual import statement only imports options, that should be used throughout the file.
The imports specifically needed to execute any of the following statements are added to each code cell.


```python
import pandas as pd
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 70)
```

## The Backup Option

Using Python's `csv` module is an option, that is always available. The `csv` library is a standard
library of python.


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

## Import using numpy - 1

Here, numpy's `loadtxt` module is used to import the locally stored dataset.


```python
from numpy import loadtxt

file = '/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes.csv'
raw_data = open(file, 'rt')
data = loadtxt(raw_data,delimiter= ',')
print(data.shape)
```

(768, 9)


## Import using numpy - 2

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


## Import using Pandas

The favored way to import *csv* files.

Since `numpy` only accepts numerical data, that contains no strings in
any row or column its use is limited to numerical datasets only. `pandas`
is the library used to create and manipulate data in the form of its own table
format called `DataFrame`.
Under the hood it calls `numpy` or other highly efficient libraries to do its
computing, while it extends the tools to import, manipulate and export datasets immensely
compared to `numpy`.

The workflow to import data using `pandas` revolves around its `pandas.read_csv()`
function in the case of a csv file.

### Pandas Import Function

Key Things to remember about `pandas.read_csv()` function:

- By default, the function will process any strings, that could be column `names` present on the first line and
readable for it as the column names of the dataset.
- It is safe practice adding `index_col=None` as an option to the function call, if one does not
want there to be any column that gets used as a column index or several ones for that matter. Like that only
the row index gets built by `pandas`.
- It is a common thing for the resulting `pandas.DataFrame` to be named *df* and
so can be found in many data science source code project files (*like found on [kaggle.com](https://www.kaggle.com/) for example*)


```python
import pandas as pd
from pprint import pprint
df = pd.read_csv(filepath_or_buffer='/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes-with_headers.csv', index_col=None)
print(df.describe().to_markdown())
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

# Ways to read in csv Data

After being imported, the data is then turned into a `numpy.array()` or a
`pandas.DataFrame()` in the last option covered here.

## Import

Importing Libraries, Modules and Functions

In the following import section, `pandas` is imported using the alias `pd`.
There are some `pd.set_option()` statements to be found in the import section.
These have no effect on the import of the data. They are needed to make the console
output of some commands, such as the descriptive `df.describe()` command more readable.

The actual import statement only imports options, that should be used throughout the file.
The imports specifically needed to execute any of the following statements are added to each code cell.


```python
import pandas as pd
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 70)
```

## The Backup Option

Using Python's `csv` module is an option, that is always available. The `csv` library is a standard
library of python.


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

## Import using numpy - 1

Here, numpy's `loadtxt` module is used to import the locally stored dataset.


```python
from numpy import loadtxt

file = '/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes.csv'
raw_data = open(file, 'rt')
data = loadtxt(raw_data,delimiter= ',')
print(data.shape)
```

    (768, 9)


## Import using numpy - 2

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


## Import using Pandas

The favored way to import *csv* files.

Since `numpy` only accepts numerical data, that contains no strings in
any row or column its use is limited to numerical datasets only. `pandas`
is the library used to create and manipulate data in the form of its own table
format called `DataFrame`.
Under the hood it calls `numpy` or other highly efficient libraries to do its
computing, while it extends the tools to import, manipulate and export datasets immensely
compared to `numpy`.

The workflow to import data using `pandas` revolves around its `pandas.read_csv()`
function in the case of a csv file.

### Pandas Import Function

Key Things to remember about `pandas.read_csv()` function:

- By default, the function will process any strings, that could be column `names` present on the first line and
  readable for it as the column names of the dataset.
- It is safe practice adding `index_col=None` as an option to the function call, if one does not
  want there to be any column that gets used as a column index or several ones for that matter. Like that only
  the row index gets built by `pandas`.
- It is a common thing for the resulting `pandas.DataFrame` to be named *df* and
  so can be found in many data science source code project files (*like found on [kaggle.com](https://www.kaggle.com/) for example*)


```python
import pandas as pd
from pprint import pprint
df = pd.read_csv(filepath_or_buffer='/Users/tobias/all_code/projects/python_projects/py_workflows/lessgo/pima-indians-diabetes-with_headers.csv', index_col=None)
print(df.describe().to_markdown())
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


```python
pprint(df.info())
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

