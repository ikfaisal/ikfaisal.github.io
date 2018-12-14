---
title:  "Exploratory Data Analysis (EDA)"
categories: generalassembly python dataviz
---
_Jonathan | Jon | Ibrahim_
---
In our second week we were asked to give a presentation about EDA. My group partners were Jonathan & Jonathan. Here I am posting what we have prepared to present.

### Objectives

- Data Collection
- Data Cleaning
- Data Visualisation


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_style('whitegrid')

%matplotlib inline
```

### Data Collection

Data collection is the process of gathering information in an established systematic way that enables one to test hypothesis and evaluate outcomes easily.


```python
fifa = pd.read_csv('./DataSets/FIFA18.csv', low_memory=False)
```


```python
fifa.head()
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
      <th>Name</th>
      <th>Age</th>
      <th>Photo</th>
      <th>Nationality</th>
      <th>Flag</th>
      <th>Overall</th>
      <th>Potential</th>
      <th>Club</th>
      <th>Club Logo</th>
      <th>...</th>
      <th>RB</th>
      <th>RCB</th>
      <th>RCM</th>
      <th>RDM</th>
      <th>RF</th>
      <th>RM</th>
      <th>RS</th>
      <th>RW</th>
      <th>RWB</th>
      <th>ST</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Cristiano Ronaldo</td>
      <td>32</td>
      <td>https://cdn.sofifa.org/48/18/players/20801.png</td>
      <td>Portugal</td>
      <td>https://cdn.sofifa.org/flags/38.png</td>
      <td>94</td>
      <td>94</td>
      <td>Real Madrid CF</td>
      <td>https://cdn.sofifa.org/24/18/teams/243.png</td>
      <td>...</td>
      <td>61.0</td>
      <td>53.0</td>
      <td>82.0</td>
      <td>62.0</td>
      <td>91.0</td>
      <td>89.0</td>
      <td>92.0</td>
      <td>91.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>L. Messi</td>
      <td>30</td>
      <td>https://cdn.sofifa.org/48/18/players/158023.png</td>
      <td>Argentina</td>
      <td>https://cdn.sofifa.org/flags/52.png</td>
      <td>93</td>
      <td>93</td>
      <td>FC Barcelona</td>
      <td>https://cdn.sofifa.org/24/18/teams/241.png</td>
      <td>...</td>
      <td>57.0</td>
      <td>45.0</td>
      <td>84.0</td>
      <td>59.0</td>
      <td>92.0</td>
      <td>90.0</td>
      <td>88.0</td>
      <td>91.0</td>
      <td>62.0</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Neymar</td>
      <td>25</td>
      <td>https://cdn.sofifa.org/48/18/players/190871.png</td>
      <td>Brazil</td>
      <td>https://cdn.sofifa.org/flags/54.png</td>
      <td>92</td>
      <td>94</td>
      <td>Paris Saint-Germain</td>
      <td>https://cdn.sofifa.org/24/18/teams/73.png</td>
      <td>...</td>
      <td>59.0</td>
      <td>46.0</td>
      <td>79.0</td>
      <td>59.0</td>
      <td>88.0</td>
      <td>87.0</td>
      <td>84.0</td>
      <td>89.0</td>
      <td>64.0</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>L. Suárez</td>
      <td>30</td>
      <td>https://cdn.sofifa.org/48/18/players/176580.png</td>
      <td>Uruguay</td>
      <td>https://cdn.sofifa.org/flags/60.png</td>
      <td>92</td>
      <td>92</td>
      <td>FC Barcelona</td>
      <td>https://cdn.sofifa.org/24/18/teams/241.png</td>
      <td>...</td>
      <td>64.0</td>
      <td>58.0</td>
      <td>80.0</td>
      <td>65.0</td>
      <td>88.0</td>
      <td>85.0</td>
      <td>88.0</td>
      <td>87.0</td>
      <td>68.0</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>M. Neuer</td>
      <td>31</td>
      <td>https://cdn.sofifa.org/48/18/players/167495.png</td>
      <td>Germany</td>
      <td>https://cdn.sofifa.org/flags/21.png</td>
      <td>92</td>
      <td>92</td>
      <td>FC Bayern Munich</td>
      <td>https://cdn.sofifa.org/24/18/teams/21.png</td>
      <td>...</td>
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
<p>5 rows × 75 columns</p>
</div>



After getting data we need to check the data-type of features.

There are following types of features :

- numeric
- categorical
- ordinal
- datetime
- coordinates

In order to know the data types/features of data, we need to run:


```python
fifa.dtypes
```




    Unnamed: 0               int64
    Name                    object
    Age                      int64
    Photo                   object
    Nationality             object
    Flag                    object
    Overall                  int64
    Potential                int64
    Club                    object
    Club Logo               object
    Value                   object
    Wage                    object
    Special                  int64
    Acceleration            object
    Aggression              object
    Agility                 object
    Balance                 object
    Ball control            object
    Composure               object
    Crossing                object
    Curve                   object
    Dribbling               object
    Finishing               object
    Free kick accuracy      object
    GK diving               object
    GK handling             object
    GK kicking              object
    GK positioning          object
    GK reflexes             object
    Heading accuracy        object
                            ...   
    Vision                  object
    Volleys                 object
    CAM                    float64
    CB                     float64
    CDM                    float64
    CF                     float64
    CM                     float64
    ID                       int64
    LAM                    float64
    LB                     float64
    LCB                    float64
    LCM                    float64
    LDM                    float64
    LF                     float64
    LM                     float64
    LS                     float64
    LW                     float64
    LWB                    float64
    Preferred Positions     object
    RAM                    float64
    RB                     float64
    RCB                    float64
    RCM                    float64
    RDM                    float64
    RF                     float64
    RM                     float64
    RS                     float64
    RW                     float64
    RWB                    float64
    ST                     float64
    Length: 75, dtype: object




