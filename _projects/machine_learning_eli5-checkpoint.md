---
title: Machine Learning Demo Post
date: 2019-07-27 00:00:00
description: This is a demo post that shows what you can do inside portfolio and blog posts. We’ve included everything you need to create engaging posts and case studies to show off your work in a beautiful way.
featured_image: /images/website_export_hamburg_alster20130608.jpg
# gallery_images: website_export_hamburg_alster20130608.jpg
---
Testing how I can post a project.

```python
from sklearn.linear_model import Lasso
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split
import eli5
from sklearn.impute import SimpleImputer
from eli5.sklearn import PermutationImportance, explain_linear_regressor_weights
from IPython.display import display, HTML
from bs4 import BeautifulSoup
import pandas as pd
import numpy as np
from sklearn.cluster import KMeans
from scipy.spatial.distance import cdist, pdist
import matplotlib.pyplot as plt
import mpl_toolkits
```


```python
from scipy.cluster.hierarchy import dendrogram, linkage, fcluster
from geopy.distance import vincenty
from sklearn.decomposition import PCA
from sklearn.cluster import DBSCAN
import matplotlib.cm as cm
from scipy.spatial.distance import cdist, pdist
from sklearn import metrics
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler
from datetime import datetime
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('ggplot')
#from mpl_toolkits.basemap import Basemap
import copy
import json
import math
from collections import OrderedDict
import warnings
warnings.filterwarnings('ignore')
%matplotlib inline

```


```python
import numpy
```


```python
import geopandas
```


```python
import sklearn
```


```python
sklearn
```




    <module 'sklearn' from '/Users/tobiasklein 1/PycharmsProjects/so_deep/env/lib/python3.7/site-packages/sklearn/__init__.py'>




```python
from sklearn import linear_model
```


```python
import os
import sys
sys.executable
```




    '/Users/tobiasklein 1/PycharmsProjects/so_deep/env/bin/python3'




```python
df = pd.read_csv("/Users/tobiasklein 1/PycharmsProjects/so_deep/bachelor_thesis/interim_data/machine_learning_output_jupyter_nb.csv")
```


```python
df.info()
# %%
df[['kaltmiete']].boxplot()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 12323 entries, 0 to 12322
    Data columns (total 57 columns):
    Unnamed: 0                   12323 non-null int64
    einbau_kue                   12323 non-null int64
    lift                         12323 non-null int64
    nebenkosten                  12120 non-null float64
    gesamt_miete                 12322 non-null object
    heiz_kosten                  12322 non-null object
    lat                          9480 non-null float64
    lng                          9480 non-null float64
    str                          9481 non-null object
    nutzf                        1184 non-null object
    regio                        12322 non-null object
    parking                      3186 non-null object
    online_since                 12323 non-null object
    baujahr                      11130 non-null float64
    objekt_zustand               7808 non-null object
    heizungsart                  9524 non-null object
    wesent_energietr             9928 non-null object
    endenergiebedarf             3771 non-null object
    kaltmiete                    12322 non-null float64
    quadratmeter                 12323 non-null float64
    anzahl_zimmer                12323 non-null float64
    balkon/terasse               12323 non-null int64
    keller                       12323 non-null float64
    typ                          9701 non-null object
    etage                        12323 non-null float64
    anz_schlafzimmer             6467 non-null float64
    anz_badezimmer               7315 non-null float64
    haustiere                    3914 non-null object
    nicht_mehr_verfg_seit        12323 non-null object
    json_heatingType             12322 non-null object
    json_balcony                 12322 non-null float64
    json_electricityBasePrice    12322 non-null object
    json_picturecount            12323 non-null float64
    json_telekomDownloadSpeed    11625 non-null float64
    json_telekomUploadSpeed      11568 non-null float64
    json_totalRent               12322 non-null object
    json_yearConstructed         12322 non-null object
    json_electricityKwhPrice     12322 non-null object
    json_firingTypes             12322 non-null object
    json_hasKitchen              12322 non-null object
    json_cellar                  12322 non-null object
    json_yearConstructedRange    12322 non-null object
    json_baseRent                12322 non-null object
    json_livingSpace             11750 non-null float64
    json_condition               12322 non-null object
    json_interiorQual            12322 non-null object
    json_petsAllowed             12322 non-null object
    json_lift                    12322 non-null object
    splitted_regio_str           12322 non-null object
    plz                          12322 non-null float64
    stadt_u_viertel              12322 non-null object
    gps                          12323 non-null object
    time_gap                     12323 non-null int64
    indexn                       12323 non-null int64
    str_plit                     9735 non-null object
    etagen_im_haus               4653 non-null float64
    kaltm_qdm                    12323 non-null float64
    dtypes: float64(19), int64(6), object(32)
    memory usage: 5.4+ MB





    <matplotlib.axes._subplots.AxesSubplot at 0x7fa6706ee9e8>




![png](/images/machine_learning_demo/output_9_2.png)



```python
df_learn = pd.get_dummies(df[["parking","baujahr","objekt_zustand","heizungsart","wesent_energietr"]])
```


```python
df_learn.info()
```

dfn = df[["nebenkosten", "kaltmiete", "json_picturecount", "plz", "etage", "balkon/terasse", "lift", "quadratmeter",
          "anzahl_zimmer", "json_telekomDownloadSpeed", "json_telekomUploadSpeed", "lng","lat","time_gap"]]
dfn = dfn.dropna()


```python
df_nn = pd.get_dummies(df)
df_nn = df_nn.dropna()
```


```python

