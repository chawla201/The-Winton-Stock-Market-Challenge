
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

## Technologies Used
    
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

## Model Building
After imputing missing values and executing Principle Component Analysis on the numerical data columns, the categorical data was transformed into dummy variable columns using Pandas' get_dummies() feature. <br>
The data was split into training (70%) and testing (30%) data. <br>
I tried two different models:
<ul>
  <li> <strong>Random Forest Regressor</strong>: For baseline model
  <li> <strong>Multi Layer Perceptron Regressor (MLPReggresor)</strong>: Since the data involved feature values of different ranges, I thought a Multi Layer Perceptron model will be resistent to those variations 
</ul>
Since the problem statement dictates us to predict multiple values, MultiOutputRegressor is used.
<h5 align="center">y_test (blue) vs. y_pred (orange) for first 500 data points in test data</h5>
<table>
  <tr><td><h5 align="center">MLP Regressor</h5></td><td><h5 align="center">Random Forest Regressor</h5></td></tr>
  <tr><td><img src='https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/mlp_intit1.png' width=500></td><td><img src='https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/rfr_init1.png' width=500></td></tr>
  <tr><td><img src='https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/mlp_intit2.png' width=500></td><td><img src='https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/rfr_init2.png' width=500></td></tr>
</table>
<br>
<h2>Hyperparameter Tuning</h2>
As seen in the graphs above, the prediction lined for Random Forest Regressors are mostly flat lines with a few sparse peaks. While on the contrary, Multi-level Perceptron Regressor shows way better results. Thus only Multi-level Perceptron Regressor underwent hyperparameter tuning.
<strong>Grid Search Cross Validation</strong> method is used to fine tune the regression model.
The best model obtained after hyper parameter tuning is: <br>
<img src="https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/best_estimator.jpg" width=600>

<h2>Model Evaluation</h2>
Mean Absolute Error (MAE) is used the performance metric for evaluating the regression model. MAE is easy to interpret and provides a clear view of the performance of the model.
<p align='center'>
  <img src="https://github.com/chawla201/The-Winton-Stock-Market-Challenge/blob/master/images/mae.png" width=400>
 </p>
 The Mean Absolute Error of the model = <strong>0.01366</strong>
 
