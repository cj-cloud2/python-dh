# **Lab Sheet: NumPy Mathematical & Statistical Functions**

**Target Audience:** Data Scientists (Beginner Python)
**Objective:** Master the core mathematical and statistical engines within NumPy.

## **Topics Covered**

1. **Mathematical Functions (Ufuncs)**: Standard constants (, ) and vectorized operations.
2. **`numpy.linalg`**: Linear Algebra essentials (Matrix multiplication, Inverses).
3. **`numpy.fft`**: Fast Fourier Transforms for signal analysis.
4. **`numpy.random`**: generating synthetic data and distributions.

---

## **1. Mathematical Constants and Functions**

### **Concept & Use**

While Python has a built-in `math` library, NumPy provides **Universal Functions (ufuncs)**. These are faster and "vectorized," meaning they can operate on an entire array of numbers at once without needing a loop. This is essential for applying mathematical transformations (like Logarithms or Exponentials) to large datasets.

### **Sample Code**

```python
import numpy as np

# 1. Constants
print(f"Pi: {np.pi}")
print(f"Euler's number (e): {np.e}")

# 2. Vectorized Math
angles = np.array([0, np.pi/2, np.pi]) # 0, 90, 180 degrees
sin_values = np.sin(angles) # Calculates sine for ALL values at once

print(f"Angles: {angles}")
print(f"Sine values: {sin_values}")

```

### **Practice Code**

```python
# Task 1: Create an array 'arr' containing numbers [1, 4, 9, 16, 25]


# Task 2: Use np.sqrt() to find the square root of 'arr' and print the result


# Task 3: Use np.exp() to calculate the exponential (e^x) of 'arr' and print it


```

---

## **2. Linear Algebra (`numpy.linalg`)**

### **Concept & Use**

The `numpy.linalg` module is the engine behind many Machine Learning algorithms. It handles Matrix operations. The most common operation you will use is the **Dot Product** (Matrix Multiplication), which combines rows and columns to calculate weighted sums.

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
# Task 1: Create a 2x2 Identity Matrix 'I' using np.eye(2) (Look up np.eye if needed, or define it manually)


# Task 2: Calculate the Dot Product of Matrix 'A' (from sample code) and your Identity Matrix 'I'
# Note: The result should be identical to Matrix A


# Task 3 (Optional): Find the Determinant of Matrix A using np.linalg.det(A)


```

---

## **3. Fast Fourier Transforms (`numpy.fft`)**

### **Concept & Use**

The **Fourier Transform** decomposes a signal (like sound or time-series data) into the frequencies that make it up. `numpy.fft` is used to convert data from the "Time Domain" (what happened when) to the "Frequency Domain" (how fast things change). This is widely used in feature extraction for time-series analysis.

### **Sample Code**

```python
import numpy as np

# Create a simple signal: [1, 0, 1, 0]
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

## **4. Random Number Generation (`numpy.random`)**

### **Concept & Use**

Data Science often requires "synthetic" data for testing models, initializing neural network weights, or splitting data into Training/Testing sets. `numpy.random` generates random numbers based on statistical distributions (like the Bell Curve/Normal distribution).

### **Sample Code**

```python
import numpy as np

# Set seed for reproducibility (so we get the same random numbers every time)
np.random.seed(42)

# Generate 3 random integers between 0 and 10
rand_ints = np.random.randint(0, 10, size=3)

# Generate 3 numbers from a Standard Normal Distribution (Bell curve, mean=0, std=1)
rand_normal = np.random.randn(3)

print("Random Integers:", rand_ints)
print("Normal Distribution Sample:", rand_normal)

```

### **Practice Code**

```python
# Task 1: Generate an array of 5 random floats between 0 and 1 using np.random.rand()


# Task 2: Simulate a coin toss. Generate 10 random integers that are either 0 or 1.


# Task 3: Generate a 2x2 matrix of random numbers drawn from a Normal Distribution


```