# X = dfn[["nebenkosten", "json_picturecount", "plz", "etage", "balkon/terasse", "lift", "quadratmeter"]]
X = df_nn.loc[:,df_nn.columns != "kaltmiete"]
y = df_nn["kaltmiete"]
print(len(df_nn))
```

    2347



```python
# using y from above
feature_names = [i for i in df_nn.columns if df_nn[i].dtype in [np.int,np.float] and i != "kaltmiete"]
```


```python
X = df_nn[feature_names]
train_X, val_X, train_y, val_y = train_test_split(X,y, random_state = 42)
my_imputer = SimpleImputer()
imputed_X_train = my_imputer.fit_transform(train_X)
imputed_X_test = my_imputer.transform(val_X)

my_model = Lasso(random_state=42).fit(imputed_X_train,train_y)
```


```python
perm = PermutationImportance(my_model, random_state=42).fit(imputed_X_test,val_y)
eli5.show_weights(perm, feature_names = val_X.columns.tolist())
```





    <style>
    table.eli5-weights tr:hover {
        filter: brightness(85%);
    }
</style>



    

    

    

    

    

    


    

    

    

    

    

    


    

    

    

    

    
        <table class="eli5-weights eli5-feature-importances" style="border-collapse: collapse; border: none; margin-top: 0em; table-layout: auto;">
    <thead>
    <tr style="border: none;">
        <th style="padding: 0 1em 0 0.5em; text-align: right; border: none;">Weight</th>
        <th style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">Feature</th>
    </tr>
    </thead>
    <tbody>
    
        <tr style="background-color: hsl(120, 100.00%, 80.00%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                1.4088
                
                    &plusmn; 0.1074
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                quadratmeter
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 88.54%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.6361
                
                    &plusmn; 0.0568
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                kaltm_qdm
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.54%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0065
                
                    &plusmn; 0.0021
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                json_livingSpace
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.61%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0050
                
                    &plusmn; 0.0009
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                anz_schlafzimmer
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.69%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0037
                
                    &plusmn; 0.0012
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                anzahl_zimmer
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.69%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0036
                
                    &plusmn; 0.0018
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                baujahr
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.84%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0015
                
                    &plusmn; 0.0012
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                nebenkosten
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.88%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0009
                
                    &plusmn; 0.0003
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                etage
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.88%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0009
                
                    &plusmn; 0.0007
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                indexn
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.88%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0009
                
                    &plusmn; 0.0011
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                Unnamed: 0
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.89%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0008
                
                    &plusmn; 0.0006
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                json_telekomUploadSpeed
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.90%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0007
                
                    &plusmn; 0.0006
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                json_telekomDownloadSpeed
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.93%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0005
                
                    &plusmn; 0.0002
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                json_balcony
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.93%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0004
                
                    &plusmn; 0.0003
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                time_gap
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.93%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0004
                
                    &plusmn; 0.0003
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                balkon/terasse
            </td>
        </tr>
    
        <tr style="background-color: hsl(120, 100.00%, 99.95%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0.0002
                
                    &plusmn; 0.0004
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                json_picturecount
            </td>
        </tr>
    
        <tr style="background-color: hsl(0, 100.00%, 100.00%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0
                
                    &plusmn; 0.0000
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                lift
            </td>
        </tr>
    
        <tr style="background-color: hsl(0, 100.00%, 100.00%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0
                
                    &plusmn; 0.0000
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                etagen_im_haus
            </td>
        </tr>
    
        <tr style="background-color: hsl(0, 100.00%, 100.00%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0
                
                    &plusmn; 0.0000
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                lng
            </td>
        </tr>
    
        <tr style="background-color: hsl(0, 100.00%, 100.00%); border: none;">
            <td style="padding: 0 1em 0 0.5em; text-align: right; border: none;">
                0
                
                    &plusmn; 0.0000
                
            </td>
            <td style="padding: 0 0.5em 0 0.5em; text-align: left; border: none;">
                keller
            </td>
        </tr>
    
    
        
            <tr style="background-color: hsl(0, 100.00%, 100.00%); border: none;">
                <td colspan="2" style="padding: 0 0.5em 0 0.5em; text-align: center; border: none; white-space: nowrap;">
                    <i>&hellip; 4 more &hellip;</i>
                </td>
            </tr>
        
    
    </tbody>
</table>
    

    


    

    

    

    

    

    








```python
X_learn = df_learn
```


```python
df = df.dropna()
X = df[["lng","lat"]].values
Ks = range(1,10)
kmean = [KMeans(n_clusters=i).fit(X) for i in Ks]
```


```python
def plot_elbow(kmean, X):
    centroids = [k.cluster_centers_ for k in kmean]
    D_k = [cdist(X, center, 'euclidean') for center in centroids]
    dist = [np.min(D,axis=1) for D in D_k]

    # Total with-in sum of square
    wcss = [sum(d**2) for d in dist]
    tss = sum(pdist(X)**2)/X.shape[0]
    bss = tss-wcss

    plt.subplots(nrows=1, ncols=1, figsize=(8,8))
    ax = plt.subplot(1, 1, 1)
    ax.plot(Ks, bss/tss*100, 'b*-')
    plt.grid(True)
    plt.xlabel('Number of clusters')
    plt.ylabel('Percentage of variance explained (%)')
    plt.title('Elbow for KMeans clustering')
    plt.show()

