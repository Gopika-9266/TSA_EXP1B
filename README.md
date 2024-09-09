### Name: Gopika R
### Register No: 212222240031
### Date: 

# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:

To perform regular differencing,seasonal adjustment and log transformation on tesla stock prediction

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

#reading the dataset
train = pd.read_csv('tsla_2014_2023 (1).csv')

#preprocessing
train.timestamp = pd.to_datetime(train["date"])
train.index = train.timestamp
train.drop('date',axis = 1, inplace = True)

#looking at the first few rows
train.head()
train['open'].plot()

from statsmodels.tsa.stattools import adfuller
def adf_test(timeseries):
    #Perform Dickey-Fuller test:
    print ('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic','p-value','#Lags Used','Number of Observations Used'])
    for key,value in dftest[4].items():
       dfoutput['Critical Value (%s)'%key] = value
    print (dfoutput)

adf_test(train['open'])

train['open_diff'] = train['open'] - train['open'].shift(1)
train['open'].dropna().plot()

# Seasonal Differencing
n=7
train['open_diff'] = train['open'] - train['open'].shift(n)
train['open_diff'].dropna().plot()

# Transformation
train['open_log'] = np.log(train['open'])
train['open_log_diff'] = train['open_log'] - train['open_log'].shift(1)
train['open_log_diff'].dropna().plot()


# Combined Graph
# Seasonal Differencing
n=7
train['open_diff'] = train['open'] - train['open'].shift(n)
train['open_diff'].dropna().plot()

# Transformation
train['open_log'] = np.log(train['open'])
train['open_log_diff'] = train['open_log'] - train['open_log'].shift(1)
train['open_log_diff'].dropna().plot()

train['open_diff'] = train['open'] - train['open'].shift(1)
train['open'].dropna().plot()
```


### OUTPUT:

![exp1b-img1](https://github.com/user-attachments/assets/c3ba00ae-2245-4f8d-a744-83cb531d90d0)
![exp1b-img2](https://github.com/user-attachments/assets/ef967ba1-aba5-4478-ab0b-0a842cc9d698)


REGULAR DIFFERENCING:

![Screenshot 2024-09-09 111331](https://github.com/user-attachments/assets/1e243fb1-2706-4354-9924-9cff1dde0758)

SEASONAL ADJUSTMENT:

![exp1b-img3](https://github.com/user-attachments/assets/2d9c86d8-9fab-46fc-8fe1-68bd8fa105f2)


LOG TRANSFORMATION:

![exp1b-img4](https://github.com/user-attachments/assets/9d9545b4-d504-4f31-b31f-b4c92686317d)

COMBINED GRAPH:
![exp1b-img5](https://github.com/user-attachments/assets/18cf011b-ece9-4eec-abf4-bad00cfd2dd5)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on tesla stock prediction.
