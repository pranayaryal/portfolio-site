---
layout: post
title: Plot feature importance
image: img/speeches-cover.jpg
author: Pranay Aryal
date: 2018-08-10T10:00:00.000Z
tags:
  - Python
---

This is how you can plot feature importances.
```py
def plot_feature_importances(df):
    df = df.sort_values('importance', ascending=False).reset_index().head(10)
    
    plt.figure(figsize=(16, 10))
    
    fig, ax = plt.subplots()
    
    ax.barh(df['feature'], df['importance'], align="center", color='green')
    ax.invert_yaxis()
    ax.set_xlabel("Importance")
    ax.set_title('Feature importance')
    plt.show()
```


#### Pair plots for EDA

```py
# Copy the data for plotting
plot_data = ext_data.drop(columns = ['DAYS_BIRTH']).copy()
 
# Add in the age of the client in years
plot_data['YEARS_BIRTH'] = age_data['YEARS_BIRTH']
 
# Drop na values and limit to first 100000 rows
plot_data = plot_data.dropna().loc[:100000, :]
 
# Function to calculate correlation coefficient between two columns
def corr_func(x, y, **kwargs):
    r = np.corrcoef(x, y)[0][1]
    ax = plt.gca()
    ax.annotate("r = {:.2f}".format(r),
                xy=(.2, .8), xycoords=ax.transAxes,
                size = 20)
 
# Create the pairgrid object
grid = sns.PairGrid(data = plot_data, size = 3, diag_sharey=False,
                    hue = 'TARGET', 
                    vars = [x for x in list(plot_data.columns) if x != 'TARGET'])
 
# Upper is a scatter plot
grid.map_upper(plt.scatter, alpha = 0.2)
```