plot_elbow(kmean, X)

```


![png](/images/machine_learning_demo/output_20_0.png)



```python
def plot_stations_map(ax, stns):
    # determine range to print based on min, max lat and lon of the data
    lat = list(df['lat'])
    lon = list(df['lng'])
    margin = 0.01 # buffer to add to the range
    lat_min = min(lat) - margin
    lat_max = max(lat) + margin
    lon_min = min(lon) - margin
    lon_max = max(lon) + margin

    # create map using BASEMAP
    m = Basemap(llcrnrlon=lon_min,
                llcrnrlat=lat_min,
                urcrnrlon=lon_max,
                urcrnrlat=lat_max,
                lat_0=(lat_max - lat_min)/2,
                lon_0=(lon_max - lon_min)/2,
                projection='lcc',
                resolution = 'f',)

    m.drawcoastlines()
    m.fillcontinents(lake_color='aqua')
    m.drawmapboundary(fill_color='aqua')
    m.drawrivers()    
    
    # plot points
    clist = list(df['cluster'].unique())
    if -1 in clist:
        clist.remove(-1)
    k = len(clist)
    colors = iter(cm.Set1(np.linspace(0, 1, max(10, k))))
    for i in range(k):
        color = next(colors)
        dfs = df.loc[df['cluster'] == clist[i]]        
        #print("Cluster {} has {} samples.".format(clist[i], df.shape[0]))
        
        # convert lat and lon to map projection coordinates
        lons, lats = m(list(dfs['lng']), list(dfs['lat']))        
        ax.scatter(lons, lats, marker = 'o', color=color, edgecolor='gray', zorder=5, alpha=1.0, s=15)

```


```python
k = [2, 3, 4]
n = len(k)
plt.subplots(nrows=1, ncols=3, figsize=(18,15))

for i in range(n):
    est = kmean[k[i]-1]
    df['cluster'] = est.predict(X).tolist()
    
    ax = plt.subplot(1, 3, i+1)
    ax.set_title("Spatial Clustering with KMeans (k={})".format(k[i]))

    plot_stations_map(ax, df)

```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-35-b4bf478f1608> in <module>
         10     ax.set_title("Spatial Clustering with KMeans (k={})".format(k[i]))
         11 
    ---> 12     plot_stations_map(ax, df)
    

    <ipython-input-34-e3e22946221d> in plot_stations_map(ax, stns)
         10 
         11     # create map using BASEMAP
    ---> 12     m = Basemap(llcrnrlon=lon_min,
         13                 llcrnrlat=lat_min,
         14                 urcrnrlon=lon_max,


    NameError: name 'Basemap' is not defined



![png](/images/machine_learning_demo/output_22_1.png)



```python

```
