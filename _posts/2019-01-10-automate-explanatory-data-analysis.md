---
title:  "Automate Exploratory Data Analysis"
---

<a id='eda-definition'></a>

## What is Exploratory Data Analysis?

---

Exploratory Data Analysis (EDA) is the first step in our data analysis process. Here, we make sense of the data we have and then figure out what questions we want to ask and how to frame them, as well as how best to manipulate our available data sources to get the answers we need.

In short, we’re looking for clues that suggest our logical next steps, questions or areas of research.

> Exploratory Data Analysis refers to the critical process of performing initial investigations on data so as to discover patterns, to spot anomalies, to test hypothesis and to check assumptions with the help of summary statistics and graphical representations.

There are some tasks we need to perform almost always. In this blog I'll explore if there are something we can automate which will help us to improve our productivity.

To starts with, **Import Necessary Libraries**


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

% matplotlib inline
```

**Load Dataset using Panda**


```python
def dataframe_readcsv(csvFileName):
    '''
    Helper function that gives a dataframe of a given csv filename

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    df = pd.read_csv(csvFileName)
    return df
```


```python
def dataframe_shape(df):
    '''
    Helper function that gives a shape of a given dataframe

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    print('\n')
    print('='*80)

    print('Shape:')
    print(df.shape)
```


```python
def dataframe_dtypesame_head(df):
    '''
    Helper function that gives a datatypes of a given dataframe

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    print('\n')
    print('='*80)

    print('Head:')
    print(df.head())
```


```python
def dataframe_tail(df):
    '''
    Helper function that gives a tail of a given dataframe

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    print('\n')
    print('='*80)

    print('Tail:')
    print(df.tail())

```

It is also a good practice to know the columns and their corresponding data types.


```python
def dataframe_dtypes(df):
    '''
    Helper function that gives a data types of a given dataframe

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    print('\n')
    print('='*80)

    print('Data Types:')
    print(df.dtypes)

```


```python
def dataframe_info(df):
    '''
    Helper function that gives a info of a given dataframe

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    print('\n')
    print('='*80)

    print('Info:')
    print(df.info())
```

There are two types of data: qualitative and quantitative. Both types of data have strengths and limitations and may be appropriate for different settings, evaluation designs, and evaluation questions.

Quantitative data are numerical information, the analysis of which involves statistical techniques. The type of data you collect guides the analysis process.

- Requires use of statistical analysis
- Variables can be identified and relationships measured
- Counted or expressed numerically
- Often perceived as a more objective method of data analysis
- Typically collected with surveys or questionnaires
- Often represented visually using graphs or charts



```python
def quantitative_summarized(dataframe, x=None, y=None, hue=None, palette='Set1', ax=None, verbose=True, swarm=False):
    '''
    Helper function that gives a quick summary of quantattive data
    Arguments
    =========
    dataframe: pandas dataframe
    x: str. horizontal axis to plot the labels of categorical data (usually the target variable)
    y: str. vertical axis to plot the quantitative data
    hue: str. if you want to compare it another categorical variable (usually the target variable if x is another variable)
    palette: array-like. Colour of the plot
    swarm: if swarm is set to True, a swarm plot would be overlayed
    Returns
    =======
    Quick Stats of the data and also the box plot of the distribution
    '''
    series = dataframe[y]
    print(series.describe())
    print('mode: ', series.mode())
    if verbose:
        print('='*80)
        print(series.value_counts())

    sns.boxplot(x=x, y=y, hue=hue, data=dataframe, palette=palette, ax=ax)

    if swarm:
        sns.swarmplot(x=x, y=y, hue=hue, data=dataframe,
                      palette=palette, ax=ax)

    plt.show()
```

Qualitative data consist of words and narratives. The analysis of qualitative data can come in many forms including highlighting key words, extracting themes, and elaborating on concepts.

- Examines non-numerical data for patterns and meanings
- Often described as being more “rich” than quantitative data
- Is gathered and analyzed by an individual, it can be more subjective
- Can be collected through methods such as observation techniques, focus groups, interviews, and case studies


```python
def categorical_summarized(dataframe, x=None, y=None, hue=None, palette='Set1', ax=None, verbose=True):
    '''
    Helper function that gives a quick summary of a given column of categorical data
    Arguments
    =========
    dataframe: pandas dataframe
    x: str. horizontal axis to plot the labels of categorical data, y would be the count
    y: str. vertical axis to plot the labels of categorical data, x would be the count
    hue: str. if you want to compare it another variable (usually the target variable)
    palette: array-like. Colour of the plot|
    Returns
    =======
    Quick Stats of the data and also the count plot
    '''
    if x == None:
        column_interested = y
    else:
        column_interested = x
    series = dataframe[column_interested]
    print(series.describe())
    print('mode: ', series.mode())
    if verbose:
        print('='*80)
        print(series.value_counts())

    sns.countplot(x=x, y=y, hue=hue, data=dataframe, palette=palette, ax=ax)
    plt.show()
```


```python
def init_numeric_types(df):
    '''
    Helper function that gives a quick summary of quantattive data

    Arguments
    =========
    dataframe: pandas dataframe

    Returns
    =======
    Quick Stats of the data and also the box plot of the distribution
    '''
    print('\n')
    print('Numeric Data Types:')
    numeric_columns = df.select_dtypes(include=[np.number]).columns.tolist()
    for o in numeric_columns:
        try:
            print('\n')
            print(f'{o}')
            quantitative_summarized(df, y=o)
        except:
            continue
```


```python
def init_object_types(df):
    '''
    Helper function that gives a quick summary of a given column of categorical data

    Arguments
    =========
    dataframe: pandas dataframe

    Returns
    =======
    Quick Stats of the data and also the count plot
    '''
    print('\n')    
    print('Object Data Types:')
    object_columns = df.select_dtypes(include=[np.object]).columns.tolist()
    for o in object_columns:
        print('\n')
        print(f'{o}')
        categorical_summarized(df, x=o)
```


```python
def init_dataframe(csvFileName, shape=False, head=False, tail=False, dtypes=False, info=False, summaryObject=False, summaryNumeric=False):
    '''
    Helper function that gives a a high level summary of a given dataframe

    Arguments
    =========
    dataframe: pandas dataframe
    '''
    df = pd.read_csv(csvFileName)

    if shape == True:
        dataframe_shape(df)

    if head == True:
        dataframe_head(df)

    if tail == True:
        dataframe_tail(df)

    if dtypes == True:
        dataframe_dtypes(df)

    if info == True:
        dataframe_info(df)

    if summaryObject == True:
        init_object_types(df)

    if summaryNumeric == True:
        init_numeric_types(df)
```

Last of all I have created a python file and put all these methods there. All I need to do next time is using this library, I can get a quick EDA of my dataset.

It was a fun exercise. Please share your ideas also.


```python
% matplotlib inline
import auto_eda

csvFileName = './datasets/sacramento_real_estate_transactions.csv'
auto_eda.init_dataframe(csvFileName, shape=True, head=True, tail=True, dtypes=True, info=True, summaryObject=True, summaryNumeric=True)
```
---

You can find the jupyter notebook [here](https://github.com/ikfaisal/linear-regression/blob/master/AutoEDA.ipynb).
