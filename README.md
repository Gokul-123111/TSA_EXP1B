# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
###  Date: 20.10.2026

#### NAME: GOKUL S
#### REG.NO.: 212224240044


### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv('/content/Indian_Climate_Dataset_2024_2025.csv')
data.head()

# many cities per date, so pick one city
data = data[data['City'] == 'Chennai']

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

temp = 'Temperature_Avg (°C)'

# 1. regular differencing
data['temp_diff'] = data[temp] - data[temp].shift(1)

# 2. seasonal adjustment (residual after removing trend + seasonality)
result = seasonal_decompose(data[temp], model='additive', period=30)
data['temp_sea_diff'] = result.resid

# 3. log transformation
data['temp_log'] = np.log(data[temp])

# 4. log + regular differencing
data['temp_log_diff'] = data['temp_log'] - data['temp_log'].shift(1)

# 5. log + regular diff + seasonal adjustment
result = seasonal_decompose(data['temp_log_diff'].dropna(), model='additive', period=30)
data['temp_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data[temp], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('Temperature (°C)')

plt.subplot(6, 1, 2)
plt.plot(data['temp_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Temperature')

plt.subplot(6, 1, 3)
plt.plot(data['temp_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally adjusted Temperature')

plt.subplot(6, 1, 4)
plt.plot(data['temp_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Temperature)')

plt.subplot(6, 1, 5)
plt.plot(data['temp_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(Temperature))')

plt.subplot(6, 1, 6)
plt.plot(data['temp_log_seasonal_diff'], label='Log Transformation, Regular Diff and Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(Temperature)))')

plt.tight_layout()
plt.show()

data[[temp, 'temp_diff', 'temp_log']].plot(kind='line')
plt.show()
```

### OUTPUT:

<img width="1575" height="260" alt="image" src="https://github.com/user-attachments/assets/999e29a0-6e96-4b0e-8009-8b7675a52f89" />

#### REGULAR DIFFERENCING:

<img width="1582" height="252" alt="image" src="https://github.com/user-attachments/assets/77ba9d3d-70fb-4141-81d3-aba99690bdda" />

#### SEASONAL ADJUSTMENT:

<img width="1577" height="262" alt="image" src="https://github.com/user-attachments/assets/4f3e963f-e107-47e9-8112-72008aea6844" />

#### LOG TRANSFORMATION:

<img width="1577" height="245" alt="image" src="https://github.com/user-attachments/assets/903fa914-442d-4a61-956d-d071fe86c0a2" />

####  Log Transformation and Regular Differencing:

<img width="1587" height="257" alt="image" src="https://github.com/user-attachments/assets/0906d4f9-0a86-46ca-81c1-5e97333c22a9" />

####  Log Transformation, Regular Differencing and Seasonal Differencing

<img width="1582" height="257" alt="image" src="https://github.com/user-attachments/assets/91e0ac9d-dcb7-4e01-b200-cbed558e9bcf" />

#### OVERALL VIEW

<img width="550" height="447" alt="image" src="https://github.com/user-attachments/assets/15364c1e-3d6f-4832-9ab3-dbeeaf992308" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
