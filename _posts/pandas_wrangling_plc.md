# Wrangling with that Data! /3
We begin by importing the needed libraries and modules.


```python
import numpy as np

import re  # Python built-in regular expression library.

import pandas as pd

seed = 42  # Random seed, to give repeatable random output.
```

## Reading in the DataFrame from the Previous Steps

Values we alter, compared to their default values are the following:

- `na_values=['np.nan`,'[]']
    - In addition to the new label (`np.nan`) for missing values, that we applied at the end of the previous step we can see, that '[]' marks missing values in any of the columns, with a 'json\_' prefix. By marking '[]' values as *NaN* values we can skip a lot of column by column reassignments later. This comes from the design of the web scraping algorithm, that appended an empty list, if there was no value for a variable.
- `index_col=False`
    - The value `False` gets rid of any column assignments by pandas, that would cause `df.index` to be anything different but the simple *int64* range index, that a df has by default. We want that default index.

The output shows what it would look like, if `[]` was not assigned to *NaN*. The two selected columns are a subset of the greater set of columns, that all mark *NaN* values by `[]`, if they are left unchanged.


```python
df = pd.read_csv("../data/df_concat.csv", na_values=["np.nan"], index_col=False)

df[["lat", "lng"]].sample(10, random_state=seed)
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
      <th>lat</th>
      <th>lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9779</th>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>1217</th>
      <td>['lat: 53.59486878110865,']</td>
      <td>['lng: 10.034865006358897']</td>
    </tr>
    <tr>
      <th>5883</th>
      <td>['lat: 53.67059294891176,']</td>
      <td>['lng: 10.009386891198915']</td>
    </tr>
    <tr>
      <th>12069</th>
      <td>['lat: 53.529315016275675,']</td>
      <td>['lng: 9.771992201313864']</td>
    </tr>
    <tr>
      <th>4655</th>
      <td>['lat: 53.59448189788084,']</td>
      <td>['lng: 9.95212036649195']</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>['lat: 53.54201271469222,']</td>
      <td>['lng: 10.106397290234725']</td>
    </tr>
    <tr>
      <th>5382</th>
      <td>['lat: 53.597584833917175,']</td>
      <td>['lng: 10.1536482993936']</td>
    </tr>
    <tr>
      <th>4060</th>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>10762</th>
      <td>[]</td>
      <td>[]</td>
    </tr>
    <tr>
      <th>10120</th>
      <td>[]</td>
      <td>[]</td>
    </tr>
  </tbody>
</table>
</div>



We add `[]` to the labels of *NaN* values, to start cleaning the DataFrame.


```python
df = pd.read_csv("../data/df_concat.csv", na_values=["np.nan", "[]"], index_col=False)

df[["lat", "lng"]].sample(10, random_state=seed)
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
      <th>lat</th>
      <th>lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9779</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1217</th>
      <td>['lat: 53.59486878110865,']</td>
      <td>['lng: 10.034865006358897']</td>
    </tr>
    <tr>
      <th>5883</th>
      <td>['lat: 53.67059294891176,']</td>
      <td>['lng: 10.009386891198915']</td>
    </tr>
    <tr>
      <th>12069</th>
      <td>['lat: 53.529315016275675,']</td>
      <td>['lng: 9.771992201313864']</td>
    </tr>
    <tr>
      <th>4655</th>
      <td>['lat: 53.59448189788084,']</td>
      <td>['lng: 9.95212036649195']</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>['lat: 53.54201271469222,']</td>
      <td>['lng: 10.106397290234725']</td>
    </tr>
    <tr>
      <th>5382</th>
      <td>['lat: 53.597584833917175,']</td>
      <td>['lng: 10.1536482993936']</td>
    </tr>
    <tr>
      <th>4060</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10762</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10120</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## df.regio

The wrangling process begins with the `df.regio` column. At the beginning it holds the values of 3 variables, namely:
- Postal Code
- City
- Neighborhood

Upon looking at the unique values, only the postal code seems to be a somewhat reliably entered variable by the users. Whatever comes after the postal code seems unreliable.
This data comes from user input and there do not seem to be appropriate user input control mechanisms on the website to make sure, that the data is reliable and correct. We
will focus on the gps data anyway, since we need more specific data for each valid listings, than neighborhood an city data.

There is a space separating postal code from the rest of the data in the `df.regio` column. It will allow us to extract the postal code for each listing, that has a valid postal code, using space (" ") as a separator.
We will create a regular expression pattern to make sure, that we only extract valid postal code entries.


