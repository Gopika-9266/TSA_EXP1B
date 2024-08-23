### Name: Gopika R
### Register No: 212222240031
### Date: 

# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:

To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

### ALGORITHM:

1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("AirPassengers.csv")
train.timestamp = pd.to_datetime(train.Month, format = '%Y-%m')
train.drop('Month', axis=1, inplace = True)
train.head()
train['#Passengers'].plot()

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)
adf_test(train['#Passengers'])

train['#Passengers_diff'] = train['#Passengers'] - train['#Passengers'].shift(1)
train['#Passengers_diff'].dropna().plot()
# Seasonal Differencing
n=7
train['#Passengers_diff'] = train['#Passengers'] - train['#Passengers'].shift(n)
train['#Passengers_diff'].dropna().plot()
# Transformation
train['#Passengers_log'] = np.log(train['#Passengers'])
train['#Passengers_log_diff'] = train['#Passengers_log'] - train['#Passengers_log'].shift(1)
train['#Passengers_log_diff'].dropna().plot()
```


### OUTPUT:

![exp1b-img1](https://github.com/user-attachments/assets/42c81afe-cf76-464c-8a27-2da05cc0f916)

![exp1b-img2](https://github.com/user-attachments/assets/e412e94e-8430-437d-8d69-a359a56ac6f1)


REGULAR DIFFERENCING:
![exp1b-img3](https://github.com/user-attachments/assets/d0a1290c-acfd-4c98-8d1c-03cbdb8c997a)


SEASONAL ADJUSTMENT:
![exp1b-img4](https://github.com/user-attachments/assets/fc6af112-68f6-4d1d-909a-d596208b4b9d)


LOG TRANSFORMATION:
![exp1b-img5](https://github.com/user-attachments/assets/86270cdf-e9e9-482d-ab99-d3699785012d)

Combined Graph:
![exp1b-img6](https://github.com/user-attachments/assets/cde9a884-42f5-404e-ad90-a270b3280a53)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
