---
title:  "Interactive Process to Examine Independent Variable"
---

In explanatory data analysis one of the most important part is to visualize relationship between dependent variable and independent variable.

To ease the process in this blog I'll try to develop an interactive process to visualize relationship with each and every independent variable.

There will be dropdown list which will list all predictor variables. User'll able to select any variable including object and numeric types. Based on selection if selected variable is object it'll plot countplot and boxplot. Otherwise, it'll plot density along with scatter.

I am hoping this utility will save some time as well as very focused look of variables we want to examine.

**Import Necessary Library**


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import ipywidgets as widgets
from ipywidgets import interact, interactive, fixed, interact_manual, Output
from IPython.display import clear_output
```

We'll start the process by loading csv data using panda.


```python
# Load sample data
df = pd.read_csv('./housing.csv')
house = df.copy()
```

After loading the data check the data for possible dependent variable.


```python
# Sale Price is our target variable
dependent_variable = 'SalePrice'

# All columns but SalePrice is our independent variable
independent_variable = [l for l in house.columns if l != dependent_variable]
```

This is the trigger function which will manage all plotting. This function will fire whenever user changes value in dropdownlist.

First, clear the output window if there are something already. Check variable type. If it's a object type plot countplot and boxplot. Otherwise plot a scatterplot where we'll get the relationship.


```python
# Triigger function
def get_and_plot(change):
    with out:
        clear_output()
        if house[select_variable.value].dtype != 'object':
            sns.jointplot(x=house[select_variable.value], y=house[dependent_variable], data=house, kind="reg")
        else:
            fig, axs = plt.subplots(nrows=2, ncols = 1, figsize=(10, 10))
            ax = sns.boxplot(x=select_variable.value, y=dependent_variable, data=house, ax=axs[0])
            ax = sns.countplot(x=select_variable.value, data=house, ax=axs[1])
        plt.show()
```

Here we are building the dropdown widget using python widget.


```python
# Dropdown list
select_variable = widgets.Dropdown(
    options = independent_variable,
    value = independent_variable[0],
    description = 'Columns:',
    disabled=False
)

# Trigger
select_variable.observe(get_and_plot, names='value')
```

Finally, interact with user. User can select any variable and see if there are any interesting insight.


```python
# Output
display(select_variable)
out = Output()
display(out)
```


<p>Failed to display Jupyter Widget of type <code>Dropdown</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>




<p>Failed to display Jupyter Widget of type <code>Output</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>



**Happy Exploring!**