```python
df.regio.unique() # Only parts are printed here.
```




    array(['22115 Hamburg Billstedt', '22049 Hamburg Dulsberg',
           '22147 Hamburg Alt-Rahlstedt/Oldenfelde Rahlstedt',
           '22111 Hamburg Horn Hamburg', '22087 Hamburg-Uhlenhorst Hamburg',
           '20457 Hamburg HafenCity Osakaallee 4',
           '20457 Hamburg HafenCity Singapurstraße 5',
           '22041 Hamburg-Wandsbek', '22041 Hamburg-Marienthal',
           '22089 Hamburg-Eilbek Hamm-Nord',
           '22609 Hamburg / Nienstedten Hamburg', '21077 hamburg',
           '20148 Hamburg / Rotherbaum Hamburg', '22399 hamburg Poppenbüttel',
           '22085 hamburg Eilbek', '22337 Hamburg-Ohlsdorf Hamburg',
           '21147 Hamburg', '22087 Hamburg Barmbek-Süd',
           '22299 Winterhude  Winterhude', '21129 Hamburg',
           '22549 Hamburg Bahrenfeld', '21029 Bergedorf Hamburg',
           '20095 Hamburg', '22211 Hamburg Horn', '21039 Hamburg Lohbrügge',
           '22767 Hamburg-St. Pauli Hamburg',
           '21031 Hamburg Lohbrügge Hamburg', '22045 Hamburg Wandsbek',
           '21031 Hamburg-Lohbrügge Hamburg', '22083 Barmbek-Süd Hamburg',
           '20357 Hamburg-Eimsbüttel Hamburg',
           '20257 Hamburg-Eimsbüttel Altona-Nord',
           '20148 Hamburg-Harvestehude', '21033 Hamburg-Lohbrügge Hamburg',
           '22087 Hamburg-Hohenfelde Hamburg',
           '22297 Hamburg-Winterhude Hamburg',
           '22767 Hamburg-Altona/St.Pauli St. Pauli',
           '20097 Hamburg-St. Georg Hammerbrook'], dtype=object)



The `df["regio"]` column is split by whitespace and expanded into two columns. The first part of the expanded column is the *postal code*.
Only the postal code part of the split column is kept. The values for city in the original `regio` column add no information, since all rows of the DataFrame are from within the city of Hamburg.
There is no recurring structure in the data, that gives the neighborhood for each listing. Longitude and Latitude are the values we shall focus on. There will be another postal code like variable, that we will add later. It will be more precise than the postal code of each listing.



We use `match` to validate, that all entries have a valid postalcode.


```python
print(f"Number of rows in the df, before dropna is applied: {len(df)}\n")
df["postal_code"] = df["regio"].str.split(" ", expand=True, n=1)[0]
df = df.dropna(subset=["postal_code"])  # drop rows, where postal code has nan values.
print(f"Number of rows in the df, after dropna is applied: {len(df)}\n")
```

    Number of rows in the df, before dropna is applied: 12325
    
    Number of rows in the df, after dropna is applied: 12324
    


From the output above, we can see, that there was only 1 line with a missing value in the postal code column.


```python
match = [
    m for m in pd.Series(df["postal_code"]) if re.match(r"\A2\d{4}\Z", str(m))
]  # data validation
print(
    f"\nThe number of non-valid postal code entries is: {len(df.postal_code) - len(match)}"
)
```

    
    The number of non-valid postal code entries is: 0


The validation shows, that not only are there no more missing values in the postal code column, but that there are no invalid postal code entries either.

It is good to keep the information below in mind when validating strings using the `re` module.

> Match Objects always have a boolean value of True. Since `match()` and `search()` return a match object, one can test whether there was a match with a simple if statement.

The following example, shows how a match object can be used to validate data. The boolean values are displayed and `assert` is used to check for entries, without a match object.


```python
for mm in np.append(match[0:10], ""):
    if (
        mm
    ):  # if a match was found, the match object exists and it's boolean value is True
        print(bool(mm))
        b = bool(mm)
    else:
        print(bool(mm))
        b = bool(mm)
    assert b == True
```

    True
    True
    True
    True
    True
    True
    True
    True
    True
    True
    False



    ---------------------------------------------------------------------------

    AssertionError                            Traceback (most recent call last)

    Input In [27], in <module>
          8     print(bool(mm))
          9     b = bool(mm)
    ---> 10 assert b == True


    AssertionError: 


Finally, we assign the correct data type to `df["postal_code"]`. It's values are integers, but ordering them or performing arithmetical operations on them makes no sense. Therefore, the column is assigned the dtype *category*.


```python
df["postal_code"] = df["postal_code"].astype("category", errors="raise")
```

That was the second part of 'going from webscrpaing data to tidy DataFrame'.
