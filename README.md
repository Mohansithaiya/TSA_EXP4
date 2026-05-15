# Ex.No:04   FIT ARMA MODEL FOR TIME SERIES
# Date: 13/05/2026



### AIM:
To implement ARMA model in python.
### ALGORITHM:
1. Import necessary libraries.
2. Set up matplotlib settings for figure size.
3. Define an ARMA(1,1) process with coefficients ar1 and ma1, and generate a sample of 1000

data points using the ArmaProcess class. Plot the generated time series and set the title and x-
axis limits.

4. Display the autocorrelation and partial autocorrelation plots for the ARMA(1,1) process using
plot_acf and plot_pacf.
5. Define an ARMA(2,2) process with coefficients ar2 and ma2, and generate a sample of 10000

data points using the ArmaProcess class. Plot the generated time series and set the title and x-
axis limits.

6. Display the autocorrelation and partial autocorrelation plots for the ARMA(2,2) process using
plot_acf and plot_pacf.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.arima_process import ArmaProcess
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
import warnings

# Ignore warnings
warnings.filterwarnings('ignore')

# Load dataset
data = pd.read_excel("/content/Hyderabad-AirQ.xlsx")

# Remove spaces from column names
data.columns = data.columns.str.strip()

# Display column names
print("Columns in Dataset:")
print(data.columns)

# Convert Date column
data['Date'] = pd.to_datetime(data['Date'])

# Use PM2.5 column
pm_data = data['PM2.5'].dropna()

# Figure size
plt.rcParams['figure.figsize'] = [10, 7]

# ---------------- ARMA(1,1) ----------------

ar1 = np.array([1, -0.5])
ma1 = np.array([1, 0.5])

arma1 = ArmaProcess(ar1, ma1).generate_sample(
    nsample=len(pm_data)
)

# Plot ARMA(1,1)
plt.figure()
plt.plot(arma1)

plt.title("Simulated ARMA(1,1) Process")
plt.xlabel("Time")
plt.ylabel("PM2.5 Values")

plt.xlim([0, 200])
plt.grid()
plt.show()

# ACF and PACF
plt.figure()

plt.subplot(2,1,1)
plot_acf(arma1, lags=20, ax=plt.gca())
plt.title("ACF of ARMA(1,1)")

plt.subplot(2,1,2)
plot_pacf(arma1, lags=20, ax=plt.gca())
plt.title("PACF of ARMA(1,1)")

plt.tight_layout()
plt.show()

# ---------------- ARMA(2,2) ----------------

ar2 = np.array([1, -0.33, 0.5])
ma2 = np.array([1, 0.9, 0.3])

arma2 = ArmaProcess(ar2, ma2).generate_sample(
    nsample=len(pm_data)
)

# Plot ARMA(2,2)
plt.figure()
plt.plot(arma2)

plt.title("Simulated ARMA(2,2) Process")
plt.xlabel("Time")
plt.ylabel("PM2.5 Values")

plt.xlim([0, 200])
plt.grid()
plt.show()

# ACF and PACF
plt.figure()

plt.subplot(2,1,1)
plot_acf(arma2, lags=20, ax=plt.gca())
plt.title("ACF of ARMA(2,2)")

plt.subplot(2,1,2)
plot_pacf(arma2, lags=20, ax=plt.gca())
plt.title("PACF of ARMA(2,2)")

plt.tight_layout()
plt.show()
```

OUTPUT:
SIMULATED ARMA(1,1) PROCESS:
<img width="857" height="624" alt="image" src="https://github.com/user-attachments/assets/1a546f1e-af85-42de-91f9-c91f536858ba" />

Partial Autocorrelation

<img width="990" height="690" alt="image" src="https://github.com/user-attachments/assets/141b89c1-1565-48a3-9ab9-f6ce8ba7351f" />

Autocorrelation

<img width="990" height="690" alt="image" src="https://github.com/user-attachments/assets/4cf90c99-ba27-4b11-a3d3-8d0f250b877d" />



SIMULATED ARMA(2,2) PROCESS:


<img width="857" height="624" alt="image" src="https://github.com/user-attachments/assets/b4e5194c-e72f-443a-838b-86935df6a4a2" />

Partial Autocorrelation

<img width="990" height="690" alt="image" src="https://github.com/user-attachments/assets/e9554a20-e56d-4e9f-bdbf-12209b25057d" />



Autocorrelation


<img width="990" height="690" alt="image" src="https://github.com/user-attachments/assets/5e8bb207-11ee-4953-a0f9-9bf494bc3283" />

RESULT:
Thus, a python program is created to fir ARMA Model successfully.
