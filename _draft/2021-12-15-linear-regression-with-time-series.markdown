---
layout: post
title:  "Linear Regression With Time Series"
description: "Use two features unique to time series: lags and time steps."
categories: learning
read_minutes: 10
is_project_page: false
show_downloads: false
linux_compatible: false
---

# **Table of Contents**

1. Linear Regression With Time Series
2. Trend
3. Seasonality
4. Time Series as Features
5. Hybrid Models
6. Forecasting With Machine Learning

* * *

### 문단 복사 붙여넣기용
<p>　</p>

**Forecasting**: most common application of machine learning in the real world.

After finishing this course, you'll know how to:

  - engineer features to model the major time series components (trends, seasons, and cycles),
  - visualize time series with many kinds of time series plots,
  - create forecasting *hybrids* that combine the strengths of complementary models, and
  - adapt machine learning methods to a variety of forecasting tasks.

## **1. Linear Regression With Time Series**
> ### **Why do I come up with this project?**

**time dummy**: counts off time steps in the series from beginning to end. With time dummy model becomes:
```
target = weight * time + bias
```
**time dependence**:  if its values can be predicted from the time they occured. Time-step features let you model time dependence.

**Lag Features**
```
target = weight * lag + bias
```
each observation in a series is plotted against the previous observation.
**serial dependence**: when an observation can be predicted from previous observations. lag features let you model serial dependence.

Adapting machine learning algorithms to time series problems is largely about feature engineering with the time index and lags. we use linear regression for its simplicity, but these features will be useful whichever algorithm you choose for your forecasting task.

```python
# Time feature
df['Time'] = np.arange(len(tunnel.index))

# Lag feature using `shift` method
df['Lag_1'] = df['NumVehicles'].shift(1)
```

Linear regression model: Explainable: easy to interpret what contribution each feature makes to the predictions.

* * *

## **2. Trend**

represents a persistent, long-term change in the mean of the series.

any persistent and slow-moving change in a series could constitute a trend -- time series commonly have trends in their variation for instance.

```
# Quadradic trend regression
# 포물선 y = X^2 모양의 regression line
target = a * time ** 2 + b * time + c
```

**Moving Average**: use `rolling`to begin a windowed computation.

Time Dummy using 	`DeterministicProcess` in `statsmodel`: help us avoid some tricky failure cases that can arise with time series and linear regression.
`order`: `1` = linear, `2` = quadratic, `3` = cubic ...

(Deterministic process, is a technical term for a time series that is non-random or completely determined, like the `const` and `trend` series are. Features derived from the time index will generally be deterministic.)

`fit_intercept=False` in LinearRegression: DeterministicProcess에서 `const` feature로 절편을 집어넣었으니까 duplicated feature를 없앤다.

```python
# Out-of-sample Prediction
X = dp.out_of_sample(steps=30)
```

we can use trend models as a component in a "hybrid model" with algorithms unable to learn trends (like XGBoost and random forests).

To get a better fit to the somewhat complicated trend in Store Sales, we could try using an order 11 polynomial instead of 3.
However, An order 11 polynomial will include terms like t ** 11. Terms like these tend to diverge rapidly outside of the training period making out-of-sample forecasts very unreliable.

**Splines**: Multivariate Adaptive Regression Splines (MARS) algorithm in the `pyearth` library, Alternative of polynomial trend. lots of hyperparameters you may want to investigate.

you can use splines to isolate other patterns in a time series by detrending.

* * *

## **3. Seasonality**
regular, periodic change in the mean of the series. repetitions over a day, a week, or a year are common.

**seasonal plot**: segments of the time series plotted against some common period, which is a "season" you want to observe. 

**Seasonal indicators**: binary features that represent seasonal differences in the level of a time series. if you treat a seasonal period as a categorical feature and apply one-hot encoding.
>> ex) 월화수목금토일을 7개의 dummy로 만드는 것.

Seasonal indicator is best for a season with few observations, like a weekly season of daily observations.

**Fourier features**: pairs of sine and cosine curves, one pair for each potential frequency in the season starting with the longest.
Fourier pairs modeling annual seasonality would have frequencies: once per year, twice per year, three times per year, and so on.