```python
fifa.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 17981 entries, 0 to 17980
    Data columns (total 75 columns):
    Unnamed: 0             17981 non-null int64
    Name                   17981 non-null object
    Age                    17981 non-null int64
    Photo                  17981 non-null object
    Nationality            17981 non-null object
    Flag                   17981 non-null object
    Overall                17981 non-null int64
    Potential              17981 non-null int64
    Club                   17733 non-null object
    Club Logo              17981 non-null object
    Value                  17981 non-null object
    Wage                   17981 non-null object
    Special                17981 non-null int64
    Acceleration           17981 non-null object
    Aggression             17981 non-null object
    Agility                17981 non-null object
    Balance                17981 non-null object
    Ball control           17981 non-null object
    Composure              17981 non-null object
    Crossing               17981 non-null object
    Curve                  17981 non-null object
    Dribbling              17981 non-null object
    Finishing              17981 non-null object
    Free kick accuracy     17981 non-null object
    GK diving              17981 non-null object
    GK handling            17981 non-null object
    GK kicking             17981 non-null object
    GK positioning         17981 non-null object
    GK reflexes            17981 non-null object
    Heading accuracy       17981 non-null object
    Interceptions          17981 non-null object
    Jumping                17981 non-null object
    Long passing           17981 non-null object
    Long shots             17981 non-null object
    Marking                17981 non-null object
    Penalties              17981 non-null object
    Positioning            17981 non-null object
    Reactions              17981 non-null object
    Short passing          17981 non-null object
    Shot power             17981 non-null object
    Sliding tackle         17981 non-null object
    Sprint speed           17981 non-null object
    Stamina                17981 non-null object
    Standing tackle        17981 non-null object
    Strength               17981 non-null object
    Vision                 17981 non-null object
    Volleys                17981 non-null object
    CAM                    15952 non-null float64
    CB                     15952 non-null float64
    CDM                    15952 non-null float64
    CF                     15952 non-null float64
    CM                     15952 non-null float64
    ID                     17981 non-null int64
    LAM                    15952 non-null float64
    LB                     15952 non-null float64
    LCB                    15952 non-null float64
    LCM                    15952 non-null float64
    LDM                    15952 non-null float64
    LF                     15952 non-null float64
    LM                     15952 non-null float64
    LS                     15952 non-null float64
    LW                     15952 non-null float64
    LWB                    15952 non-null float64
    Preferred Positions    17981 non-null object
    RAM                    15952 non-null float64
    RB                     15952 non-null float64
    RCB                    15952 non-null float64
    RCM                    15952 non-null float64
    RDM                    15952 non-null float64
    RF                     15952 non-null float64
    RM                     15952 non-null float64
    RS                     15952 non-null float64
    RW                     15952 non-null float64
    RWB                    15952 non-null float64
    ST                     15952 non-null float64
    dtypes: float64(26), int64(6), object(43)
    memory usage: 10.3+ MB


### Data Cleaning

High-level, data types are a way of storing data that can be utilized for different purposes. For our arithmetic and visualization purposes, we want to change the datatypes to floats or integers that will allow subsequent mathematical processes to be run on them.


```python
'''
From our initial dataset read through, we can determine that wage is returned as an object data type, but
it should be a float or integer, so it warrants further inspection.
'''

fifa.Wage.head()
```




    0    €565K
    1    €565K
    2    €280K
    3    €510K
    4    €230K
    Name: Wage, dtype: object




```python
def remove_currency(data_column):
    '''
    We can see from the above that we need to from replace €, K from data column and convert to int.

    We can do so using this function.
    '''
    data_column = data_column.str.replace('€', '')
    data_column = data_column.str.replace('K', '')
    data_column = pd.to_numeric(data_column)
    return data_column
```


```python
'''
Here we call the above function on this Wage column.
'''

fifa["Wage"] = remove_currency(fifa["Wage"])
```


```python
'''
Here we check that the symbols have been removed.
'''

fifa.Wage.head()
```




    0    565
    1    565
    2    280
    3    510
    4    230
    Name: Wage, dtype: int64




```python
fifa.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 17981 entries, 0 to 17980
    Data columns (total 75 columns):
    Unnamed: 0             17981 non-null int64
    Name                   17981 non-null object
    Age                    17981 non-null int64
    Photo                  17981 non-null object
    Nationality            17981 non-null object
    Flag                   17981 non-null object
    Overall                17981 non-null int64
    Potential              17981 non-null int64
    Club                   17733 non-null object
    Club Logo              17981 non-null object
    Value                  17981 non-null object
    Wage                   17981 non-null int64
    Special                17981 non-null int64
    Acceleration           17981 non-null object
    Aggression             17981 non-null object
    Agility                17981 non-null object
    Balance                17981 non-null object
    Ball control           17981 non-null object
    Composure              17981 non-null object
    Crossing               17981 non-null object
    Curve                  17981 non-null object
    Dribbling              17981 non-null object
    Finishing              17981 non-null object
    Free kick accuracy     17981 non-null object
    GK diving              17981 non-null object
    GK handling            17981 non-null object
    GK kicking             17981 non-null object
    GK positioning         17981 non-null object
    GK reflexes            17981 non-null object
    Heading accuracy       17981 non-null object
    Interceptions          17981 non-null object
    Jumping                17981 non-null object
    Long passing           17981 non-null object
    Long shots             17981 non-null object
    Marking                17981 non-null object
    Penalties              17981 non-null object
    Positioning            17981 non-null object
    Reactions              17981 non-null object
    Short passing          17981 non-null object
    Shot power             17981 non-null object
    Sliding tackle         17981 non-null object
    Sprint speed           17981 non-null object
    Stamina                17981 non-null object
    Standing tackle        17981 non-null object
    Strength               17981 non-null object
    Vision                 17981 non-null object
    Volleys                17981 non-null object
    CAM                    15952 non-null float64
    CB                     15952 non-null float64
    CDM                    15952 non-null float64
    CF                     15952 non-null float64
    CM                     15952 non-null float64
    ID                     17981 non-null int64
    LAM                    15952 non-null float64
    LB                     15952 non-null float64
    LCB                    15952 non-null float64
    LCM                    15952 non-null float64
    LDM                    15952 non-null float64
    LF                     15952 non-null float64
    LM                     15952 non-null float64
    LS                     15952 non-null float64
    LW                     15952 non-null float64
    LWB                    15952 non-null float64
    Preferred Positions    17981 non-null object
    RAM                    15952 non-null float64
    RB                     15952 non-null float64
    RCB                    15952 non-null float64
    RCM                    15952 non-null float64
    RDM                    15952 non-null float64
    RF                     15952 non-null float64
    RM                     15952 non-null float64
    RS                     15952 non-null float64
    RW                     15952 non-null float64
    RWB                    15952 non-null float64
    ST                     15952 non-null float64
    dtypes: float64(26), int64(7), object(42)
    memory usage: 10.3+ MB



```python
'''
We can now observe that value needs the same treatment
'''

fifa.Value.head()
```




    0    €95.5M
    1     €105M
    2     €123M
    3      €97M
    4      €61M
    Name: Value, dtype: object




