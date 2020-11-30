
<h1 align='center'>The Winton Stock Market Challenge</h1>

[Winton Stock Market Challenge](https://www.kaggle.com/c/the-winton-stock-market-challenge/overview) was a competition hosted by Winton on Kaggle in 2016.
The main task of this competition was predict the interday and intraday return of a stock, given the history of the past few days.
<br>
__NOTE:__<br>
To view the final code with the interactive graphs, [click here](https://nbviewer.jupyter.org/github/chawla201/The-Winton-Stock-Market-Challenge/blob/master/Final%20code.ipynb) 


## Data

In this competition the challenge is to predict the return of a stock, given the history of the past few days. 

We provide 5-day windows of time, days D-2, D-1, D, D+1, and D+2. You are given returns in days D-2, D-1, and part of day D, and you are asked to predict the returns in the rest of day D, and in days D+1 and D+2.

During day D, there is intraday return data, which are the returns at different points in the day. We provide 180 minutes of data, from t=1 to t=180. In the training set you are given the full 180 minutes, in the test set just the first 120 minutes are provided.

For each 5-day window, we also provide 25 features, Feature_1 to Feature_25. These may or may not be useful in your prediction.

Each row in the dataset is an arbitrary stock at an arbitrary 5 day time window.
<p align="center">
  <img src="https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/data.jpg" width=1000>
</p>
<br>

## Tecnologies Used
    
* <strong>Python</strong>
* <strong>Pandas</strong>
* <strong>Numpy</strong>
* <strong>Matplotlib</strong>
* <strong>Seaborn</strong>
* <strong>Plotly</strong>
* <strong>Scikit Learn</strong>
* <strong>Principle Componnent Analysis</strong>
* <strong>Iterative Imputer</strong>
* <strong>Random Forest Regressor</strong>
* <strong>Multi-layer Perceptron Regressor</strong>
* <strong>Multi Output Regressor</strong>

## Exploratory Data Analysis
Exploratory Data Analysis  is performed to explore the structure of the data, identify categorical and continuos data feilds, missing values, and corelations amongst different data columns <br> 
<p>
  Corelation Heatmap between diffent features:
</p>
<img src="https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/heatmap.png" width=500>

## Feature Engineering
As observed in the corelation heatmap above, alot of features are strongly corelated to each other. This means that it is possibble to apply Dimentionality Reduction methods such as Principle Component Analysis. <br>
__Principal component analysis (PCA)__ is the process of computing the principal components and using them to perform a change of basis on the data, sometimes using only the first few principal components and ignoring the rest. <br>
The optimum number of principle components can be found by observing the variance for different sets of components. The set with variance closest to one is concidered as the one with optimum number of principle components.
<img src="https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/pca.png" width=400>
<br>
Here we can observe that the optimum number of components is 12 <br>
To simplify the problem, the intraday returns are aggregated as sum and standard deviation for both features (Ret_2 to Ret_120) and target labels (Ret_121 to Ret_180)
Standard deviation of the interday returns is also considered to see how much the returns vary.

## Modelling and Hyperparameter Tuning