linear regression algorithm will figure out the weights that will fit the seasonal component in the set of sine / cosine curves 

only needed eight features (four sine / cosine pairs) to get a good estimate of the annual seasonality.
 By modeling only the "main effect" of the seasonality, you'll usually need to add far fewer features to your training data, which means reduced computation time and less risk of overfitting.

**Periodogram**: strength of the frequencies in a time series.

`statsmodels` function about how a set of Fourier features could be derived.

create seasonal features using `DeterministicProcess`. To use two seasonal periods (weekly and annual), we'll need to instantiate one of them as an "additional term".

Using time series as inputs to a forecast lets us model the another component often found in series: *cycles.*

**detrending** or **deseasonalizing** series: removing from a series its trend or seasons.
```python
# Predicted value가 Seasonality를 잘 잡았다고도 해석 가능.
y_deseason = y - y_pred
```

What can we do with a deseasonalized model:
From a plot of the deseasonalized Average Sales, it appears these holidays could have some predictive power.

* * *

## **4. Time Series as Features**

Some time series properties can only be modeled as serially dependent properties,

trend and seasonality: learning time dependence.
**Cycles**: learn serial dependence.

Cyclic behavior: is characteristic of systems that can affect themselves or whose reactions persist over time.

ex) Economies, epidemics, animal populations, volcano eruptions, and similar natural phenomena often display cyclic behavior.

Cycles are not necessarily time dependent, as seasons are.

The (at least relative) independence from time means that cyclic behavior can be much more irregular than seasonality.

**Lagging**: needed to investigate possible serial dependence like cycles.

ex)forecast the future unemployment rate as a function of the unemployment rate in the prior two months.

**autocorrelation**: correlation a time series has with one of its lags (0.99 autocorrelation at lag 1 & 0.98 at lag 2 ...)

If lag 2 doesn't contain anything new, there would be no reason to include it if we already have lag 1.

**partial autocorrelation**: the amount of "new" correlation the lag contributes. Can help you choose which lag features to use.

**correlogram**: The correlogram is for lag features essentially what the periodogram is for Fourier features.

Keep in mind that autocorrelation and partial autocorrelation are measures of linear dependence.
>> it's best to look at a lag plot (or use some more general measure of dependence, like mutual information) when choosing lag features to look for any non-linear dependence which we might overlook with autocorrelation.

When using lag features, however, we are limited to forecasting time steps whose lagged values are available. 
ex) Using a lag 1 feature on Monday, we can't make a forecast for Wednesday because the lag 1 value needed is Tuesday which hasn't happened yet.

limitation of using only lags of the target series as features.: needs a time step to react to sudden changes.

Solution
**leading indicators**: time series that could provide an "early warning" for changes in flu cases.
ex) flu-related search terms as measured by Google Trends.

You could model such series with linear regression by just adding the appropriate features for each component. You can even combine models trained to learn the components separately.

To isolate any purely cyclic behavior, we'll start by deseasonalizing the series.
After deseasonlizing, we can then try to isolate cyclic behavior using a moving-average plot just like we did with trend.
 The idea is to choose a window long enough to smooth over short-term seasonality, but short enough to still preserve the cycles. [ex) 7-day MA]

"lookahead leakage" or "Look-Ahead Bias": using data that would not have been known or available during the period being analyzed.
>> research is necessary to determine what data was available at the time.

Winners of Kaggle forecasting competitions have often included moving averages and other rolling statistics in their feature sets. Such features seem to be especially useful when used with GBDT algorithms like XGBoost.

**GBDT**: Gradient Boost Decision Tree

To avoid lookahead leakage:
1. Result should be set at the right end of the window instead of the center = should use center=False (the default) in the rolling method. 
2. the target should be lagged a step.

[Pandas `Window` documentation] for more statistics you can compute.

`ewm` in place of rolling: "exponential weighted" windows
>> exponential decay is often a more realistic representation of how effects propagate over time.

* * *

## **5. Hybrid Models**

