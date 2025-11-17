# Ex.No: 1B      CONVERTING NON-STATIONARY SERIES INTO STATIONARY FORM

## Developed By : shalini venkatesulu

## Register Number: 212223220104

# Date: 17/11/2025

### AIM:

To convert the international airline passenger dataset into a stationary time series by applying differencing, seasonal modification, and logarithmic transformation.

### PROCEDURE:

1. Load essential Python libraries such as pandas and numpy.
2. Import the dataset using pandas.
3. If necessary, clean the data and then apply the following transformations:

   * Regular differencing
   * Seasonal adjustment
   * Logarithmic transformation
4. Visualize the dataset before and after each transformation step.
5. Summarize and interpret the changes observed.

### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

df = pd.read_csv("weatherHistory.csv")
df['Formatted Date'] = pd.to_datetime(df['Formatted Date'], utc=True)
df = df.set_index('Formatted Date')


daily = df.resample('D').mean(numeric_only=True)

daily['Temp_diff1'] = daily['Temperature (C)'].diff()

decomp1 = seasonal_decompose(daily['Temperature (C)'].dropna(), model='additive', period=365)
daily['Temp_season_adj'] = decomp1.resid

daily['Temp_log'] = np.log1p(daily['Temperature (C)'] - daily['Temperature (C)'].min())

daily['Temp_log_diff'] = daily['Temp_log'].diff()

decomp2 = seasonal_decompose(daily['Temp_log_diff'].dropna(), model='additive', period=365)
daily['Temp_log_season_adj'] = decomp2.resid


fig, axes = plt.subplots(3, 2, figsize=(15, 15))

axes[0, 0].plot(daily['Temperature (C)'], color='tab:blue')
axes[0, 0].set_title("Original Temperature Series")

axes[0, 1].plot(daily['Temp_diff1'], color='tab:orange')
axes[0, 1].set_title("First Difference")

axes[1, 0].plot(daily['Temp_season_adj'], color='tab:green')
axes[1, 0].set_title("Seasonal Component Removed")

axes[1, 1].plot(daily['Temp_log'], color='tab:red')
axes[1, 1].set_title("Log Transformation")

axes[2, 0].plot(daily['Temp_log_diff'], color='tab:purple')
axes[2, 0].set_title("Log Differenced")

axes[2, 1].plot(daily['Temp_log_season_adj'], color='tab:brown')
axes[2, 1].set_title("Log + Seasonal Differencing")

for ax in axes.flat:
    ax.set_xlabel("Date")
    ax.set_ylabel("Temperature")

plt.tight_layout()
plt.show()
```

### OUTPUT:

**After Regular Differencing:**

<img width="791" height="528" alt="image" src="https://github.com/user-attachments/assets/c332d7f9-62ad-436f-9ade-d231e8d8fa26" />

<img width="824" height="515" alt="image" src="https://github.com/user-attachments/assets/c9c0c3c9-9f1c-4515-b993-2de7f1a46230" />

<img width="801" height="512" alt="image" src="https://github.com/user-attachments/assets/f3fa23b9-5267-4802-8e56-5e222f813b88" />


**After Seasonal Adjustment:**

<img width="785" height="499" alt="image" src="https://github.com/user-attachments/assets/9030ad02-5f7a-4cc1-9f8c-3b28e858396e" />




**After Log Transformation:**
<img width="830" height="509" alt="image" src="https://github.com/user-attachments/assets/beb0d280-7cef-4104-928a-4369d6083d8a" />


### RESULT:
The non-stationary airline passenger dataset was successfully transformed into stationary form using differencing, seasonal adjustment, and logarithmic conversion techniques.
The non-stationary airline passenger dataset was successfully transformed into stationary form using differencing, seasonal adjustment, and logarithmic conversion techniques.



