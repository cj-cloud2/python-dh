# **Lab Sheet: NumPy for Data Science - Mathematics & Statistics**

**Target Audience:** Data Scientists (Beginner Python)
**Objective:** Master the core mathematical, statistical, and installation basics of NumPy.

## **Topics Covered**

1. **Installation**: Setting up NumPy.
2. **Mathematical Functions (`numpy.math`)**: Constants and vectorized operations.
3. **Linear Algebra (`numpy.linalg`)**: Matrix multiplication and essential operations.
4. **Fast Fourier Transforms (`numpy.fft`)**: Frequency analysis.
5. **Random Number Generation (`numpy.random`)**: Creating synthetic data.

---

## **1. Installation**

### **Concept & Use**

Before using NumPy, it must be installed in your Python environment. We use `pip`, the standard package installer for Python. In a Jupyter Notebook, we can run terminal commands by placing a `!` symbol before the command.

### **Sample Code**

```python
# Installing numpy using pip
# Note: The '!' tells Jupyter to run this as a terminal command
!pip install numpy

```

### **Practice Code**

```python
# Task: Verify the installation by importing numpy and checking its version
# 1. Import numpy as np


# 2. Print the version string (stored in np.__version__)


```

---

## **2. Mathematical Constants and Functions (`numpy.math`)**

### **Concept & Use**

NumPy is designed for "Vectorization." Unlike standard Python math which calculates one number at a time, NumPy functions can apply a mathematical operation (like Square Root, Sine, or Log) to an entire array of data simultaneously. This is crucial for performance when working with large datasets.

### **Sample Code**

```python
import numpy as np

# 1. Constants
print(f"Pi: {np.pi}")
print(f"Euler's number (e): {np.e}")

# 2. Vectorized Math
# Create an array of angles: 0, 90, 180 degrees
angles = np.array([0, np.pi/2, np.pi]) 

# Calculate Sine for ALL values at once
sin_values = np.sin(angles) 

print(f"Angles: {angles}")
print(f"Sine values: {sin_values}")

```

### **Practice Code**

```python
# Task 1: Create an array 'arr' containing numbers [1, 4, 9, 16, 25]


# Task 2: Use np.sqrt() to find the square root of 'arr' and print the result


# Task 3: Use np.log() to find the natural logarithm of 'arr'


```

---

## **3. Linear Algebra (`numpy.linalg`)**

### **Concept & Use**

The `numpy.linalg` module is the engine behind many Machine Learning algorithms (like Linear Regression and PCA). It handles matrix operations. The most critical operation to understand is the **Dot Product** (Matrix Multiplication), which calculates the weighted sum of rows and columns.

### **Sample Code**

```python
import numpy as np

# Create two 2x2 matrices
A = np.array([[1, 2],
              [3, 4]])
B = np.array([[5, 6],
              [7, 8]])

# Matrix Multiplication (Dot Product)
# Row 1 of A * Col 1 of B: (1*5) + (2*7) = 19
dot_product = np.dot(A, B)

print("Matrix A:\n", A)
print("Dot Product of A and B:\n", dot_product)

```

### **Practice Code**

```python
# Task 1: Create a 2x2 Identity Matrix 'I' using np.eye(2) 
# (An identity matrix has 1s on the diagonal and 0s elsewhere)


# Task 2: Calculate the Dot Product of Matrix 'A' (from sample code) and 'I'
# Note: The result should be identical to Matrix A


# Task 3 (Optional): Find the Inverse of Matrix A using np.linalg.inv(A)


```

---

## **4. Fast Fourier Transforms (`numpy.fft`)**

### **Concept & Use**

The **Fourier Transform** is used to decompose a signal (like sound, stock prices, or time-series sensor data) into the frequencies that compose it. `numpy.fft` converts data from the "Time Domain" (x-axis is time) to the "Frequency Domain" (x-axis is frequency). This is essential for signal processing and feature extraction.

### **Sample Code**

```python
import numpy as np

# Create a simple signal: [1, 0, 1, 0] repeating
signal = np.array([1.0, 0.0, 1.0, 0.0])

# Compute the FFT (Frequency spectrum)
fft_spectrum = np.fft.fft(signal)

print("Original Signal:", signal)
print("Frequency Spectrum (Complex Numbers):", fft_spectrum)

```

### **Practice Code**

```python
# Task 1: Create an array 'wave' with values [0, 1, 0, -1]


# Task 2: Compute the FFT of 'wave' using np.fft.fft() and store it in 'wave_fft'


# Task 3: Print the 'wave_fft' results


```

---

## **5. Random Number Generation (`numpy.random`)**

### **Concept & Use**

Data Science often requires "synthetic" data for testing models, initializing neural network weights, or splitting data into Training/Testing sets. `numpy.random` generates random numbers based on statistical distributions. The most common is the **Normal (Gaussian) Distribution**, also known as the Bell Curve.

### **Sample Code**

```python
import numpy as np

# Set seed for reproducibility (so we get the same random numbers every time)
np.random.seed(42)

# Generate 3 random integers between 0 and 10
rand_ints = np.random.randint(0, 10, size=3)

# Generate 3 numbers from a Standard Normal Distribution (Mean=0, Std Dev=1)
rand_normal = np.random.randn(3)

print("Random Integers:", rand_ints)
print("Normal Distribution Sample:", rand_normal)

```

### **Practice Code**

```python
# Task 1: Generate an array of 5 random floats between 0 and 1 using np.random.rand()


# Task 2: Simulate a coin toss. Generate 10 random integers that are either 0 or 1.


# Task 3: Generate a 3x3 matrix of random numbers drawn from a Normal Distribution


```