---
title: 'Wrangling Data'
subtitle: 'With Pandas from Raw Webscraping Data to Tidy DataFrame.'
date: 2022-03-09 00:00:00
description: 'Various features were extracted from the listings through the use of webscraping and it is the main objective at this stage to clean and construct a tidy DataFrame, that is ready for the following stages.'
featured_image: 'mT68055%25%25--tYF_5__5jhhh5pls$0-G.jpeg'
gallery_images: 'YtOk89__87-kbtTGW$DD-L.jpeg'
accent_color: '#08877d'
---

# From Raw Webscraping Data to Tidy Pandas DataFrame

Importing the necessary modules

```python
import pandas as pd  # The library used to manipulate and to create a tidy DataFrame object
import matplotlib.pyplot as plt  # The main library used for any kind of data visualization
import numpy as np  # numpy is needed throughout the cleaning and plotting process
import re  # Adds regular expression functionality

plt.style.use('science')  # Use a custom template for styling plots
```

## Reading In the Input Data

The input data is split into 3 csv files, that together capture all rental listings that were online and within the boundaries of the city of Hamburg at the time of scraping the data. The source was a
large German rental listing site called 'Immoscout24'. [ImmoScout24 - https://www.immobilienscout24.de](https://www.immobilienscout24.de/) is their official brand name and URL.

Various features were extracted from the listings through the use of webscraping and it is the main objective at this stage to clean and construct a tidy DataFrame, that is ready for the following
stages. A brief overview of the following stages is given below.

- Feature Engineering - Adding location based features
- EDA - Exploratory Data Analysis
- Machine Learning - Fitting and tuning 2 models, then predicting the value of variable 'base rent'
- Analyzing & Discussing the results

Back to the task at hand, we begin by reading in the csv files and creating the Pandas (*pd*) DataFrame object. Throughout this article, any Pandas DataFrame object will be assigned to a variable that
always contains the letters 'df', plus any prefix or suffix, preceding or succeeding the letters 'df' in some cases.

The path to the input data is assigned to variables `scraping_{1..3}`. For each of them a DataFrame object is created afterwards. The DataFrame `df`, which holds the data of all three is created and
duplicate rows are dropped. The command used to drop any possibly duplicate rows is `df.drop_duplicates()` without any specifying further parameters as to the subset of columns to consider when
determining, if two rows are identical. Like that, only such rows are dropped, that have identical values for all variables found in the dataset. This was mainly done to get rid of overlapping page
ranges from the scraping part and also to get rid of duplicate listings on the website.

```python
scraping_1 = "../data/20181203-first_scraping_topage187.csv"
scraping_2 = "../data/20181203-second_scraping_topage340.csv"
scraping_3 = "../data/20181203-third_scraping_topage340.csv"

df1 = pd.read_csv(scraping_1, index_col=False, parse_dates=False)
df2 = pd.read_csv(scraping_2, index_col=False, parse_dates=False)
df3 = pd.read_csv(scraping_3, index_col=False, parse_dates=False)

df = df1.append([df2, df3], ignore_index=True)
del df["Unnamed: 0"]
df = df.drop_duplicates()
```

## First Look at the DataFrame

To get a first look at the newly create DataFrame `df`, one can choose between multiple tools in the pandas library. It is assumed, that the Dataframe is named `df` in the following, as a couple of
the tools, the pandas library has to offer, are described and links to the documentation page of each command are added for more detail on how each command works.

- `df.head()` - [pandas.DataFrame.head — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.head.html)
- The counterpart of `df.head()` is `df.tail()` - [pandas.DataFrame.tail — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.tail.html)
- `df.columns` - [pandas.DataFrame.columns — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.columns.html)
- `df.index` - [pandas.DataFrame.index — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.index.html)
- `df.describe()` - [pandas.DataFrame.describe — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.describe.html)
- `df.shape` - [pandas.DataFrame.shape — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.shape.html)
- `df.count()` - [pandas.DataFrame.count — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.count.html)
- `df.nunique()` - [pandas.DataFrame.nunique — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.nunique.html)
- `df.value_counts()` - [pandas.DataFrame.value_counts — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.value_counts.html)
- `df.filter()` - [pandas.DataFrame.filter — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.filter.html)
- `df.sample()` - [pandas.DataFrame.sample — pandas documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sample.html)

### Commands

`df.head()`

**Description -** The command `df.head()`returns the first 5 rows of the DataFrame by default, if no parameters are specified by the user. Using the parameter *n*, one can specify the number of rows,
that get returned. Needless to say, rows returned will always start at the first index value and include the following *n-1* rows.

**Example -** In the first call to `df.head()`, the default value for number of lines printed (*n*=5) is used by not specifying any parameter value in the function call. In the second call, the number
of lines printed is changed to *n*=9.

```python
df.head()  # Includes index values [0:4], which is default (n=5)
```

<div style="width:656px;overflow-x:scroll;">

<table>
  <thead>
    <tr>
      <th></th>
      <th>einbau_kue</th>
      <th>lift</th>
      <th>nebenkosten</th>
      <th>gesamt_miete</th>
      <th>heiz_kosten</th>
      <th>lat</th>
      <th>lng</th>
      <th>str</th>
      <th>nutzf</th>
      <th>regio</th>
      <th>...</th>
      <th>json_firingTypes</th>
      <th>json_hasKitchen</th>
      <th>json_cellar</th>
      <th>json_yearConstructedRange</th>
      <th>json_baseRent</th>
      <th>json_livingSpace</th>
      <th>json_condition</th>
      <th>json_interiorQual</th>
      <th>json_petsAllowed</th>
      <th>json_lift</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>190,84</td>
      <td>541,06</td>
      <td>inkl. 78 €</td>
      <td>['lat: 53.52943934146104,']</td>
      <td>['lng: 10.152357145948395']</td>
      <td>Strietkoppel 20</td>
      <td>NaN</td>
      <td>22115 Hamburg Billstedt</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"3"']</td>
      <td>['"obj_baseRent":"350.22"']</td>
      <td>['"obj_livingSpace":"76"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>117,95</td>
      <td>559,05</td>
      <td>inkl. 52,07 €</td>
      <td>['lat: 53.58414266878421,']</td>
      <td>['lng: 10.06842724545814']</td>
      <td>Naumannplatz 2</td>
      <td>NaN</td>
      <td>22049 Hamburg Dulsberg</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"1"']</td>
      <td>['"obj_baseRent":"441.1"']</td>
      <td>['"obj_livingSpace":"60"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>249,83</td>
      <td>839,01</td>
      <td>inkl. 110,58 €</td>
      <td>['lat: 53.6044918821393,']</td>
      <td>['lng: 9.86423115803761']</td>
      <td>Warthestr. 52a</td>
      <td>NaN</td>
      <td>22547 Hamburg Lurup</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"5"']</td>
      <td>['"obj_baseRent":"589.18"']</td>
      <td>['"obj_livingSpace":"75"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>70</td>
      <td>665  (zzgl. Heizkosten)</td>
      <td>nicht in Nebenkosten enthalten</td>
      <td>['lat: 53.56394970119381,']</td>
      <td>['lng: 9.956881419437474']</td>
      <td>Oelkersallee 53</td>
      <td>NaN</td>
      <td>22769 Hamburg Altona-Nord</td>
      <td>...</td>
      <td>['"obj_firingTypes":"no_information"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"595"']</td>
      <td>['"obj_livingSpace":"46"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>213,33</td>
      <td>651,81</td>
      <td>inkl. 57,78 €</td>
      <td>['lat: 53.60180649336605,']</td>
      <td>['lng: 10.081257248271337']</td>
      <td>Haldesdorfer Str. 119a</td>
      <td>NaN</td>
      <td>22179 Hamburg Bramfeld</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"6"']</td>
      <td>['"obj_baseRent":"438.48"']</td>
      <td>['"obj_livingSpace":"52"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 47 columns</p>

</div>

```python
df.head(n=9)  # Includes index values [0:8]
```

<div style="width:656px;overflow-x:scroll;">

<table>
  <thead>
    <tr>
      <th></th>
      <th>einbau_kue</th>
      <th>lift</th>
      <th>nebenkosten</th>
      <th>gesamt_miete</th>
      <th>heiz_kosten</th>
      <th>lat</th>
      <th>lng</th>
      <th>str</th>
      <th>nutzf</th>
      <th>regio</th>
      <th>...</th>
      <th>json_firingTypes</th>
      <th>json_hasKitchen</th>
      <th>json_cellar</th>
      <th>json_yearConstructedRange</th>
      <th>json_baseRent</th>
      <th>json_livingSpace</th>
      <th>json_condition</th>
      <th>json_interiorQual</th>
      <th>json_petsAllowed</th>
      <th>json_lift</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>190,84</td>
      <td>541,06</td>
      <td>inkl. 78 €</td>
      <td>['lat: 53.52943934146104,']</td>
      <td>['lng: 10.152357145948395']</td>
      <td>Strietkoppel 20</td>
      <td>NaN</td>
      <td>22115 Hamburg Billstedt</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"3"']</td>
      <td>['"obj_baseRent":"350.22"']</td>
      <td>['"obj_livingSpace":"76"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>117,95</td>
      <td>559,05</td>
      <td>inkl. 52,07 €</td>
      <td>['lat: 53.58414266878421,']</td>
      <td>['lng: 10.06842724545814']</td>
      <td>Naumannplatz 2</td>
      <td>NaN</td>
      <td>22049 Hamburg Dulsberg</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"1"']</td>
      <td>['"obj_baseRent":"441.1"']</td>
      <td>['"obj_livingSpace":"60"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>249,83</td>
      <td>839,01</td>
      <td>inkl. 110,58 €</td>
      <td>['lat: 53.6044918821393,']</td>
      <td>['lng: 9.86423115803761']</td>
      <td>Warthestr. 52a</td>
      <td>NaN</td>
      <td>22547 Hamburg Lurup</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"5"']</td>
      <td>['"obj_baseRent":"589.18"']</td>
      <td>['"obj_livingSpace":"75"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>70</td>
      <td>665  (zzgl. Heizkosten)</td>
      <td>nicht in Nebenkosten enthalten</td>
      <td>['lat: 53.56394970119381,']</td>
      <td>['lng: 9.956881419437474']</td>
      <td>Oelkersallee 53</td>
      <td>NaN</td>
      <td>22769 Hamburg Altona-Nord</td>
      <td>...</td>
      <td>['"obj_firingTypes":"no_information"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"595"']</td>
      <td>['"obj_livingSpace":"46"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>213,33</td>
      <td>651,81</td>
      <td>inkl. 57,78 €</td>
      <td>['lat: 53.60180649336605,']</td>
      <td>['lng: 10.081257248271337']</td>
      <td>Haldesdorfer Str. 119a</td>
      <td>NaN</td>
      <td>22179 Hamburg Bramfeld</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"6"']</td>
      <td>['"obj_baseRent":"438.48"']</td>
      <td>['"obj_livingSpace":"52"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>150</td>
      <td>890</td>
      <td>inkl. 90 €</td>
      <td>['lat: 53.561192834080046,']</td>
      <td>['lng: 10.032298671585043']</td>
      <td>Elisenstraße 13</td>
      <td>8 m²</td>
      <td>22087 Hamburg Hohenfelde</td>
      <td>...</td>
      <td>['"obj_firingTypes":"oil"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"1"']</td>
      <td>['"obj_baseRent":"740"']</td>
      <td>['"obj_livingSpace":"67.37"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>145</td>
      <td>745  (zzgl. Heizkosten)</td>
      <td>nicht in Nebenkosten enthalten</td>
      <td>['lat: 53.493636048600344,']</td>
      <td>['lng: 10.204297951920761']</td>
      <td>Brüdtweg 15</td>
      <td>NaN</td>
      <td>21033 Hamburg / Lohbrügge Hamburg</td>
      <td>...</td>
      <td>['"obj_firingTypes":"no_information"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"4"']</td>
      <td>['"obj_baseRent":"600"']</td>
      <td>['"obj_livingSpace":"77"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>250</td>
      <td>936</td>
      <td>inkl. 150 €</td>
      <td>['lat: 53.56978432240341,']</td>
      <td>['lng: 9.973693895665868']</td>
      <td>Bundesstraße 64</td>
      <td>NaN</td>
      <td>20144 Hamburg Eimsbüttel</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"y"']</td>
      <td>['"obj_yearConstructedRange":"1"']</td>
      <td>['"obj_baseRent":"686"']</td>
      <td>['"obj_livingSpace":"58"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"normal"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>100</td>
      <td>1.250</td>
      <td>100 €</td>
      <td>['lat: 53.57611822321049,']</td>
      <td>['lng: 9.952844267614122']</td>
      <td>Osterstraße 102</td>
      <td>NaN</td>
      <td>20259 Hamburg Eimsbüttel</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"1"']</td>
      <td>['"obj_baseRent":"1050"']</td>
      <td>['"obj_livingSpace":"80.57"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"normal"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
  </tbody>
</table>

<p>9 rows × 47 columns</p>

</div>



`df.tail()`

**Description -** The command `df.tail()` is the counterpart to `df.head()`, it returns the last 5 rows of the DataFrame by default, if no parameters are specified by the user. Using the parameter *n*
, one can specify the number of rows, that get returned. Needless to say, rows returned will always end with the row at the last index value and include the preceding *n-1* rows.

**Example -** First the maximum of the index of `df` is checked, to show that the last printed row is indeed the last value in the index of the DataFrame, other than that the examples mirror the two
from the `df.head()` command, to display their similarities.

```python
print('The maximum value of the range index of df is %s' % df.index.max())
df.tail()
```

    The maximum value of the range index of df is 12494

<div style="width:656px;overflow-x:scroll;">

<table>
  <thead>
    <tr>
      <th></th>
      <th>einbau_kue</th>
      <th>lift</th>
      <th>nebenkosten</th>
      <th>gesamt_miete</th>
      <th>heiz_kosten</th>
      <th>lat</th>
      <th>lng</th>
      <th>str</th>
      <th>nutzf</th>
      <th>regio</th>
      <th>...</th>
      <th>json_firingTypes</th>
      <th>json_hasKitchen</th>
      <th>json_cellar</th>
      <th>json_yearConstructedRange</th>
      <th>json_baseRent</th>
      <th>json_livingSpace</th>
      <th>json_condition</th>
      <th>json_interiorQual</th>
      <th>json_petsAllowed</th>
      <th>json_lift</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12490</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>80</td>
      <td>1.058</td>
      <td>47 €</td>
      <td>['lat: 53.586938610218276,']</td>
      <td>['lng: 10.016258235901141']</td>
      <td>Goldbekufer 29</td>
      <td>8 m²</td>
      <td>22303 Hamburg Winterhude</td>
      <td>...</td>
      <td>['"obj_firingTypes":"oil"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"y"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"931"']</td>
      <td>['"obj_livingSpace":"66.5"']</td>
      <td>['"obj_condition":"mint_condition"']</td>
      <td>['"obj_interiorQual":"sophisticated"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>12491</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>61</td>
      <td>674</td>
      <td>26 €</td>
      <td>['lat: 53.55758333359278,']</td>
      <td>['lng: 10.03986901076397']</td>
      <td>Burgstraße 34</td>
      <td>NaN</td>
      <td>20535 Hamburg Hamm-Nord</td>
      <td>...</td>
      <td>['"obj_firingTypes":"oil"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"y"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"587"']</td>
      <td>['"obj_livingSpace":"51"']</td>
      <td>['"obj_condition":"refurbished"']</td>
      <td>['"obj_interiorQual":"sophisticated"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>12492</th>
      <td>Einbauküche</td>
      <td>NaN</td>
      <td>76</td>
      <td>752</td>
      <td>70 €</td>
      <td>['lat: 53.6486450531966,']</td>
      <td>['lng: 10.039966464612842']</td>
      <td>Bei der Ziegelei 4</td>
      <td>8 m²</td>
      <td>22339 Hamburg Hummelsbüttel</td>
      <td>...</td>
      <td>['"obj_firingTypes":"oil"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"y"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"606"']</td>
      <td>['"obj_livingSpace":"63.69"']</td>
      <td>['"obj_condition":"refurbished"']</td>
      <td>['"obj_interiorQual":"sophisticated"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
    <tr>
      <th>12493</th>
      <td>Einbauküche</td>
      <td>Personenaufzug</td>
      <td>59,93</td>
      <td>382,73</td>
      <td>21,62 €</td>
      <td>['lat: 53.54886472789119,']</td>
      <td>['lng: 10.079737639604678']</td>
      <td>Culinstraße 58</td>
      <td>NaN</td>
      <td>22111 Hamburg Horn</td>
      <td>...</td>
      <td>['"obj_firingTypes":"district_heating"']</td>
      <td>['"obj_hasKitchen":"y"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"301.18"']</td>
      <td>['"obj_livingSpace":"30.89"']</td>
      <td>['"obj_condition":"no_information"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"y"']</td>
    </tr>
    <tr>
      <th>12494</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>101</td>
      <td>499,91</td>
      <td>in Nebenkosten enthalten</td>
      <td>['lat: 53.46145736469006,']</td>
      <td>['lng: 9.966232033537533']</td>
      <td>Denickestraße 42 b</td>
      <td>NaN</td>
      <td>21075 Hamburg Harburg</td>
      <td>...</td>
      <td>[]</td>
      <td>['"obj_hasKitchen":"n"']</td>
      <td>['"obj_cellar":"n"']</td>
      <td>['"obj_yearConstructedRange":"2"']</td>
      <td>['"obj_baseRent":"398.91"']</td>
      <td>['"obj_livingSpace":"46.93"']</td>
      <td>['"obj_condition":"well_kept"']</td>
      <td>['"obj_interiorQual":"no_information"']</td>
      <td>['"obj_petsAllowed":"no_information"']</td>
      <td>['"obj_lift":"n"']</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 47 columns</p>

</div>



`df.columns`

**Description -** The command `df.columns` does one thing and one thing well, one might say. It returns a list of strings, the list of the columns of the DataFrame. It's output can be iterated
through, in order to select subsets of all columns. An iteration can be done in the form of a list comprehension, that makes use of conditional clauses for example. It also helps one find problematic
column names, that need to be changed in order to qualify as tidy. The output of it also helps one get an overview of all the columns names and therefore is a starting point for dropping certain
columns and renaming the columns, so they follow an easy to remember and precise naming pattern.

**Example -** Below, the set of columns of the DataFrame are printed. One can see, that there are two types of patterns found in the names of the columns.

1. The first set of columns originates from values found in listings, that are visible to the visitor. These ones have no prefix attached to them and they all have German names.
2. Columns in the second set have the prefix 'json_' added to them. This comes from the fact, that they were sourced from a *script tag* found in the raw *HTML* code of each listing. The inner *HTML*
   of these *script tags* consisted of key-value pairs using a *json* like formatting. It was not machine readable though. The names of these columns were in English already and only the 'json_'
   prefix was added afterwards.

There are several other differences between the sets, as we will see later.

```python
df.columns
```

    Index(['einbau_kue', 'lift', 'nebenkosten', 'gesamt_miete', 'heiz_kosten',
           'lat', 'lng', 'str', 'nutzf', 'regio', 'parking', 'online_since',
           'baujahr', 'objekt_zustand', 'heizungsart', 'wesent_energietr',
           'endenergiebedarf', 'kaltmiete', 'quadratmeter', 'anzahl_zimmer',
           'balkon/terasse', 'keller', 'typ', 'etage', 'anz_schlafzimmer',
           'anz_badezimmer', 'haustiere', 'nicht_mehr_verfg_seit',
           'json_heatingType', 'json_balcony', 'json_electricityBasePrice',
           'json_picturecount', 'json_telekomDownloadSpeed',
           'json_telekomUploadSpeed', 'json_totalRent', 'json_yearConstructed',
           'json_electricityKwhPrice', 'json_firingTypes', 'json_hasKitchen',
           'json_cellar', 'json_yearConstructedRange', 'json_baseRent',
           'json_livingSpace', 'json_condition', 'json_interiorQual',
           'json_petsAllowed', 'json_lift'],
          dtype='object')

`df.`

**Description -** The command `df.` returns

**Example -** `df.`

```python
df.index
```

    Int64Index([    0,     1,     2,     3,     4,     5,     6,     7,     8,
                    9,
                ...
                12485, 12486, 12487, 12488, 12489, 12490, 12491, 12492, 12493,
                12494],
               dtype='int64', length=12325)

```python
df.dtypes
```

```markdown
einbau_kue                    object
lift                          object
nebenkosten                   object
gesamt_miete                  object
heiz_kosten                   object
lat                           object
lng                           object
str                           object
nutzf                         object
regio                         object
parking                       object
online_since                  object
baujahr                       object
objekt_zustand                object
heizungsart                   object
wesent_energietr              object
endenergiebedarf              object
kaltmiete                     object
quadratmeter                  object
anzahl_zimmer                 object
balkon/terasse                object
keller                        object
typ                           object
etage                         object
anz_schlafzimmer             float64
anz_badezimmer               float64
haustiere                     object
nicht_mehr_verfg_seit         object
json_heatingType              object
json_balcony                  object
json_electricityBasePrice     object
json_picturecount             object
json_telekomDownloadSpeed     object
json_telekomUploadSpeed       object
json_totalRent                object
json_yearConstructed          object
json_electricityKwhPrice      object
json_firingTypes              object
json_hasKitchen               object
json_cellar                   object
json_yearConstructedRange     object
json_baseRent                 object
json_livingSpace              object
json_condition                object
json_interiorQual             object
json_petsAllowed              object
json_lift                     object
dtype: object
```

```python
df.shape
```

    (12325, 47)

```python
df.count()
```

```markdown
einbau_kue 8024 lift 2975 nebenkosten 12324 gesamt_miete 12324 heiz_kosten 12324 lat 12324 lng 12324 str 9482 nutzf 1185 regio 12324 parking 3187 online_since 12324 baujahr 11342 objekt_zustand 7810
heizungsart 9526 wesent_energietr 9930 endenergiebedarf 3771 kaltmiete 12324 quadratmeter 12324 anzahl_zimmer 12324 balkon/terasse 8526 keller 6337 typ 9703 etage 9737 anz_schlafzimmer 6469
anz_badezimmer 7317 haustiere 3914 nicht_mehr_verfg_seit 11629 json_heatingType 12324 json_balcony 12324 json_electricityBasePrice 12324 json_picturecount 12324 json_telekomDownloadSpeed 12324
json_telekomUploadSpeed 12324 json_totalRent 12324 json_yearConstructed 12324 json_electricityKwhPrice 12324 json_firingTypes 12324 json_hasKitchen 12324 json_cellar 12324 json_yearConstructedRange
12324 json_baseRent 12324 json_livingSpace 12324 json_condition 12324 json_interiorQual 12324 json_petsAllowed 12324 json_lift 12324 dtype: int64
```

```python
df.describe().to_markdown()
```

To get a first look at the DataFrame, that holds all records, there are multiple tools in the pandas library one can use. It is assumed, that the Dataframe is named `df` in the following.

1. A popular choice is `df.head()`
2. Its counterpart is `df.tail()`
3. Another one is `df.describe()`
4.