```python
def remove_currency_mill(data_column):
    data_column = data_column.str.replace('€', '')
    data_column = data_column.str.replace('M', '')
    data_column = data_column.str.replace('K', '')
    data_column = pd.to_numeric(data_column)
    return data_column
```


```python
fifa["Value"] = remove_currency_mill(fifa["Value"])
```


```python
fifa.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 17981 entries, 0 to 17980
    Data columns (total 75 columns):
    Unnamed: 0             17981 non-null int64
    Name                   17981 non-null object
    Age                    17981 non-null int64
    Photo                  17981 non-null object
    Nationality            17981 non-null object
    Flag                   17981 non-null object
    Overall                17981 non-null int64
    Potential              17981 non-null int64
    Club                   17733 non-null object
    Club Logo              17981 non-null object
    Value                  17981 non-null float64
    Wage                   17981 non-null int64
    Special                17981 non-null int64
    Acceleration           17981 non-null object
    Aggression             17981 non-null object
    Agility                17981 non-null object
    Balance                17981 non-null object
    Ball control           17981 non-null object
    Composure              17981 non-null object
    Crossing               17981 non-null object
    Curve                  17981 non-null object
    Dribbling              17981 non-null object
    Finishing              17981 non-null object
    Free kick accuracy     17981 non-null object
    GK diving              17981 non-null object
    GK handling            17981 non-null object
    GK kicking             17981 non-null object
    GK positioning         17981 non-null object
    GK reflexes            17981 non-null object
    Heading accuracy       17981 non-null object
    Interceptions          17981 non-null object
    Jumping                17981 non-null object
    Long passing           17981 non-null object
    Long shots             17981 non-null object
    Marking                17981 non-null object
    Penalties              17981 non-null object
    Positioning            17981 non-null object
    Reactions              17981 non-null object
    Short passing          17981 non-null object
    Shot power             17981 non-null object
    Sliding tackle         17981 non-null object
    Sprint speed           17981 non-null object
    Stamina                17981 non-null object
    Standing tackle        17981 non-null object
    Strength               17981 non-null object
    Vision                 17981 non-null object
    Volleys                17981 non-null object
    CAM                    15952 non-null float64
    CB                     15952 non-null float64
    CDM                    15952 non-null float64
    CF                     15952 non-null float64
    CM                     15952 non-null float64
    ID                     17981 non-null int64
    LAM                    15952 non-null float64
    LB                     15952 non-null float64
    LCB                    15952 non-null float64
    LCM                    15952 non-null float64
    LDM                    15952 non-null float64
    LF                     15952 non-null float64
    LM                     15952 non-null float64
    LS                     15952 non-null float64
    LW                     15952 non-null float64
    LWB                    15952 non-null float64
    Preferred Positions    17981 non-null object
    RAM                    15952 non-null float64
    RB                     15952 non-null float64
    RCB                    15952 non-null float64
    RCM                    15952 non-null float64
    RDM                    15952 non-null float64
    RF                     15952 non-null float64
    RM                     15952 non-null float64
    RS                     15952 non-null float64
    RW                     15952 non-null float64
    RWB                    15952 non-null float64
    ST                     15952 non-null float64
    dtypes: float64(27), int64(7), object(41)
    memory usage: 10.3+ MB


We can use the describe function to provide more information on the data.

- describe() function shows the statistics of the data.

- If you try running this with columns that do not have all integers or floats, then the column data will not be displayed.

- It can be very useful to look at these statistics early on to get high level idea about the data.


```python
fifa.describe().T
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
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Unnamed: 0</th>
      <td>17981.0</td>
      <td>8990.000000</td>
      <td>5190.811931</td>
      <td>0.0</td>
      <td>4495.0</td>
      <td>8990.0</td>
      <td>13485.0</td>
      <td>17980.0</td>
    </tr>
    <tr>
      <th>Age</th>
      <td>17981.0</td>
      <td>25.144541</td>
      <td>4.614272</td>
      <td>16.0</td>
      <td>21.0</td>
      <td>25.0</td>
      <td>28.0</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>Overall</th>
      <td>17981.0</td>
      <td>66.247984</td>
      <td>6.987965</td>
      <td>46.0</td>
      <td>62.0</td>
      <td>66.0</td>
      <td>71.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>Potential</th>
      <td>17981.0</td>
      <td>71.190813</td>
      <td>6.102199</td>
      <td>46.0</td>
      <td>67.0</td>
      <td>71.0</td>
      <td>75.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>Value</th>
      <td>17981.0</td>
      <td>260.810316</td>
      <td>288.430164</td>
      <td>0.0</td>
      <td>4.3</td>
      <td>150.0</td>
      <td>475.0</td>
      <td>975.0</td>
    </tr>
    <tr>
      <th>Wage</th>
      <td>17981.0</td>
      <td>11.546966</td>
      <td>23.080000</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>12.0</td>
      <td>565.0</td>
    </tr>
    <tr>
      <th>Special</th>
      <td>17981.0</td>
      <td>1594.095100</td>
      <td>272.151435</td>
      <td>728.0</td>
      <td>1449.0</td>
      <td>1633.0</td>
      <td>1786.0</td>
      <td>2291.0</td>
    </tr>
    <tr>
      <th>CAM</th>
      <td>15952.0</td>
      <td>59.251755</td>
      <td>9.880164</td>
      <td>27.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>CB</th>
      <td>15952.0</td>
      <td>55.550464</td>
      <td>12.192579</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>57.0</td>
      <td>65.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>CDM</th>
      <td>15952.0</td>
      <td>56.865283</td>
      <td>10.310178</td>
      <td>26.0</td>
      <td>49.0</td>
      <td>58.0</td>
      <td>65.0</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>CF</th>
      <td>15952.0</td>
      <td>59.030028</td>
      <td>9.926988</td>
      <td>27.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>CM</th>
      <td>15952.0</td>
      <td>58.506833</td>
      <td>8.888040</td>
      <td>30.0</td>
      <td>53.0</td>
      <td>59.0</td>
      <td>65.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>ID</th>
      <td>17981.0</td>
      <td>207658.710138</td>
      <td>32291.667313</td>
      <td>16.0</td>
      <td>192622.0</td>
      <td>214057.0</td>
      <td>231448.0</td>
      <td>241219.0</td>
    </tr>
    <tr>
      <th>LAM</th>
      <td>15952.0</td>
      <td>59.251755</td>
      <td>9.880164</td>
      <td>27.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>LB</th>
      <td>15952.0</td>
      <td>56.979689</td>
      <td>9.791627</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>58.0</td>
      <td>64.0</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>LCB</th>
      <td>15952.0</td>
      <td>55.550464</td>
      <td>12.192579</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>57.0</td>
      <td>65.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>LCM</th>
      <td>15952.0</td>
      <td>58.506833</td>
      <td>8.888040</td>
      <td>30.0</td>
      <td>53.0</td>
      <td>59.0</td>
      <td>65.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>LDM</th>
      <td>15952.0</td>
      <td>56.865283</td>
      <td>10.310178</td>
      <td>26.0</td>
      <td>49.0</td>
      <td>58.0</td>
      <td>65.0</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>LF</th>
      <td>15952.0</td>
      <td>59.030028</td>
      <td>9.926988</td>
      <td>27.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>LM</th>
      <td>15952.0</td>
      <td>60.057736</td>
      <td>9.349180</td>
      <td>28.0</td>
      <td>54.0</td>
      <td>61.0</td>
      <td>67.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>LS</th>
      <td>15952.0</td>
      <td>58.204050</td>
      <td>9.181392</td>
      <td>31.0</td>
      <td>52.0</td>
      <td>59.0</td>
      <td>65.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>LW</th>
      <td>15952.0</td>
      <td>59.359265</td>
      <td>9.978084</td>
      <td>26.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>LWB</th>
      <td>15952.0</td>
      <td>57.698721</td>
      <td>9.142825</td>
      <td>31.0</td>
      <td>51.0</td>
      <td>58.0</td>
      <td>64.0</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>RAM</th>
      <td>15952.0</td>
      <td>59.251755</td>
      <td>9.880164</td>
      <td>27.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>RB</th>
      <td>15952.0</td>
      <td>56.979689</td>
      <td>9.791627</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>58.0</td>
      <td>64.0</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>RCB</th>
      <td>15952.0</td>
      <td>55.550464</td>
      <td>12.192579</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>57.0</td>
      <td>65.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>RCM</th>
      <td>15952.0</td>
      <td>58.506833</td>
      <td>8.888040</td>
      <td>30.0</td>
      <td>53.0</td>
      <td>59.0</td>
      <td>65.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>RDM</th>
      <td>15952.0</td>
      <td>56.865283</td>
      <td>10.310178</td>
      <td>26.0</td>
      <td>49.0</td>
      <td>58.0</td>
      <td>65.0</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>RF</th>
      <td>15952.0</td>
      <td>59.030028</td>
      <td>9.926988</td>
      <td>27.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>RM</th>
      <td>15952.0</td>
      <td>60.057736</td>
      <td>9.349180</td>
      <td>28.0</td>
      <td>54.0</td>
      <td>61.0</td>
      <td>67.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>RS</th>
      <td>15952.0</td>
      <td>58.204050</td>
      <td>9.181392</td>
      <td>31.0</td>
      <td>52.0</td>
      <td>59.0</td>
      <td>65.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>RW</th>
      <td>15952.0</td>
      <td>59.359265</td>
      <td>9.978084</td>
      <td>26.0</td>
      <td>53.0</td>
      <td>60.0</td>
      <td>66.0</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>RWB</th>
      <td>15952.0</td>
      <td>57.698721</td>
      <td>9.142825</td>
      <td>31.0</td>
      <td>51.0</td>
      <td>58.0</td>
      <td>64.0</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>ST</th>
      <td>15952.0</td>
      <td>58.204050</td>
      <td>9.181392</td>
      <td>31.0</td>
      <td>52.0</td>
      <td>59.0</td>
      <td>65.0</td>
      <td>92.0</td>
    </tr>
  </tbody>
