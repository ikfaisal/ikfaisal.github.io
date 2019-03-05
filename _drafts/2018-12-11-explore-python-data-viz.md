---
title:  "Guided Practice: Explore Data Visualization"
categories: generalassembly python dataviz
---
![image tooltip here](http://imgur.com/1ZcRyrc.png){:height="36px" width="36px"}
---

In this guided practice lab you will use Pandas, Matplotlib, and Seaborn to create simple plots.

We'll cover plotting line plots, scatter plots, bar plots, histograms, and how to manipulate the style of your plots with Matplotlib.

We will use primarily the Boston Housing data from the UCI repository.


```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

plt.style.use('fivethirtyeight')
%matplotlib inline
```

### Pandas plotting documentation

[Link to Documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html)

### Create fake data for examples


```python
df = pd.DataFrame(np.random.randn(10, 4),
                  columns=['col1', 'col2', 'col3', 'col4'],
                  index=['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'])
```


```python
kind = ['line', 'bar', 'barh', 'hist', 'box', 'kde', 'density', 'area', 'pie', 'scatter', 'hexbin']

for k in kind:
    if (k not in ['area', 'pie', 'scatter', 'hexbin']):
        ax = df[['col1', 'col4']].plot(kind=k)

```


![png](/img/output_5_0.png)



![png](/img/output_5_1.png)



![png](/img/output_5_2.png)



![png](/img/output_5_3.png)



![png](/img/output_5_4.png)



![png](/img/output_5_5.png)



![png](/img/output_5_6.png)


### Load in Boston housing data for exercises

The data dictionary can be found [here](https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.names)


```python
housing_csv = './assets/datasets/boston_housing_data.csv'
housing = pd.read_csv(housing_csv)
```


```python
housing.describe().T
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
      <th>CRIM</th>
      <td>506.0</td>
      <td>1.716290</td>
      <td>2.653510</td>
      <td>0.00632</td>
      <td>0.0819</td>
      <td>0.250895</td>
      <td>2.326718</td>
      <td>9.96654</td>
    </tr>
    <tr>
      <th>ZN</th>
      <td>506.0</td>
      <td>11.363636</td>
      <td>23.322453</td>
      <td>0.00000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>12.500000</td>
      <td>100.00000</td>
    </tr>
    <tr>
      <th>INDUS</th>
      <td>506.0</td>
      <td>11.136779</td>
      <td>6.860353</td>
      <td>0.46000</td>
      <td>5.1900</td>
      <td>9.690000</td>
      <td>18.100000</td>
      <td>27.74000</td>
    </tr>
    <tr>
      <th>CHAS</th>
      <td>506.0</td>
      <td>0.069170</td>
      <td>0.253994</td>
      <td>0.00000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>NOX</th>
      <td>506.0</td>
      <td>0.554695</td>
      <td>0.115878</td>
      <td>0.38500</td>
      <td>0.4490</td>
      <td>0.538000</td>
      <td>0.624000</td>
      <td>0.87100</td>
    </tr>
    <tr>
      <th>RM</th>
      <td>506.0</td>
      <td>6.284634</td>
      <td>0.702617</td>
      <td>3.56100</td>
      <td>5.8855</td>
      <td>6.208500</td>
      <td>6.623500</td>
      <td>8.78000</td>
    </tr>
    <tr>
      <th>AGE</th>
      <td>506.0</td>
      <td>68.574901</td>
      <td>28.148861</td>
      <td>2.90000</td>
      <td>45.0250</td>
      <td>77.500000</td>
      <td>94.075000</td>
      <td>100.00000</td>
    </tr>
    <tr>
      <th>DIS</th>
      <td>506.0</td>
      <td>3.696228</td>
      <td>1.999689</td>
      <td>0.58570</td>
      <td>2.0737</td>
      <td>3.107300</td>
      <td>5.112625</td>
      <td>9.22290</td>
    </tr>
    <tr>
      <th>RAD</th>
      <td>506.0</td>
      <td>4.332016</td>
      <td>1.417166</td>
      <td>1.00000</td>
      <td>4.0000</td>
      <td>4.000000</td>
      <td>5.000000</td>
      <td>8.00000</td>
    </tr>
    <tr>
      <th>TAX</th>
      <td>506.0</td>
      <td>408.237154</td>
      <td>168.537116</td>
      <td>187.00000</td>
      <td>279.0000</td>
      <td>330.000000</td>
      <td>666.000000</td>
      <td>711.00000</td>
    </tr>
    <tr>
      <th>PTRATIO</th>
      <td>506.0</td>
      <td>18.455534</td>
      <td>2.164946</td>
      <td>12.60000</td>
      <td>17.4000</td>
      <td>19.050000</td>
      <td>20.200000</td>
      <td>22.00000</td>
    </tr>
    <tr>
      <th>B</th>
      <td>506.0</td>
      <td>356.674032</td>
      <td>91.294864</td>
      <td>0.32000</td>
      <td>375.3775</td>
      <td>391.440000</td>
      <td>396.225000</td>
      <td>396.90000</td>
    </tr>
    <tr>
      <th>LSTAT</th>
      <td>506.0</td>
      <td>12.653063</td>
      <td>7.141062</td>
      <td>1.73000</td>
      <td>6.9500</td>
      <td>11.360000</td>
      <td>16.955000</td>
      <td>37.97000</td>
    </tr>
    <tr>
      <th>MEDV</th>
      <td>506.0</td>
      <td>22.532806</td>
      <td>9.197104</td>
      <td>5.00000</td>
      <td>17.0250</td>
      <td>21.200000</td>
      <td>25.000000</td>
      <td>50.00000</td>
    </tr>
  </tbody>
</table>
</div>




```python
for k in kind:
    if (k not in ['area', 'pie', 'scatter', 'hexbin']):
        housing[['TAX', 'AGE']].plot(kind=k)
```

## Line plots
---


```python
housing.plot(kind='line')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab34032a90>




![png](/img/output_11_1.png)


### Line plot with a DataFrame


```python
housing.plot(kind='line')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab33fe2c18>




![png](/img/output_13_1.png)


### Line plot with a Series


```python
housing['CRIM'].plot(kind='line')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab340ef748>




![png](/img/output_15_1.png)


### Change the size of a plot


```python
housing['CRIM'].plot(kind='line', figsize=(15, 8))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab339fa438>




![png](/img/output_17_1.png)


### Change the color of a plot


```python
housing['CRIM'].plot(kind='line', color='crimson', figsize=(15, 8))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab39a90ef0>




![png](/img/output_19_1.png)


### Change the style of individual lines


```python
housing['CRIM'].plot(kind='line', figsize=(15, 8), style={'CRIM': 'vb'})
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab39c2cb00>




![png](/img/output_21_1.png)


### Create a line plot of ZN and INDUS in the housing data. For ZN use a solid green line and for INDUS use a blue dashed line.

- Set the width to 12 and the height to 8.
- Change the style sheet to something you find here [Style Sheets](https://tonysyu.github.io/raw_content/matplotlib-style-gallery/gallery.html)

To use solid green line we are using 'g'
To use dashed line '--' and color blue 'b'


```python
columns_list = ['ZN', 'INDUS']
graph_size = (12,8)
graph_style = {'ZN':'g', 'INDUS':'--b'}

housing[columns_list].plot(figsize=graph_size, style=graph_style)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab35add828>




![png](/img/output_24_1.png)


## Bar Plots
---

### Bar plot from a series


```python
ax = housing['ZN'].plot(kind='bar', figsize=graph_size)
```


![png](/img/output_27_0.png)


### Using a DataFrame and Matplotlib commands we can get fancy


```python
ax = housing['ZN'].plot(kind='bar', figsize=graph_size)

# set the title

ax.set_title('Set The Title')

# move the legend

ax.legend(loc=1)

# x-axis labels

ax.set_xlabel('x-axis Labels')

# y-axis labels

ax.set_ylabel('y-axis Labels')

```




    Text(0,0.5,'y-axis Labels')




![png](/img/output_29_1.png)


### Horizontal bar plot


```python
housing['INDUS'].plot(kind='barh',figsize=graph_size)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab41a14eb8>




![png](/img/output_31_1.png)


### Create a bar chart using col1 and col2.
- Give it a large title of your choosing.
- Move the legend to the lower-left corner.


```python
ax = df[['col1', 'col2']].plot(kind='bar', figsize=graph_size)

ax.set_title('Give it a large title of your choosing')
ax.legend(loc=3)
```




    <matplotlib.legend.Legend at 0x1ab36645470>




![png](/img/output_33_1.png)


- Do the same thing but with horizontal bars.
- Move the legend to the upper right.


```python
ax = df[['col1', 'col2']].plot(kind='barh', figsize=graph_size)

ax.set_title('Do the same thing but with horizontal bars', fontdict={'fontsize': 22})
ax.legend(loc=1)
```




    <matplotlib.legend.Legend at 0x1ab45a75ac8>




![png](/img/output_35_1.png)


### We can use stacked bars


```python
ax = df[['col1', 'col2']].plot(kind='bar', stacked=True, figsize=graph_size)
```


![png](/img/output_37_0.png)


### Stacked works on horizontal barcharts


```python
ax = df[['col1', 'col2']].plot(kind='barh', stacked=True, figsize=graph_size)
```


![png](/img/output_39_0.png)


### Plot the `.value_counts()` of `CHAS` using a bar chart


```python
value_counts_df = housing['CHAS'].value_counts()

value_counts_df.plot(kind='bar', figsize=graph_size)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab461a6c50>




![png](/img/output_41_1.png)


### Create a vertical stacked bar chart using col1 and col2
- What happens when you use `df[['col1', 'col2']]` vs. `df[['col2', 'col1']]`?


```python
df[['col1', 'col2']].plot(kind='barh')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab47a69630>




![png](/img/output_43_1.png)



```python
df[['col2', 'col1']].plot(kind='barh')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab465b59b0>




![png](/img/output_44_1.png)


### Create a horizontal stacked bar chart using all columns from df


```python
df.plot(kind='barh', figsize=graph_size)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab47e53438>




![png](/img/output_46_1.png)


## Histograms
---



```python
# A:

housing.hist()
```




    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x000001AB47E6BE48>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB482BFEF0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB47F44EF0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB47F8A550>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x000001AB47FA8518>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB47FC06D8>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB4801FB70>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB48059C50>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x000001AB4808FD30>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB480B0128>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB480FBA20>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB482E1EF0>],
           [<matplotlib.axes._subplots.AxesSubplot object at 0x000001AB483029B0>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB4835D358>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB4838F048>,
            <matplotlib.axes._subplots.AxesSubplot object at 0x000001AB483C3668>]],
          dtype=object)




![png](/img/output_48_1.png)


### Single historgram


```python
norm = np.random.standard_normal(5000)
```


```python
pd.DataFrame(norm).hist()
```




    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x000001AB485C8B70>]],
          dtype=object)




![png](/img/output_51_1.png)


### Bins param adjusts the no. of bins


```python
pd.DataFrame(norm).hist(bins=50)
```




    array([[<matplotlib.axes._subplots.AxesSubplot object at 0x000001AB48652748>]],
          dtype=object)




![png](/img/output_53_1.png)


### Create a histogram with pandas for using `MEDV` in the housing data.
- Set the bins to 20.


```python
# A:

ax = housing['MEDV'].plot(kind='hist', bins=20)

ax.set_title('Histogram with pandas for using MEDV')
```




    Text(0.5,1,'Histogram with pandas for using MEDV')




![png](/img/output_55_1.png)


## Boxplots
---

We can use boxplots to quickly summarize distributions


```python
# A:

df.boxplot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab48a7b320>




![png](/img/output_57_1.png)


### Use a boxplot to preview the distributions in the housing data


```python
housing.boxplot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab48a68a58>




![png](/img/output_59_1.png)


## Scatter Plots
---

> You interpret a scatterplot by looking for trends in the data as you go from left to right.

- If the data show an uphill pattern as you move from left to right, this indicates a positive relationship between X and Y. As the X-values increase (move right), the Y-values tend to increase (move up).

- If the data show a downhill pattern as you move from left to right, this indicates a negative relationship between X and Y. As the X-values increase (move right) the Y-values tend to decrease (move down).

- If the data don’t seem to resemble any kind of pattern (even a vague one), then no relationship exists between X and Y.


```python
df.plot(x='col3', y='col4', kind='scatter', color='dodgerblue', figsize=(15,7), s=250)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab48c65828>




![png](/img/output_62_1.png)


### View the association between the variables `"ZN"` and `"INDUS"` using a scatter plot.


```python
# A:

housing.plot(x=['ZN'], y=['INDUS'], kind='scatter', figsize=(7,5), s=100)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab49cbf550>




![png](/img/output_64_1.png)


### Use a list comprehension to change the size of the scatter plot dots based on `DIS`


```python
ax = housing.plot(x='ZN', y='INDUS', kind='scatter', color='b', figsize=(15,7))
ax.set_title('The Scatter Plot Dots Based on DIS', fontdict={'fontsize':18})
```




    Text(0.5,1,'The Scatter Plot Dots Based on DIS')




![png](/img/output_66_1.png)


## Seaborn `pairplot`

---

With the dataframe object `housing`, we will render a pairplot using the Seaborn library.
What do each of the elements represent? Is this more or less useful than the previous plot?


```python
# A:

sns.pairplot(housing)
```




    <seaborn.axisgrid.PairGrid at 0x1ab48caef60>




![png](/img/output_68_1.png)


## Seaborn `heatmap`
---

When you have too many variables, a pairplot or scatter matrix can become impossible to read. We can still gauge linear correlation using a heatmap of the correlation matrix.


```python
# A:
housing_corr = housing.corr()
sns.heatmap(housing_corr)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab52a87518>




![png](/img/output_70_1.png)


## Understanding figures, subplots, and axes

---

Matplotlib uses a blank canvas called a figure


```python
# A:

fig, axes = plt.subplots(2, 3, figsize=(16, 8))
```


![png](/img/output_73_0.png)


Within this canvas, we can contain smaller objects called axes


```python
fig, axes = plt.subplots(2, 3, figsize=(16,8))
df.plot(ax=axes[0][0])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab551b9b00>




![png](/img/output_75_1.png)


Pandas allows us to plot to a specified axes if we pass the object to the ax paramter.


```python
df['col1'].plot(ax=axes[0][1])
df['col2'].plot(ax=axes[0][1])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1ab55960550>



## Let's use a bit more customization
---


```python
fig, axes = plt.subplots(2,2, figsize=(16,8))

# We can change the ticks' size
df['col2'].plot(figsize=(16,4), color='purple', fontsize=21, ax=axes[0][0])

# We can also change which ticks are visible
# list comprehension to get only the even ticks
ticks_to_show = [idx for idx, _ in enumerate(df['col2'].index) if idx % 2 == 0]
df['col2'].plot(figsize=(16,4), color='purple', xticks=ticks_to_show, fontsize=16, ax=axes[0][1])

# We can change the label rotation
df.plot(figsize=(15,7), title='Big Rotated Labels - Tiny Title',\
        fontsize=20, rot=-50, ax=axes[1][0])\

# We have to use .set_title() to fix title size
df.plot(figsize=(16,8), fontsize=20, rot=-50, ax=axes[1][1])\
       .set_title('Better-Sized Title', fontsize=21, y=1.01)

```




    Text(0.5,1.01,'Better-Sized Title')




![png](/img/output_79_1.png)