Linear regression excels at extrapolating trends, but can't learn interactions.
XGBoost excels at learning interactions, but can't extrapolate trends.

We could imagine learning the components of a time series as an iterative process

1. learn the trend and subtract it out from the series
2. learn the seasonality from the detrended residuals and subtract the seasons out
3. learn the cycles and subtract the cycles out
4. only the unpredictable error remains.

```python
# 1. Train and predict with first model
model_1.fit(X_train_1, y_train)
y_pred_1 = model_1.predict(X_train)

# 2. Train and predict with second model on residuals
model_2.fit(X_train_2, y_train - y_pred_1)
y_pred_2 = model_2.predict(X_train_2)

# 3. Add to get overall predictions
y_pred = y_pred_1 + y_pred_2
```

Usually use different feature sets (`X_train_1` and `X_train_2`) depending on what we want each model to learn.
If we use the first model to learn the trend, we generally wouldn't need a trend feature for the second model, for example.

Two ways a regression algorithm can make predictions:

1. Feature-transforming algorithms: Linear regression and neural nets
  - learn some mathematical function that takes features as an input and then combines and transforms them to produce an output that matches the target values in the training set. 
  - can **extrapolate** target values beyond the training set

2. Target-transforming algorithms: Decision trees(including Random forests + gradient boosted decision trees (like XGBoost)) and nearest neighbors
  - use the features to group the target values in the training set and make predictions by averaging values in a group; a set of feature just indicates which group to average. 
  - can't extrapolate trends. Predictions of target transformers will always be bound within the range of the training set.

Hybrid design:

1. use linear regression to extrapolate the trend
2. transform the target to remove the trend
3. apply XGBoost to the detrended residuals.

**Boosted** hybrids: To hybridize a neural net (a feature transformer), you could instead include the predictions of another model as a feature, which the neural net would then include as part of its own predictions.
 Named as boosted because the method of fitting to residuals is actually the same method the gradient boosting algorithm uses.

**Stacked** hybrids: the method of using predictions as features

> Train models for XBboost
 While the linear regression algorithm is capable of multi-output regression, the XGBoost algorithm is not.
 To predict multiple series at once with XGBoost, we'll instead convert these series from wide format, with one time series per column, to long format, with series indexed by categories along rows.

from (wide format)
|Industries	|Sales (multiple outputs)|
|Month		|BuildingMaterials	|FoodAndBeverage
|:------------------|:------------------|:--------|
|1992-01-01	|8964		|29589	|
|1992-02-01	|9023		|28570	|
|1992-03-01	|10608		|29682	|
|1992-04-01	|11630		|30228	|
|1992-05-01	|12327		|31677	|

```python
# The `stack` method converts column labels to row labels, pivoting from wide format to long
X = retail.stack()  # pivot dataset wide to long
display(X.head())
y = X.pop('Sales')  # grab target series
```

to (long format)
				
|Month		|Industries	|Sales	|
|:------------------|:------------------|:--------|
|1992-01-01	|BuildingMaterials	|8964	|
|		|FoodAndBeverage	|29589	|
|1992-02-01	|BuildingMaterials	|9023	|
|		|FoodAndBeverage	|28570	|
|1992-03-01	|BuildingMaterials	|10608	|

 So that XGBoost can learn to distinguish our two time series, we'll turn the row labels for `'Industries'` into a categorical feature with a label encoding.
 We'll also create a feature for annual seasonality by pulling the month numbers out of the time index.

```python
# Turn row labels into categorical feature columns with a label encoding
X = X.reset_index('Industries')
# Label encoding for 'Industries' feature
for colname in X.select_dtypes(["object", "category"]):
    X[colname], _ = X[colname].factorize()
```

 trend learned by XGBoost is only as good as the trend learned by the linear regression. = XGBoost wasn't able to compensate for the poorly fit trend.

