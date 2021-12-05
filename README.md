# crypto_kmeans
Using k-means to cluster a potential crypto portfolio for optimization.

## Technologies

In this project we are utilizing Python 3, Jupyter Lab, Pandas, scikit learn and hvplot.   

Pandas library -- Incredibly useful Python library for data science and data analysis  
Jupyter Lab -- Robust environment to be able to view and edit devopment projects in a streamlined system.  
hvPlot -- A high-level plotting API for the PyData ecosystem built on HoloViews.
scikit learn -- a free software machine learning library for the Python programming language.

---

## Installation Guide

* Pandas -- The source code is currently hosted on GitHub at: https://github.com/pandas-dev/pandas

Binary installers for the latest released version are available at the Python Package Index (PyPI) and on Conda.

### conda
`conda install pandas`
### or PyPI
`pip install pandas`

* Jupyter Lab -- 
    [Link for detailed instructions on installing Jupyter Lab here.](https://jupyter.org/install)  
    
*  The PyViz Ecosystem (visualization package that includes hvPlot)  

### conda
`conda install -c pyviz hvplot`
### or PyPI
`pip install pyviz`  

**For more detailed information on pyviz installation and other features, please reference the [pyviz website](https://pyviz.org/)
 

*  scikit learn --  
    [Click here for link to their homepage for detailed installation instructions and other documentation](https://scikit-learn.org/stable/) 
    
---
## Dependencies:  

import pandas as pd
import hvplot.pandas
from pathlib import Path
from sklearn.cluster import KMeans
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

## Usage

## We start by finding the optimal number of clusters(k) for our data using the KMeans method from scikit learn and analyzing our 'elbow plot'  

```python  
for i in k:
    model = KMeans(n_clusters=i, random_state=1)
    model.fit(df_market_data_scaled)
    inertia.append(model.inertia_)  
```  
*Above we fit the model to iterate over a pre-defined range for i (1 to 11), and then append the inertia values to a list for plotting our elbow curve  

```python  
df_elbow.hvplot.line(x='k', y='inertia', xticks=k, title='Elbow Curve')  
```  
*Notice the plot above shows the 'elbow' indicates the optimal value for k or the number of clusters is 4  


  
pypl_dataframe = pd.read_sql(query, con=engine, parse_dates=['time'], index_col='time')
```

**Tail of generated DataFrame:
	open	high	low	close	volume	daily_returns
time						
2020-11-30	212.51	215.83	207.0900	214.200	8992681	0.013629
2020-12-01	217.15	220.57	214.3401	216.520	9148174	0.010831
2020-12-02	215.60	215.75	210.5000	212.660	6414746	-0.017827
2020-12-03	213.33	216.93	213.1100	214.680	6463339	0.009499
2020-12-04	214.88	217.28	213.0100	217.235	2118319	0.011901

# We utilize conditional SELECT statements in SQL to extract specific data we are looking for:  

```python

query = '''
SELECT time, close 
FROM PYPL
WHERE close > 200.0'''  
```  
**Limiting the number of responses within a SQL query:**  

```python
query = '''
SELECT time, daily_returns FROM PYPL
ORDER BY daily_returns DESC
LIMIT 10;
'''
```
**Output from our limited query:  
    	daily_returns
time	
2020-03-24	0.140981
2020-05-07	0.140318
2020-03-13	0.138700
2020-04-06	0.100877
2018-10-19	0.093371
2019-10-24	0.085912
2020-11-04	0.080986
2020-03-10	0.080863
2020-04-22	0.075321
2018-12-26	0.074656


# We concatenate multiple tables from our SQL database using an 'INNER JOIN' on the 'time' column from each table  

```python
query = '''
SELECT *
FROM GDOT
INNER JOIN GS ON GDOT.time = GS.time
INNER JOIN PYPL ON GS.time = PYPL.time
INNER JOIN SQ ON PYPL.time = SQ.time;
'''
```
## We can then utilize the resulting database to isolate 'daily_returns' and perform cumulative return analyses and plots, among others  
```python
daily_returns_df = pd.DataFrame(etf_portfolio[['time','daily_returns']])
```
## Lastly, we run our notebook as a web app using 'Voila'.  A screen recording of the resulting web app can be retrieved below --

**To run our web app we simply input `voila` into the terminal.  
  The screen recording of the resulting web app can be viewed [here](./screen-capture.webm)


## License

Licensed under the [MIT License](https://github.com/git/git-scm.com/blob/main/MIT-LICENSE.txt)  Copyright 2021 Dave Thomas.


