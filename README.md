# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
### Name : HASNA MUBARAK AZEEM
### Register Number : 212223240052
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv('gold.csv')

data.head()

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data['usd_am_diff'] = data['USD (AM)'] - data['USD (AM)'].shift(1)

result = seasonal_decompose(data['USD (AM)'], model='additive', period=12)
data['usd_am_sea_diff'] = result.resid

data['usd_am_log'] = np.log(data['USD (AM)'])
data['usd_am_log_diff'] = data['usd_am_log'] - data['usd_am_log'].shift(1)

result = seasonal_decompose(data['usd_am_log_diff'].dropna(), model='additive', period=12)
data['usd_am_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['USD (AM)'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('USD (AM) Price')

plt.subplot(6, 1, 2)
plt.plot(data['usd_am_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced USD (AM) Price')

plt.subplot(6, 1, 3)
plt.plot(data['usd_am_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally Adjusted USD (AM) Price')

plt.subplot(6, 1, 4)
plt.plot(data['usd_am_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(USD (AM) Price)')

plt.subplot(6, 1, 5)
plt.plot(data['usd_am_log_diff'], label='Log')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Diff(Log(USD (AM) Price))')

plt.subplot(6, 1, 6)
plt.plot(data['usd_am_log_seasonal_diff'], label='Log')
plt.legend(loc='best')
plt.title('Log Transformation, Regular Differencing, and Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('Diff(Diff(Log(USD (AM) Price)))')

plt.tight_layout()
plt.show()

data.plot(kind='line')
```

### OUTPUT:
### Original Data:

![original](https://github.com/user-attachments/assets/3c0dd874-3f0b-4912-9036-993c1e539bfd)

### REGULAR DIFFERENCING:

![Regular](https://github.com/user-attachments/assets/1ba2596c-141e-40a6-b4b8-db12874d9e54)

### SEASONAL ADJUSTMENT:

![seasonal](https://github.com/user-attachments/assets/fdc3e7b4-acc8-4bf0-aff4-8534a579e32d)

### LOG TRANSFORMATION:

![log](https://github.com/user-attachments/assets/4c8e5bf0-0c2b-420e-bfe8-d2de958d5953)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