</table>
</div>



from the above we can observe a couple of columns that could use more cleaning/investigation.

1. the unnamed: 0 column appears to be another index row, which is not required as the data frame has applied an automatic index.

2. row ID has a minimum alot lower than the IQR.


```python
fifa.columns
```




    Index(['Unnamed: 0', 'Name', 'Age', 'Photo', 'Nationality', 'Flag', 'Overall',
           'Potential', 'Club', 'Club Logo', 'Value', 'Wage', 'Special',
           'Acceleration', 'Aggression', 'Agility', 'Balance', 'Ball control',
           'Composure', 'Crossing', 'Curve', 'Dribbling', 'Finishing',
           'Free kick accuracy', 'GK diving', 'GK handling', 'GK kicking',
           'GK positioning', 'GK reflexes', 'Heading accuracy', 'Interceptions',
           'Jumping', 'Long passing', 'Long shots', 'Marking', 'Penalties',
           'Positioning', 'Reactions', 'Short passing', 'Shot power',
           'Sliding tackle', 'Sprint speed', 'Stamina', 'Standing tackle',
           'Strength', 'Vision', 'Volleys', 'CAM', 'CB', 'CDM', 'CF', 'CM', 'ID',
           'LAM', 'LB', 'LCB', 'LCM', 'LDM', 'LF', 'LM', 'LS', 'LW', 'LWB',
           'Preferred Positions', 'RAM', 'RB', 'RCB', 'RCM', 'RDM', 'RF', 'RM',
           'RS', 'RW', 'RWB', 'ST'],
          dtype='object')




```python
fifa.drop('Unnamed: 0', axis = 1, inplace=True)
```


```python
fifa.ID.plot.hist()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2120d389fd0>




![png](/img/output_81_1.png)



```python
fifa.ID.plot.box(vert = False)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2120cff3a90>




![png](/img/output_26_1.png)


We need to decide whether we want to remove the outliers from this dataset prior to visualisation, or whether we come back to it after we have had an opportunity to look for any potential relationships between data points.

### Data Visualizations

- Charts or graphs that visualize large amounts of complex data are easier to understand than spreadsheets or reports.

- Data visualization is a quick, easy way to convey concepts in a universal manner


