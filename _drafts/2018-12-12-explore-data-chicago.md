---
title:  "Guided Practice: Explore Data of Chicago"
categories: generalassembly python dataviz
---

Very often we may need to do some data transformations to do some merging. For example, if we want to provide some information on events in a given area, we might have a dataset that looks like the following:

| Block | Event   |
|------|------|
|   1  | Block Party|
|   2  | Block Party|
|   1  | House Party|
|   1  | Open Bar|

In this example, we have multiple rows for Block (3 rows for Block 1 and 1 row for Block 2). If we wanted to join these to another table on the block keys, we'd be doing what's known as a 1 to many join. We will be revisiting that topic later.

Another option is to create some aggregate function (a count, a mean, a median, etc.) so that our data set has only one row per key. If we counted up the number of events in our toy dataset above, it might look like:

| Block | count(Event)   |
|------|------|
|   1  | 3|
|   2  | 1|

This sort of groupby aggregation allows us to join a larger dataset with a smaller, provided that we can summarize them using some sort of aggregate function.

# Your Mission, Should You Choose to Accept it

You will take the role of an enterprising researcher, making use of the numerous free datasets available at the [City of Chicago Data Portal](https://data.cityofchicago.org/). You have a hunch that different types of reporting to 311, the City's information line, might be correlated with demographic characteristics of the 77 [community areas of Chicago](https://en.wikipedia.org/wiki/Community_areas_in_Chicago). You have downloaded some of this data in the following forms:

- **2008-2012-chi-census.csv** - A few selected Census outcomes from 2008-2012, aggregated by the Community Area
- **chicago_311_abandoned_vehicles.csv** - Calls to 311 for abandoned vehicles in 2008-2012
- **chicago_311_graffiti.csv** - Calls to 311 for graffiti removal in 2008-2012
- **chicago_311_vacant_abandoned_building.csv** - Calls to 311 about vacant or abandoned buildings in 2008-2012

Firing up your trusty laptop with Python, Numpy, and Pandas, you get to work. One way to join two of the datasets together, you realize, is with the following code:

```Python
census_data = pd.read_csv('2008-2012-chi-census.csv')
abandoned_vehicles = pd.read_csv('chicago_311_abandoned_vehicles.csv')

census_data.merge(abandoned_vehicles.groupby('Community Area').count(),
        left_on='Community Area Number',
        right_index=True, how='inner')
```

**Note:** We're doing a couple of things here that we haven't done before!

1. If our keys are named differently in each dataset, we can identify them by using **left_on** and **right_on** to point to the keys in the left and right dataset respectively
2. We are counting all the rows per **'Community Area'** in **abandoned_vehicles**. For the rest of this exercise, feel free to use that construction but, if you're interested in learning more, [df.groupby](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.groupby.html) contains the documentation for the **groupby** method in Pandas
3. We can also merge on the index of a dataframe, using **left_index=True** (if we want to join on the left dataset's index) or **right_index=True** (if we want to join on the right dataset's index).


```python
import pandas as pd
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')
%matplotlib inline
```

### 1. Load each csv into Python and take a few minutes to explore each. What sort of data does it provide?


```python
census = pd.read_csv('2008-2012-chi-census.csv')
vehicles = pd.read_csv('chicago_311_abandoned_vehicles.csv')
graffiti = pd.read_csv('chicago_311_graffiti.csv')
buildings = pd.read_csv('chicago_311_vacant_abandoned_building.csv')
```


```python
census.head()
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
      <th>Community Area Number</th>
      <th>Community Area Name</th>
      <th>Percent Housing Crowded</th>
      <th>Percent Households Below Poverty</th>
      <th>Percent Aged 16+ Unemployed</th>
      <th>Percent Aged 25+ Without HS Diploma</th>
      <th>Percent Aged Under 18 or Over 64</th>
      <th>Per Capita Income</th>
      <th>Hardship Index</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>Rogers Park</td>
      <td>7.7</td>
      <td>23.6</td>
      <td>8.7</td>
      <td>18.2</td>
      <td>27.5</td>
      <td>23939</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>West Ridge</td>
      <td>7.8</td>
      <td>17.2</td>
      <td>8.8</td>
      <td>20.8</td>
      <td>38.5</td>
      <td>23040</td>
      <td>46.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>Uptown</td>
      <td>3.8</td>
      <td>24.0</td>
      <td>8.9</td>
      <td>11.8</td>
      <td>22.2</td>
      <td>35787</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>Lincoln Square</td>
      <td>3.4</td>
      <td>10.9</td>
      <td>8.2</td>
      <td>13.4</td>
      <td>25.5</td>
      <td>37524</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>North Center</td>
      <td>0.3</td>
      <td>7.5</td>
      <td>5.2</td>
      <td>4.5</td>
      <td>26.2</td>
      <td>57123</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
vehicles.head()
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
      <th>Creation Date</th>
      <th>Status</th>
      <th>Completion Date</th>
      <th>Service Request Number</th>
      <th>Type of Service Request</th>
      <th>License Plate</th>
      <th>Vehicle Make/Model</th>
      <th>Vehicle Color</th>
      <th>Current Activity</th>
      <th>Most Recent Action</th>
      <th>...</th>
      <th>ZIP Code</th>
      <th>X Coordinate</th>
      <th>Y Coordinate</th>
      <th>Ward</th>
      <th>Police District</th>
      <th>Community Area</th>
      <th>SSA</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11/06/2008</td>
      <td>Completed</td>
      <td>04/14/2011</td>
      <td>08-02247245</td>
      <td>Abandoned Vehicle Complaint</td>
      <td>ECV9366</td>
      <td>General Motors Corp.</td>
      <td>Maroon</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>60651.0</td>
      <td>1.146868e+06</td>
      <td>1.905922e+06</td>
      <td>37.0</td>
      <td>11.0</td>
      <td>23.0</td>
      <td>NaN</td>
      <td>41.897894</td>
      <td>-87.735872</td>
      <td>(41.89789380014405, -87.73587218370734)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>02/03/2009</td>
      <td>Completed - Dup</td>
      <td>06/20/2012</td>
      <td>09-00193526</td>
      <td>Abandoned Vehicle Complaint</td>
      <td>43930H</td>
      <td>Ford</td>
      <td>White</td>
      <td>FVI - Outcome</td>
      <td>Create Work Order</td>
      <td>...</td>
      <td>60639.0</td>
      <td>1.143057e+06</td>
      <td>1.913138e+06</td>
      <td>31.0</td>
      <td>25.0</td>
      <td>19.0</td>
      <td>NaN</td>
      <td>41.918219</td>
      <td>-87.749987</td>
      <td>(41.91821929083758, -87.74998656996482)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>03/19/2009</td>
      <td>Completed</td>
      <td>03/22/2011</td>
      <td>09-00478279</td>
      <td>Abandoned Vehicle Complaint</td>
      <td>X397109</td>
      <td>Ford</td>
      <td>White</td>
      <td>FVI - Outcome</td>
      <td>Vehicle was moved from original address requested</td>
      <td>...</td>
      <td>60628.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>50.0</td>
      <td>51.0</td>
      <td>41.721060</td>
      <td>-87.595821</td>
      <td>(41.72105953472156, -87.59582056221775)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>05/13/2009</td>
      <td>Completed</td>
      <td>01/26/2011</td>
      <td>09-00806953</td>
      <td>Abandoned Vehicle Complaint</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>60639.0</td>
      <td>1.138769e+06</td>
      <td>1.911409e+06</td>
      <td>29.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>NaN</td>
      <td>41.913093</td>
      <td>-87.765781</td>
      <td>(41.91309264271512, -87.76578124615286)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>05/13/2009</td>
      <td>Completed</td>
      <td>01/26/2011</td>
      <td>09-00806954</td>
      <td>Abandoned Vehicle Complaint</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>60623.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>24.0</td>
      <td>10.0</td>
      <td>29.0</td>
      <td>NaN</td>
      <td>41.861539</td>
      <td>-87.715425</td>
      <td>(41.861538991418534, -87.71542483156753)</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
graffiti.head()
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
      <th>Creation Date</th>
      <th>Status</th>
      <th>Completion Date</th>
      <th>Service Request Number</th>
      <th>Type of Service Request</th>
      <th>What Type of Surface is the Graffiti on?</th>
      <th>Where is the Graffiti located?</th>
      <th>Street Address</th>
      <th>ZIP Code</th>
      <th>X Coordinate</th>
      <th>Y Coordinate</th>
      <th>Ward</th>
      <th>Police District</th>
      <th>Community Area</th>
      <th>SSA</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04/08/2008</td>
      <td>Completed</td>
      <td>05/25/2014</td>
      <td>08-00601980</td>
      <td>Graffiti Removal</td>
      <td>Wood - Painted</td>
      <td>Front</td>
      <td>249 W CERMAK RD</td>
      <td>60616.0</td>
      <td>1.174940e+06</td>
      <td>1.889749e+06</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>34.0</td>
      <td>NaN</td>
      <td>41.852717</td>
      <td>-87.633935</td>
      <td>(41.85271673337672, -87.6339345627447)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>04/08/2008</td>
      <td>Completed - Dup</td>
      <td>10/22/2014</td>
      <td>08-00601980</td>
      <td>Graffiti Removal</td>
      <td>Wood - Painted</td>
      <td>Front</td>
      <td>249 W CERMAK RD</td>
      <td>60616.0</td>
      <td>1.174940e+06</td>
      <td>1.889749e+06</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>34.0</td>
      <td>NaN</td>
      <td>41.852717</td>
      <td>-87.633935</td>
      <td>(41.85271673337672, -87.6339345627447)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>04/17/2009</td>
      <td>Completed</td>
      <td>09/18/2015</td>
      <td>09-00652518</td>
      <td>Graffiti Removal</td>
      <td>Metal</td>
      <td>Pole</td>
      <td>50 W WACKER DR</td>
      <td>60601.0</td>
      <td>1.175891e+06</td>
      <td>1.902174e+06</td>
      <td>42.0</td>
      <td>1.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>41.887042</td>
      <td>-87.629870</td>
      <td>(41.887041950950504, -87.62987031372374)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>04/17/2009</td>
      <td>Completed</td>
      <td>09/21/2015</td>
      <td>09-00652518</td>
      <td>Graffiti Removal</td>
      <td>Metal - Painted</td>
      <td>Pole</td>
      <td>50 W WACKER DR</td>
      <td>60601.0</td>
      <td>1.175891e+06</td>
      <td>1.902174e+06</td>
      <td>42.0</td>
      <td>1.0</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>41.887042</td>
      <td>-87.629870</td>
      <td>(41.887041950950504, -87.62987031372374)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>06/16/2009</td>
      <td>Completed</td>
      <td>05/18/2016</td>
      <td>09-01018187</td>
      <td>Graffiti Removal</td>
      <td>Brick - Unpainted</td>
      <td>Rear</td>
      <td>1803 W MONTROSE AVE</td>
      <td>60613.0</td>
      <td>1.163432e+06</td>
      <td>1.929256e+06</td>
      <td>47.0</td>
      <td>19.0</td>
      <td>5.0</td>
      <td>31.0</td>
      <td>41.961407</td>
      <td>-87.674628</td>
      <td>(41.96140670845814, -87.67462801002456)</td>
    </tr>
  </tbody>
</table>
</div>




```python
buildings.head()
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
      <th>SERVICE REQUEST TYPE</th>
      <th>SERVICE REQUEST NUMBER</th>
      <th>DATE SERVICE REQUEST WAS RECEIVED</th>
      <th>LOCATION OF BUILDING ON THE LOT (IF GARAGE, CHANGE TYPE CODE TO BGD).</th>
      <th>IS THE BUILDING DANGEROUS OR HAZARDOUS?</th>
      <th>IS BUILDING OPEN OR BOARDED?</th>
      <th>IF THE BUILDING IS OPEN, WHERE IS THE ENTRY POINT?</th>
      <th>IS THE BUILDING CURRENTLY VACANT OR OCCUPIED?</th>
      <th>IS THE BUILDING VACANT DUE TO FIRE?</th>
      <th>ANY PEOPLE USING PROPERTY? (HOMELESS, CHILDEN, GANGS)</th>
      <th>...</th>
      <th>ADDRESS STREET SUFFIX</th>
      <th>ZIP CODE</th>
      <th>X COORDINATE</th>
      <th>Y COORDINATE</th>
      <th>Ward</th>
      <th>Police District</th>
      <th>Community Area</th>
      <th>LATITUDE</th>
      <th>LONGITUDE</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Vacant/Abandoned Building</td>
      <td>08-00109075</td>
      <td>01/18/2008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>ST</td>
      <td>60613.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Vacant/Abandoned Building</td>
      <td>08-00577896</td>
      <td>04/03/2008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Building is Open / Unsecure</td>
      <td>NaN</td>
      <td>Vacant</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>ST</td>
      <td>60621.0</td>
      <td>1.170179e+06</td>
      <td>1.858859e+06</td>
      <td>17.0</td>
      <td>7.0</td>
      <td>68.0</td>
      <td>41.768198</td>
      <td>-87.651771</td>
      <td>(41.76819814695611, -87.65177097869127)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Vacant/Abandoned Building</td>
      <td>08-00588295</td>
      <td>04/05/2008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Building is Open / Unsecure</td>
      <td>GARAGE, VAGRANTS BROKE INTO GARAGE AND USE IT ...</td>
      <td>Vacant</td>
      <td>NaN</td>
      <td>True</td>
      <td>...</td>
      <td>AVE</td>
      <td>60619.0</td>
      <td>1.182657e+06</td>
      <td>1.850683e+06</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>44.0</td>
      <td>41.745482</td>
      <td>-87.606287</td>
      <td>(41.745482414802325, -87.60628681474407)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Vacant/Abandoned Building</td>
      <td>08-01476976</td>
      <td>07/30/2008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Building is Open / Unsecure</td>
      <td>REAR</td>
      <td>Vacant</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>AVE</td>
      <td>60621.0</td>
      <td>1.174523e+06</td>
      <td>1.857609e+06</td>
      <td>6.0</td>
      <td>7.0</td>
      <td>68.0</td>
      <td>41.764674</td>
      <td>-87.635884</td>
      <td>(41.764673747551555, -87.63588403606937)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Vacant/Abandoned Building</td>
      <td>08-01559367</td>
      <td>08/07/2008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Building is Open / Unsecure</td>
      <td>FRONT AND REAR</td>
      <td>Vacant</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>ST</td>
      <td>60636.0</td>
      <td>1.169023e+06</td>
      <td>1.855703e+06</td>
      <td>17.0</td>
      <td>7.0</td>
      <td>67.0</td>
      <td>41.759564</td>
      <td>-87.656096</td>
      <td>(41.75956423181548, -87.65609637199394)</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 23 columns</p>
</div>



### 2. Join each of the 311 calls datasets (modifying the code above) to get a count of each type of call per Community Area


```python
census.columns
```




    Index(['Community Area Number', 'Community Area Name',
           'Percent Housing Crowded', 'Percent Households Below Poverty',
           'Percent Aged 16+ Unemployed', 'Percent Aged 25+ Without HS Diploma',
           'Percent Aged Under 18 or Over 64', 'Per Capita Income',
           'Hardship Index'],
          dtype='object')




```python
vehicles.columns
```




    Index(['Creation Date', 'Status', 'Completion Date', 'Service Request Number',
           'Type of Service Request', 'License Plate', 'Vehicle Make/Model',
           'Vehicle Color', 'Current Activity', 'Most Recent Action',
           'How Many Days Has the Vehicle Been Reported as Parked?',
           'Street Address', 'ZIP Code', 'X Coordinate', 'Y Coordinate', 'Ward',
           'Police District', 'Community Area', 'SSA', 'Latitude', 'Longitude',
           'Location'],
          dtype='object')




```python
graffiti.columns
```




    Index(['Creation Date', 'Status', 'Completion Date', 'Service Request Number',
           'Type of Service Request', 'What Type of Surface is the Graffiti on?',
           'Where is the Graffiti located?', 'Street Address', 'ZIP Code',
           'X Coordinate', 'Y Coordinate', 'Ward', 'Police District',
           'Community Area', 'SSA', 'Latitude', 'Longitude', 'Location'],
          dtype='object')




```python
buildings.columns
```




    Index(['SERVICE REQUEST TYPE', 'SERVICE REQUEST NUMBER',
           'DATE SERVICE REQUEST WAS RECEIVED',
           'LOCATION OF BUILDING ON THE LOT (IF GARAGE, CHANGE TYPE CODE TO BGD).',
           'IS THE BUILDING DANGEROUS OR HAZARDOUS?',
           'IS BUILDING OPEN OR BOARDED?',
           'IF THE BUILDING IS OPEN, WHERE IS THE ENTRY POINT?',
           'IS THE BUILDING CURRENTLY VACANT OR OCCUPIED?',
           'IS THE BUILDING VACANT DUE TO FIRE?',
           'ANY PEOPLE USING PROPERTY? (HOMELESS, CHILDEN, GANGS)',
           'ADDRESS STREET NUMBER', 'ADDRESS STREET DIRECTION',
           'ADDRESS STREET NAME', 'ADDRESS STREET SUFFIX', 'ZIP CODE',
           'X COORDINATE', 'Y COORDINATE', 'Ward', 'Police District',
           'Community Area', 'LATITUDE', 'LONGITUDE', 'Location'],
          dtype='object')




```python
vehicles_call_counts = vehicles.groupby('Community Area')[['Type of Service Request']].count()
vehicles_call_counts.rename(columns={'Type of Service Request': 'call_counts_vehicle'}, inplace=True)
```


```python
vehicles_call_counts
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
      <th>call_counts_vehicle</th>
    </tr>
    <tr>
      <th>Community Area</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0.0</th>
      <td>63</td>
    </tr>
    <tr>
      <th>1.0</th>
      <td>778</td>
    </tr>
    <tr>
      <th>2.0</th>
      <td>1217</td>
    </tr>
    <tr>
      <th>3.0</th>
      <td>442</td>
    </tr>
    <tr>
      <th>4.0</th>
      <td>751</td>
    </tr>
    <tr>
      <th>5.0</th>
      <td>675</td>
    </tr>
    <tr>
      <th>6.0</th>
      <td>878</td>
    </tr>
    <tr>
      <th>7.0</th>
      <td>549</td>
    </tr>
    <tr>
      <th>8.0</th>
      <td>341</td>
    </tr>
    <tr>
      <th>9.0</th>
      <td>125</td>
    </tr>
    <tr>
      <th>10.0</th>
      <td>568</td>
    </tr>
    <tr>
      <th>11.0</th>
      <td>740</td>
    </tr>
    <tr>
      <th>12.0</th>
      <td>291</td>
    </tr>
    <tr>
      <th>13.0</th>
      <td>415</td>
    </tr>
    <tr>
      <th>14.0</th>
      <td>692</td>
    </tr>
    <tr>
      <th>15.0</th>
      <td>1590</td>
    </tr>
    <tr>
      <th>16.0</th>
      <td>1648</td>
    </tr>
    <tr>
      <th>17.0</th>
      <td>1237</td>
    </tr>
    <tr>
      <th>18.0</th>
      <td>361</td>
    </tr>
    <tr>
      <th>19.0</th>
      <td>1434</td>
    </tr>
    <tr>
      <th>20.0</th>
      <td>405</td>
    </tr>
    <tr>
      <th>21.0</th>
      <td>1025</td>
    </tr>
    <tr>
      <th>22.0</th>
      <td>1609</td>
    </tr>
    <tr>
      <th>23.0</th>
      <td>970</td>
    </tr>
    <tr>
      <th>24.0</th>
      <td>1484</td>
    </tr>
    <tr>
      <th>25.0</th>
      <td>1681</td>
    </tr>
    <tr>
      <th>26.0</th>
      <td>293</td>
    </tr>
    <tr>
      <th>27.0</th>
      <td>476</td>
    </tr>
    <tr>
      <th>28.0</th>
      <td>512</td>
    </tr>
    <tr>
      <th>29.0</th>
      <td>528</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>48.0</th>
      <td>286</td>
    </tr>
    <tr>
      <th>49.0</th>
      <td>767</td>
    </tr>
    <tr>
      <th>50.0</th>
      <td>133</td>
    </tr>
    <tr>
      <th>51.0</th>
      <td>186</td>
    </tr>
    <tr>
      <th>52.0</th>
      <td>474</td>
    </tr>
    <tr>
      <th>53.0</th>
      <td>496</td>
    </tr>
    <tr>
      <th>54.0</th>
      <td>29</td>
    </tr>
    <tr>
      <th>55.0</th>
      <td>109</td>
    </tr>
    <tr>
      <th>56.0</th>
      <td>787</td>
    </tr>
    <tr>
      <th>57.0</th>
      <td>369</td>
    </tr>
    <tr>
      <th>58.0</th>
      <td>980</td>
    </tr>
    <tr>
      <th>59.0</th>
      <td>495</td>
    </tr>
    <tr>
      <th>60.0</th>
      <td>913</td>
    </tr>
    <tr>
      <th>61.0</th>
      <td>656</td>
    </tr>
    <tr>
      <th>62.0</th>
      <td>529</td>
    </tr>
    <tr>
      <th>63.0</th>
      <td>681</td>
    </tr>
    <tr>
      <th>64.0</th>
      <td>659</td>
    </tr>
    <tr>
      <th>65.0</th>
      <td>957</td>
    </tr>
    <tr>
      <th>66.0</th>
      <td>932</td>
    </tr>
    <tr>
      <th>67.0</th>
      <td>441</td>
    </tr>
    <tr>
      <th>68.0</th>
      <td>396</td>
    </tr>
    <tr>
      <th>69.0</th>
      <td>647</td>
    </tr>
    <tr>
      <th>70.0</th>
      <td>696</td>
    </tr>
    <tr>
      <th>71.0</th>
      <td>856</td>
    </tr>
    <tr>
      <th>72.0</th>
      <td>154</td>
    </tr>
    <tr>
      <th>73.0</th>
      <td>439</td>
    </tr>
    <tr>
      <th>74.0</th>
      <td>128</td>
    </tr>
    <tr>
      <th>75.0</th>
      <td>214</td>
    </tr>
    <tr>
      <th>76.0</th>
      <td>101</td>
    </tr>
    <tr>
      <th>77.0</th>
      <td>651</td>
    </tr>
  </tbody>
</table>
<p>78 rows × 1 columns</p>
</div>




```python
graffiti_call_counts = graffiti.groupby('Community Area')[['Type of Service Request']].count()
graffiti_call_counts.rename(columns={'Type of Service Request': 'call_counts_graffiti'}, inplace=True)
```


```python
building_call_counts = buildings.groupby('Community Area')[['SERVICE REQUEST TYPE']].count()
building_call_counts.rename(columns={'SERVICE REQUEST TYPE': 'call_counts_building'}, inplace=True)
```


```python
# More censes data can be included if we want
community_names = census[['Community Area Name', 'Community Area Number', 'Hardship Index']]

community_names = community_names.merge(vehicles_call_counts, left_on='Community Area Number', right_index=True, how='left')
community_names = community_names.merge(graffiti_call_counts, left_on='Community Area Number', right_index=True, how='left')
community_names = community_names.merge(building_call_counts, left_on='Community Area Number', right_index=True, how='left')
```


```python
community_names.head()
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
      <th>Community Area Name</th>
      <th>Community Area Number</th>
      <th>Hardship Index</th>
      <th>call_counts_vehicle</th>
      <th>call_counts_graffiti</th>
      <th>call_counts_building</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rogers Park</td>
      <td>1.0</td>
      <td>39.0</td>
      <td>778.0</td>
      <td>5009.0</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>West Ridge</td>
      <td>2.0</td>
      <td>46.0</td>
      <td>1217.0</td>
      <td>4353.0</td>
      <td>139.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Uptown</td>
      <td>3.0</td>
      <td>20.0</td>
      <td>442.0</td>
      <td>4129.0</td>
      <td>79.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lincoln Square</td>
      <td>4.0</td>
      <td>17.0</td>
      <td>751.0</td>
      <td>3969.0</td>
      <td>91.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>North Center</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>675.0</td>
      <td>4606.0</td>
      <td>105.0</td>
    </tr>
  </tbody>
</table>
</div>



### 3. What sort of trends can you identify? How would you do so (via plotting, analysis, etc.)?


```python
community_names.plot.scatter(x='call_counts_building', y='Hardship Index')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x235e2119860>




![png](/img/output_25_1.png)



```python
import seaborn as sns
f,ax1 = plt.subplots(figsize =(20,10))
sns.pointplot(x='Community Area Name',y='call_counts_graffiti',data=community_names,color='green',alpha=1)
plt.grid()
```


![png](/img/output_26_0.png)


### 4. What sorts of questions would you want to use this data to answer?


```python
# You may want to see if any of the census information is associated with 311 calls, perhaps the hardship index and graffiti removal calls.
# Explore the locations of abandoned buildings over time and see if there is a pattern
# See what kind of vehicles are most likely to be abandoned in Chicago
```
