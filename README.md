# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date: 02-11-2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

## Dataset Used : Housing Dataset

## Software Used : Jupyter Notebook

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_csv("Bengaluru_House_Data.csv")

data['total_sqft'] = pd.to_numeric(data['total_sqft'], errors='coerce')
data['price'] = pd.to_numeric(data['price'], errors='coerce')

data = data.dropna(subset=['total_sqft', 'price'])

data = data[(data['total_sqft'] > 0) & (data['total_sqft'] <= 5000)]

data['area_group'] = (data['total_sqft'] // 500) * 500

grouped = data.groupby('area_group')['price'].mean().reset_index()

years = grouped['area_group'].values
prices = grouped['price'].values

X = years - np.mean(years)

n = len(X)

x2 = X ** 2
xy = X * prices

b = (n * np.sum(xy) - np.sum(X) * np.sum(prices)) / (n * np.sum(x2) - np.sum(X) ** 2)

a = (np.sum(prices) - b * np.sum(X)) / n

linear_trend = a + b * X

print("Linear Trend Equation:")
print("y =", round(a, 2), "+", round(b, 4), "x")

plt.figure(figsize=(10, 5))

plt.plot(years, prices, marker='o', label='Original Data')
plt.plot(years, linear_trend, color='red', linestyle='--', label='Linear Trend')

plt.title('Linear Trend Estimation')
plt.xlabel('Area (Square Feet)')
plt.ylabel('Average House Price (Lakhs)')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

```

B- POLYNOMIAL TREND ESTIMATION
```

X = years - np.mean(years)

n = len(X)

A = np.column_stack((np.ones(n), X, X**2))

B = prices

solution = np.linalg.lstsq(A, B, rcond=None)[0]

a_poly, b_poly, c_poly = solution

poly_trend = a_poly + b_poly * X + c_poly * X**2

print("Polynomial Trend Equation:")
print("y =", round(a_poly, 2), "+", round(b_poly, 4), "x +", round(c_poly, 6), "x²")

plt.figure(figsize=(10, 5))

plt.plot(years, prices, marker='o', label='Original Data')
plt.plot(years, poly_trend, color='red', linestyle='--', label='Polynomial Trend')

plt.title('Polynomial Trend Estimation')
plt.xlabel('Area (Square Feet)')
plt.ylabel('Average House Price (Lakhs)')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="731" height="337" alt="image" src="https://github.com/user-attachments/assets/87d05bd2-4f80-44b8-932e-b2e61bda2ef8" />


B- POLYNOMIAL TREND ESTIMATION
<img width="745" height="335" alt="image" src="https://github.com/user-attachments/assets/717ae3f6-1796-4c83-a4e2-1948632298c5" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