```python
fifa.corr()
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
      <th>Age</th>
      <th>Overall</th>
      <th>Potential</th>
      <th>Value</th>
      <th>Wage</th>
      <th>Special</th>
      <th>CAM</th>
      <th>CB</th>
      <th>CDM</th>
      <th>CF</th>
      <th>...</th>
      <th>RB</th>
      <th>RCB</th>
      <th>RCM</th>
      <th>RDM</th>
      <th>RF</th>
      <th>RM</th>
      <th>RS</th>
      <th>RW</th>
      <th>RWB</th>
      <th>ST</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Age</th>
      <td>1.000000</td>
      <td>0.459765</td>
      <td>-0.218264</td>
      <td>-0.067069</td>
      <td>0.150006</td>
      <td>0.238667</td>
      <td>0.245855</td>
      <td>0.337481</td>
      <td>0.383450</td>
      <td>0.235596</td>
      <td>...</td>
      <td>0.321227</td>
      <td>0.337481</td>
      <td>0.365783</td>
      <td>0.383450</td>
      <td>0.235596</td>
      <td>0.232945</td>
      <td>0.287541</td>
      <td>0.206051</td>
      <td>0.337143</td>
      <td>0.287541</td>
    </tr>
    <tr>
      <th>Overall</th>
      <td>0.459765</td>
      <td>1.000000</td>
      <td>0.683474</td>
      <td>-0.233466</td>
      <td>0.593789</td>
      <td>0.604092</td>
      <td>0.650313</td>
      <td>0.448856</td>
      <td>0.607727</td>
      <td>0.636278</td>
      <td>...</td>
      <td>0.561887</td>
      <td>0.448856</td>
      <td>0.764609</td>
      <td>0.607727</td>
      <td>0.636278</td>
      <td>0.656745</td>
      <td>0.664822</td>
      <td>0.610198</td>
      <td>0.629401</td>
      <td>0.664822</td>
    </tr>
    <tr>
      <th>Potential</th>
      <td>-0.218264</td>
      <td>0.683474</td>
      <td>1.000000</td>
      <td>-0.217572</td>
      <td>0.519062</td>
      <td>0.399511</td>
      <td>0.470421</td>
      <td>0.219380</td>
      <td>0.345344</td>
      <td>0.458830</td>
      <td>...</td>
      <td>0.330672</td>
      <td>0.219380</td>
      <td>0.508133</td>
      <td>0.345344</td>
      <td>0.458830</td>
      <td>0.474998</td>
      <td>0.447747</td>
      <td>0.448580</td>
      <td>0.383213</td>
      <td>0.447747</td>
    </tr>
    <tr>
      <th>Value</th>
      <td>-0.067069</td>
      <td>-0.233466</td>
      <td>-0.217572</td>
      <td>1.000000</td>
      <td>-0.261942</td>
      <td>-0.109017</td>
      <td>-0.181998</td>
      <td>-0.093359</td>
      <td>-0.139879</td>
      <td>-0.180572</td>
      <td>...</td>
      <td>-0.125827</td>
      <td>-0.093359</td>
      <td>-0.203486</td>
      <td>-0.139879</td>
      <td>-0.180572</td>
      <td>-0.177024</td>
      <td>-0.184606</td>
      <td>-0.169072</td>
      <td>-0.144693</td>
      <td>-0.184606</td>
    </tr>
    <tr>
      <th>Wage</th>
      <td>0.150006</td>
      <td>0.593789</td>
      <td>0.519062</td>
      <td>-0.261942</td>
      <td>1.000000</td>
      <td>0.367419</td>
      <td>0.412427</td>
      <td>0.220554</td>
      <td>0.321822</td>
      <td>0.408102</td>
      <td>...</td>
      <td>0.299300</td>
      <td>0.220554</td>
      <td>0.457183</td>
      <td>0.321822</td>
      <td>0.408102</td>
      <td>0.412422</td>
      <td>0.421092</td>
      <td>0.390940</td>
      <td>0.343395</td>
      <td>0.421092</td>
    </tr>
    <tr>
      <th>Special</th>
      <td>0.238667</td>
      <td>0.604092</td>
      <td>0.399511</td>
      <td>-0.109017</td>
      <td>0.367419</td>
      <td>1.000000</td>
      <td>0.854197</td>
      <td>0.401629</td>
      <td>0.650723</td>
      <td>0.822487</td>
      <td>...</td>
      <td>0.623048</td>
      <td>0.401629</td>
      <td>0.943764</td>
      <td>0.650723</td>
      <td>0.822487</td>
      <td>0.872130</td>
      <td>0.793552</td>
      <td>0.825615</td>
      <td>0.735167</td>
      <td>0.793552</td>
    </tr>
    <tr>
      <th>CAM</th>
      <td>0.245855</td>
      <td>0.650313</td>
      <td>0.470421</td>
      <td>-0.181998</td>
      <td>0.412427</td>
      <td>0.854197</td>
      <td>1.000000</td>
      <td>-0.070694</td>
      <td>0.257182</td>
      <td>0.986346</td>
      <td>...</td>
      <td>0.204500</td>
      <td>-0.070694</td>
      <td>0.903315</td>
      <td>0.257182</td>
      <td>0.986346</td>
      <td>0.983408</td>
      <td>0.927452</td>
      <td>0.983941</td>
      <td>0.368896</td>
      <td>0.927452</td>
    </tr>
    <tr>
      <th>CB</th>
      <td>0.337481</td>
      <td>0.448856</td>
      <td>0.219380</td>
      <td>-0.093359</td>
      <td>0.220554</td>
      <td>0.401629</td>
      <td>-0.070694</td>
      <td>1.000000</td>
      <td>0.929486</td>
      <td>-0.141250</td>
      <td>...</td>
      <td>0.926170</td>
      <td>1.000000</td>
      <td>0.328064</td>
      <td>0.929486</td>
      <td>-0.141250</td>
      <td>-0.029624</td>
      <td>-0.129200</td>
      <td>-0.139745</td>
      <td>0.849959</td>
      <td>-0.129200</td>
    </tr>
    <tr>
      <th>CDM</th>
      <td>0.383450</td>
      <td>0.607727</td>
      <td>0.345344</td>
      <td>-0.139879</td>
      <td>0.321822</td>
      <td>0.650723</td>
      <td>0.257182</td>
      <td>0.929486</td>
      <td>1.000000</td>
      <td>0.165728</td>
      <td>...</td>
      <td>0.968022</td>
      <td>0.929486</td>
      <td>0.631197</td>
      <td>1.000000</td>
      <td>0.165728</td>
      <td>0.292332</td>
      <td>0.129067</td>
      <td>0.175801</td>
      <td>0.955188</td>
      <td>0.129067</td>
    </tr>
    <tr>
      <th>CF</th>
      <td>0.235596</td>
      <td>0.636278</td>
      <td>0.458830</td>
      <td>-0.180572</td>
      <td>0.408102</td>
      <td>0.822487</td>
      <td>0.986346</td>
      <td>-0.141250</td>
      <td>0.165728</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.123218</td>
      <td>-0.141250</td>
      <td>0.846493</td>
      <td>0.165728</td>
      <td>1.000000</td>
      <td>0.970136</td>
      <td>0.967872</td>
      <td>0.986833</td>
      <td>0.286582</td>
      <td>0.967872</td>
    </tr>
    <tr>
      <th>CM</th>
      <td>0.365783</td>
      <td>0.764609</td>
      <td>0.508133</td>
      <td>-0.203486</td>
      <td>0.457183</td>
      <td>0.943764</td>
      <td>0.903315</td>
      <td>0.328064</td>
      <td>0.631197</td>
      <td>0.846493</td>
      <td>...</td>
      <td>0.558706</td>
      <td>0.328064</td>
      <td>1.000000</td>
      <td>0.631197</td>
      <td>0.846493</td>
      <td>0.898170</td>
      <td>0.779877</td>
      <td>0.844640</td>
      <td>0.685704</td>
      <td>0.779877</td>
    </tr>
    <tr>
      <th>ID</th>
      <td>-0.719316</td>
      <td>-0.425881</td>
      <td>0.001998</td>
      <td>0.088663</td>
      <td>-0.213480</td>
      <td>-0.232074</td>
      <td>-0.268760</td>
      <td>-0.285998</td>
      <td>-0.345803</td>
      <td>-0.254976</td>
      <td>...</td>
      <td>-0.282252</td>
      <td>-0.285998</td>
      <td>-0.367868</td>
      <td>-0.345803</td>
      <td>-0.254976</td>
      <td>-0.250306</td>
      <td>-0.291824</td>
      <td>-0.229243</td>
      <td>-0.304484</td>
      <td>-0.291824</td>
    </tr>
    <tr>
      <th>LAM</th>
      <td>0.245855</td>
      <td>0.650313</td>
      <td>0.470421</td>
      <td>-0.181998</td>
      <td>0.412427</td>
      <td>0.854197</td>
      <td>1.000000</td>
      <td>-0.070694</td>
      <td>0.257182</td>
      <td>0.986346</td>
      <td>...</td>
      <td>0.204500</td>
      <td>-0.070694</td>
      <td>0.903315</td>
      <td>0.257182</td>
      <td>0.986346</td>
      <td>0.983408</td>
      <td>0.927452</td>
      <td>0.983941</td>
      <td>0.368896</td>
      <td>0.927452</td>
    </tr>
    <tr>
      <th>LB</th>
      <td>0.321227</td>
      <td>0.561887</td>
      <td>0.330672</td>
      <td>-0.125827</td>
      <td>0.299300</td>
      <td>0.623048</td>
      <td>0.204500</td>
      <td>0.926170</td>
      <td>0.968022</td>
      <td>0.123218</td>
      <td>...</td>
      <td>1.000000</td>
      <td>0.926170</td>
      <td>0.558706</td>
      <td>0.968022</td>
      <td>0.123218</td>
      <td>0.273691</td>
      <td>0.077723</td>
      <td>0.158306</td>
      <td>0.981366</td>
      <td>0.077723</td>
    </tr>
    <tr>
      <th>LCB</th>
      <td>0.337481</td>
      <td>0.448856</td>
      <td>0.219380</td>
      <td>-0.093359</td>
      <td>0.220554</td>
      <td>0.401629</td>
      <td>-0.070694</td>
      <td>1.000000</td>
      <td>0.929486</td>
      <td>-0.141250</td>
      <td>...</td>
      <td>0.926170</td>
      <td>1.000000</td>
      <td>0.328064</td>
      <td>0.929486</td>
      <td>-0.141250</td>
      <td>-0.029624</td>
      <td>-0.129200</td>
      <td>-0.139745</td>
      <td>0.849959</td>
      <td>-0.129200</td>
    </tr>
    <tr>
      <th>LCM</th>
      <td>0.365783</td>
      <td>0.764609</td>
      <td>0.508133</td>
      <td>-0.203486</td>
      <td>0.457183</td>
      <td>0.943764</td>
      <td>0.903315</td>
      <td>0.328064</td>
      <td>0.631197</td>
      <td>0.846493</td>
      <td>...</td>
      <td>0.558706</td>
      <td>0.328064</td>
      <td>1.000000</td>
      <td>0.631197</td>
      <td>0.846493</td>
      <td>0.898170</td>
      <td>0.779877</td>
      <td>0.844640</td>
      <td>0.685704</td>
      <td>0.779877</td>
    </tr>
    <tr>
      <th>LDM</th>
      <td>0.383450</td>
      <td>0.607727</td>
      <td>0.345344</td>
      <td>-0.139879</td>
      <td>0.321822</td>
      <td>0.650723</td>
      <td>0.257182</td>
      <td>0.929486</td>
      <td>1.000000</td>
      <td>0.165728</td>
      <td>...</td>
      <td>0.968022</td>
      <td>0.929486</td>
      <td>0.631197</td>
      <td>1.000000</td>
      <td>0.165728</td>
      <td>0.292332</td>
      <td>0.129067</td>
      <td>0.175801</td>
      <td>0.955188</td>
      <td>0.129067</td>
    </tr>
    <tr>
      <th>LF</th>
      <td>0.235596</td>
      <td>0.636278</td>
      <td>0.458830</td>
      <td>-0.180572</td>
      <td>0.408102</td>
      <td>0.822487</td>
      <td>0.986346</td>
      <td>-0.141250</td>
      <td>0.165728</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.123218</td>
      <td>-0.141250</td>
      <td>0.846493</td>
      <td>0.165728</td>
      <td>1.000000</td>
      <td>0.970136</td>
      <td>0.967872</td>
      <td>0.986833</td>
      <td>0.286582</td>
      <td>0.967872</td>
    </tr>
    <tr>
      <th>LM</th>
      <td>0.232945</td>
      <td>0.656745</td>
      <td>0.474998</td>
      <td>-0.177024</td>
      <td>0.412422</td>
      <td>0.872130</td>
      <td>0.983408</td>
      <td>-0.029624</td>
      <td>0.292332</td>
      <td>0.970136</td>
      <td>...</td>
      <td>0.273691</td>
      <td>-0.029624</td>
      <td>0.898170</td>
      <td>0.292332</td>
      <td>0.970136</td>
      <td>1.000000</td>
      <td>0.900747</td>
      <td>0.988587</td>
      <td>0.439558</td>
      <td>0.900747</td>
    </tr>
    <tr>
      <th>LS</th>
      <td>0.287541</td>
      <td>0.664822</td>
      <td>0.447747</td>
      <td>-0.184606</td>
      <td>0.421092</td>
      <td>0.793552</td>
      <td>0.927452</td>
      <td>-0.129200</td>
      <td>0.129067</td>
      <td>0.967872</td>
      <td>...</td>
      <td>0.077723</td>
      <td>-0.129200</td>
      <td>0.779877</td>
      <td>0.129067</td>
      <td>0.967872</td>
      <td>0.900747</td>
      <td>1.000000</td>
      <td>0.929186</td>
      <td>0.222406</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>LW</th>
      <td>0.206051</td>
      <td>0.610198</td>
      <td>0.448580</td>
      <td>-0.169072</td>
      <td>0.390940</td>
      <td>0.825615</td>
      <td>0.983941</td>
      <td>-0.139745</td>
      <td>0.175801</td>
      <td>0.986833</td>
      <td>...</td>
      <td>0.158306</td>
      <td>-0.139745</td>
      <td>0.844640</td>
      <td>0.175801</td>
      <td>0.986833</td>
      <td>0.988587</td>
      <td>0.929186</td>
      <td>1.000000</td>
      <td>0.327975</td>
      <td>0.929186</td>
    </tr>
    <tr>
      <th>LWB</th>
      <td>0.337143</td>
      <td>0.629401</td>
      <td>0.383213</td>
      <td>-0.144693</td>
      <td>0.343395</td>
      <td>0.735167</td>
      <td>0.368896</td>
      <td>0.849959</td>
      <td>0.955188</td>
      <td>0.286582</td>
      <td>...</td>
      <td>0.981366</td>
      <td>0.849959</td>
      <td>0.685704</td>
      <td>0.955188</td>
      <td>0.286582</td>
      <td>0.439558</td>
      <td>0.222406</td>
      <td>0.327975</td>
      <td>1.000000</td>
      <td>0.222406</td>
    </tr>
    <tr>
      <th>RAM</th>
      <td>0.245855</td>
      <td>0.650313</td>
      <td>0.470421</td>
      <td>-0.181998</td>
      <td>0.412427</td>
      <td>0.854197</td>
      <td>1.000000</td>
      <td>-0.070694</td>
      <td>0.257182</td>
      <td>0.986346</td>
      <td>...</td>
      <td>0.204500</td>
      <td>-0.070694</td>
      <td>0.903315</td>
      <td>0.257182</td>
      <td>0.986346</td>
      <td>0.983408</td>
      <td>0.927452</td>
      <td>0.983941</td>
      <td>0.368896</td>
      <td>0.927452</td>
    </tr>
    <tr>
      <th>RB</th>
      <td>0.321227</td>
      <td>0.561887</td>
      <td>0.330672</td>
      <td>-0.125827</td>
      <td>0.299300</td>
      <td>0.623048</td>
      <td>0.204500</td>
      <td>0.926170</td>
      <td>0.968022</td>
      <td>0.123218</td>
      <td>...</td>
      <td>1.000000</td>
      <td>0.926170</td>
      <td>0.558706</td>
      <td>0.968022</td>
      <td>0.123218</td>
      <td>0.273691</td>
      <td>0.077723</td>
      <td>0.158306</td>
      <td>0.981366</td>
      <td>0.077723</td>
    </tr>
    <tr>
      <th>RCB</th>
      <td>0.337481</td>
      <td>0.448856</td>
      <td>0.219380</td>
      <td>-0.093359</td>
      <td>0.220554</td>
      <td>0.401629</td>
      <td>-0.070694</td>
      <td>1.000000</td>
      <td>0.929486</td>
      <td>-0.141250</td>
      <td>...</td>
      <td>0.926170</td>
      <td>1.000000</td>
      <td>0.328064</td>
      <td>0.929486</td>
      <td>-0.141250</td>
      <td>-0.029624</td>
      <td>-0.129200</td>
      <td>-0.139745</td>
      <td>0.849959</td>
      <td>-0.129200</td>
    </tr>
    <tr>
      <th>RCM</th>
      <td>0.365783</td>
      <td>0.764609</td>
      <td>0.508133</td>
      <td>-0.203486</td>
      <td>0.457183</td>
      <td>0.943764</td>
      <td>0.903315</td>
      <td>0.328064</td>
      <td>0.631197</td>
      <td>0.846493</td>
      <td>...</td>
      <td>0.558706</td>
      <td>0.328064</td>
      <td>1.000000</td>
      <td>0.631197</td>
      <td>0.846493</td>
      <td>0.898170</td>
      <td>0.779877</td>
      <td>0.844640</td>
      <td>0.685704</td>
      <td>0.779877</td>
    </tr>
    <tr>
      <th>RDM</th>
      <td>0.383450</td>
      <td>0.607727</td>
      <td>0.345344</td>
      <td>-0.139879</td>
      <td>0.321822</td>
      <td>0.650723</td>
      <td>0.257182</td>
      <td>0.929486</td>
      <td>1.000000</td>
      <td>0.165728</td>
      <td>...</td>
      <td>0.968022</td>
      <td>0.929486</td>
      <td>0.631197</td>
      <td>1.000000</td>
      <td>0.165728</td>
      <td>0.292332</td>
      <td>0.129067</td>
      <td>0.175801</td>
      <td>0.955188</td>
      <td>0.129067</td>
    </tr>
    <tr>
      <th>RF</th>
      <td>0.235596</td>
      <td>0.636278</td>
      <td>0.458830</td>
      <td>-0.180572</td>
      <td>0.408102</td>
      <td>0.822487</td>
      <td>0.986346</td>
      <td>-0.141250</td>
      <td>0.165728</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.123218</td>
      <td>-0.141250</td>
      <td>0.846493</td>
      <td>0.165728</td>
      <td>1.000000</td>
      <td>0.970136</td>
      <td>0.967872</td>
      <td>0.986833</td>
      <td>0.286582</td>
      <td>0.967872</td>
    </tr>
    <tr>
      <th>RM</th>
      <td>0.232945</td>
      <td>0.656745</td>
      <td>0.474998</td>
      <td>-0.177024</td>
      <td>0.412422</td>
      <td>0.872130</td>
      <td>0.983408</td>
      <td>-0.029624</td>
      <td>0.292332</td>
      <td>0.970136</td>
      <td>...</td>
      <td>0.273691</td>
      <td>-0.029624</td>
      <td>0.898170</td>
      <td>0.292332</td>
      <td>0.970136</td>
      <td>1.000000</td>
      <td>0.900747</td>
      <td>0.988587</td>
      <td>0.439558</td>
      <td>0.900747</td>
    </tr>
    <tr>
      <th>RS</th>
      <td>0.287541</td>
      <td>0.664822</td>
      <td>0.447747</td>
      <td>-0.184606</td>
      <td>0.421092</td>
      <td>0.793552</td>
      <td>0.927452</td>
      <td>-0.129200</td>
      <td>0.129067</td>
      <td>0.967872</td>
      <td>...</td>
      <td>0.077723</td>
      <td>-0.129200</td>
      <td>0.779877</td>
      <td>0.129067</td>
      <td>0.967872</td>
      <td>0.900747</td>
      <td>1.000000</td>
      <td>0.929186</td>
      <td>0.222406</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>RW</th>
      <td>0.206051</td>
      <td>0.610198</td>
      <td>0.448580</td>
      <td>-0.169072</td>
      <td>0.390940</td>
      <td>0.825615</td>
      <td>0.983941</td>
      <td>-0.139745</td>
      <td>0.175801</td>
      <td>0.986833</td>
      <td>...</td>
      <td>0.158306</td>
      <td>-0.139745</td>
      <td>0.844640</td>
      <td>0.175801</td>
      <td>0.986833</td>
      <td>0.988587</td>
      <td>0.929186</td>
      <td>1.000000</td>
      <td>0.327975</td>
      <td>0.929186</td>
    </tr>
    <tr>
      <th>RWB</th>
      <td>0.337143</td>
      <td>0.629401</td>
      <td>0.383213</td>
      <td>-0.144693</td>
      <td>0.343395</td>
      <td>0.735167</td>
      <td>0.368896</td>
      <td>0.849959</td>
      <td>0.955188</td>
      <td>0.286582</td>
      <td>...</td>
      <td>0.981366</td>
      <td>0.849959</td>
      <td>0.685704</td>
      <td>0.955188</td>
      <td>0.286582</td>
      <td>0.439558</td>
      <td>0.222406</td>
      <td>0.327975</td>
      <td>1.000000</td>
      <td>0.222406</td>
    </tr>
    <tr>
      <th>ST</th>
      <td>0.287541</td>
      <td>0.664822</td>
      <td>0.447747</td>
      <td>-0.184606</td>
      <td>0.421092</td>
      <td>0.793552</td>
      <td>0.927452</td>
      <td>-0.129200</td>
      <td>0.129067</td>
      <td>0.967872</td>
      <td>...</td>
      <td>0.077723</td>
      <td>-0.129200</td>
      <td>0.779877</td>
      <td>0.129067</td>
      <td>0.967872</td>
      <td>0.900747</td>
      <td>1.000000</td>
      <td>0.929186</td>
      <td>0.222406</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 33 columns</p>
</div>




```python
ax = fifa.plot.scatter('Age', 'Wage', figsize=(16,4))
ax.set_title("Age/Wage")
```




    Text(0.5,1,'Age/Wage')




![png](/img/output_30_1.png)


- Data visualization is a quick, easy way to convey concepts in a universal manner

# Types of Plot

- Univariate
- Bivariate
- Multivariate

### Univariate

- 'line' : line plot (default)
- 'bar' : vertical bar plot
- 'pie' : pie plot
- 'barh' : horizontal bar plot
- 'hist' : histogram
- 'area' : area plot

# Line, Area

- Good for ordinal categorical and interval data.

- Line graphs are used to track changes over short and long periods of time.

- Line graphs can also be used to compare changes over the same period of time for more than one group.


```python
# 'line' : line plot (default)