```python
# Possible Model 1 and Model 2 for hybrid

# Model 1 (trend)
from pyearth import Earth
from sklearn.linear_model import ElasticNet, Lasso, Ridge

# Model 2
from sklearn.ensemble import ExtraTreesRegressor, RandomForestRegressor
from sklearn.neighbors import KNeighborsRegressor
from sklearn.neural_network import MLPRegressor
```
other algorithms you like in the scikit-learn [User Guide](https://scikit-learn.org/stable/supervised_learning.html).

* * *

## **6. Forecasting With Machine Learning**
 > create forecasts for any time in the future

**forecast origin**: time at which you are making a forecast. Practically, you might consider the forecast origin to be the last time for which you have training data for the time being predicted. Everything up to the origin can be used to create features.

**forecast horizon**: time for which you are making a forecast. We often describe a forecast by the number of time steps in its horizon: a "1-step" forecast or "5-step" forecast, say. The forecast horizon describes the target.

**lead time (or sometimes latency)**: time between the origin and the horizon. In practice, it may be necessary for a forecast to begin multiple steps ahead of the origin because of delays in data acquisition or processing.

 In order to forecast time series with ML algorithms, we need to transform the series into a dataframe we can use with those algorithms.

8-week horizon with a 1-week lead time.  = forecasting eight weeks of flu cases starting with the following week.

strategies for producing the multiple target steps required for a forecast.
1. **Multioutput model**
  - Linear regression and neural networks
  - simple and efficient
  - not possible for every algorithm(XGBoost)

2. **Direct strategy**
  - one model forecasts 1-step ahead, another 2-steps ahead ...
  - can help to have a different model make forecasts for each step.
  - training lots of models can be computationally expensive.

3. **Recursive strategy**
  - Train a single one-step model and use its forecasts to update the lag features for the next step.
  - only need to train one model
  - can be inaccurate for long horizons since errors will accumulate.

4. **DirRec strategy**
  - combination of the direct and recursive strategies
  - train a model for each step and use forecasts from previous steps as *new* lag features.
  - can capture serial dependence better than Direct since each model always has an up-to-date set of lag features,
  - can also suffer from error propagation like Recursive.


`MultiOutputRegressor(XGBRegressor())`: apply Direct strategy to XGBoost
`RegressorChain()`: apply DirRec stretegy
Recursive: code ourserlves.

* * *

Congratulations! You've completed Kaggle's *Time Series* course. If you haven't already, join our companion competition: [Store Sales - Time Series Forecasting](https://www.kaggle.com/c/29781) and apply the skills you've learned.

For inspiration, check out Kaggle's previous forecasting competitions. Studying winning competition solutions is a great way to upgrade your skills.

- [**Corporación Favorita**](https://www.kaggle.com/c/favorita-grocery-sales-forecasting): the competition *Store Sales* is derived from.
- [**Rossmann Store Sales**](https://www.kaggle.com/c/rossmann-store-sales)
- [**Wikipedia Web Traffic**](https://www.kaggle.com/c/web-traffic-time-series-forecasting/)
- [**Walmart Store Sales**](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)
- [**Walmart Sales in Stormy Weather**](https://www.kaggle.com/c/walmart-recruiting-sales-in-stormy-weather)
- [**M5 Forecasting - Accuracy**](https://www.kaggle.com/c/m5-forecasting-accuracy)

# References #

Here are some great resources you might like to consult for more on time series and forecasting. They all played a part in shaping this course:

- *Learnings from Kaggle's forecasting competitions*, an article by Casper Solheim Bojer and Jens Peder Meldgaard.
- *Forecasting: Principles and Practice*, a book by Rob J Hyndmann and George Athanasopoulos.
- *Practical Time Series Forecasting with R*, a book by Galit Shmueli and Kenneth C. Lichtendahl Jr.
- *Time Series Analysis and Its Applications*, a book by Robert H. Shumway and David S. Stoffer.
- *Machine learning strategies for time series forecasting*, an article by Gianluca Bontempi, Souhaib Ben Taieb, and Yann-Aël Le Borgne.
- *On the use of cross-validation for time series predictor evaluation*, an article by Christoph Bergmeir and José M. Benítez.


**The End**

* * *

[Pandas `Window` documentation]:
https://pandas.pydata.org/pandas-docs/stable/user_guide/window.html