fifa.groupby(by='Age').mean()[['Wage']].plot.line(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x212262e5b70>




![png](/img/output_82_1.png)



```python
# 'line' : line plot (default)

fifa.groupby(by='Age').mean()[['Wage', 'Overall']].plot.line(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x21226445d30>




![png](/img/output_36_1.png)



```python
# 'area' : area plot

fifa.groupby(by='Age').mean()[['Overall', 'Wage']].plot.area(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x212266a80f0>




![png](/img/output_37_1.png)



```python
# 'kde' : Kernel Density Estimation plot

fifa.loc[0:]['Overall'].plot(kind='kde', figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x21226a3d710>




![png](/img/output_38_1.png)



```python
# 'density' : same as 'kde'

fifa.loc[0:]['Potential'].plot(kind='density', figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x21226fb6470>




![png](/img/output_39_1.png)


# Bar, Barh, Pie

- Good for nominal and small ordinal categorical data.

- Bar graphs are used to compare things between different groups


```python
# 'bar' : vertical bar plot

fifa['Nationality'].value_counts().head(10).plot.bar(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2122638d400>




![png](/img/output_80_1.png)



```python
# 'barh' : horizontal bar plot

fifa['Nationality'].value_counts().head(10).plot.barh(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x21226371978>




![png](/img/output_42_1.png)



```python
# 'pie' : pie plot

fifa['Nationality'].value_counts().head(10).plot.pie(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x21225e21710>




![png](/img/output_83_1.png)


### Histogram

- Good for interval data.


```python
# 'hist' : histogram

fifa["Age"].plot.hist(bins=100, figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x212176e5320>




![png](/img/output_45_1.png)


### Boxplot

- To visualize the distribution of values within each column.




```python
# 'box' : boxplot

fifa['Age'].plot.box(figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x2122669ba90>




![png](/img/output_47_1.png)


### Bivariate

- 'scatter' : scatter plot
- 'hexbin' : hexbin plot

### Scatter

A simple scatter plot simply maps each variable of interest to a point in two-dimensional space.


```python
# 'scatter' : scatter plot

fifa.plot(kind='scatter', x='Overall', y='Wage', figsize=(10,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x212269c7c88>




![png](/img/output_50_1.png)


### Hexbin

- A hex plot aggregates points in space into hexagons, and then colors those hexagons based on the values within them


```python
# 'hexbin' : hexbin plot

fifa.plot(kind='hexbin', x='Overall', y='Age', figsize=(10,6), grid=15)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x212269b9ef0>




![png](/img/output_52_1.png)


### Multivariate

- Multivariate Scatter Plot
- Grouped Box Plot
- Heatmap


```python
# Heatmap

f = (
    fifa.loc[:, ['Acceleration', 'Aggression', 'Agility', 'Balance', 'Ball control']]
        .applymap(lambda v: int(v) if str.isdecimal(v) else np.nan)
        .dropna()
).corr()

sns.heatmap(f, annot=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x21226dde198>




![png](/img/output_54_1.png)


# Happy Exploring!

References:

[https://www.kaggle.com/residentmario/welcome-to-data-visualization](https://www.kaggle.com/residentmario/welcome-to-data-visualization)

[https://pandas.pydata.org/pandas-docs/stable/visualization.html](https://pandas.pydata.org/pandas-docs/stable/visualization.html)

[https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html](https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html)
