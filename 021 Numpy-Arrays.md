# **Lab Sheet: NumPy Array Creation & Manipulation**

**Target Audience:** Data Scientists (Beginner Python)
**Objective:** Learn how to create, reshape, join, and split data structures using NumPy.

## **Topics Covered**

1. **`numpy.array`**: Creating arrays from existing data (Lists/Tuples).
2. **`numpy.shape` & `reshape**`: Inspecting dimensions and restructuring data.
3. **`numpy.concatenate`**: Joining multiple arrays together.
4. **`numpy.split`**: Dividing larger arrays into smaller chunks.

---

## **1. Creating Arrays (`numpy.array`)**

### **Concept & Use**

The `ndarray` (N-dimensional array) is the core object in NumPy. Unlike Python lists, NumPy arrays must contain data of the **same type** (usually numbers). This uniformity allows NumPy to store data compactly and perform calculations much faster. You will use this to convert raw data lists into a format ready for analysis.

### **Sample Code**

```python
import numpy as np

# 1. Creating a 1D Array (Vector) from a list
data_list = [10, 20, 30, 40]
arr_1d = np.array(data_list)

# 2. Creating a 2D Array (Matrix) from a list of lists
matrix_list = [[1, 2], [3, 4], [5, 6]]
arr_2d = np.array(matrix_list)

print("1D Array:", arr_1d)
print("2D Array:\n", arr_2d)

```

### **Practice Code**

```python
# Task 1: Create a python list called 'prices' with values [10.5, 20.0, 5.5]


# Task 2: Convert 'prices' into a NumPy array called 'np_prices' using np.array()


# Task 3: Print 'np_prices'


```

---

## **2. Shape & Reshape (`numpy.shape`, `reshape`)**

### **Concept & Use**

Data often comes in the wrong format (e.g., a single long list of pixels that actually represents a 2D image).

* **`.shape`**: An attribute (not a function) that tells you the dimensions (Rows, Columns).
* **`.reshape()`**: A function that changes the structure of data without changing the data itself.

### **Sample Code**

```python
import numpy as np

# Create a 1D array with 12 numbers (0 to 11)
arr = np.arange(12) 
print(f"Original: {arr}")
print(f"Original Shape: {arr.shape}")

# Reshape into a Matrix with 3 Rows and 4 Columns
# Note: 3 * 4 must equal the total elements (12)
reshaped_arr = arr.reshape(3, 4)

print("\nReshaped (3x4):\n", reshaped_arr)
print(f"New Shape: {reshaped_arr.shape}")

```

### **Practice Code**

```python
# Task 1: Create an array 'my_data' containing numbers 0 to 9 using np.arange(10)


# Task 2: Print the shape of 'my_data' (It should be (10,))


# Task 3: Reshape 'my_data' into a 2D array with 2 Rows and 5 Columns. Store it in 'my_matrix'.


# Task 4: Print 'my_matrix'


```

---

## **3. Joining Arrays (`numpy.concatenate`)**

### **Concept & Use**

In Data Science, you often need to merge datasets (e.g., adding new rows of data to an existing dataset).

* **`concatenate`**: Joins arrays along an existing axis.
* **`stack` (or `vstack`/`hstack`)**: Often used to stack arrays vertically (adding rows) or horizontally (adding columns).

### **Sample Code**

```python
import numpy as np

arr_a = np.array([1, 2, 3])
arr_b = np.array([4, 5, 6])

# 1. Concatenating 1D arrays (Appending to the end)
combined = np.concatenate((arr_a, arr_b))
print("Concatenated:", combined)

# 2. Vertical Stack (Sticking them together like rows in a table)
# This creates a 2D array
stacked = np.vstack((arr_a, arr_b))
print("\nVertical Stack:\n", stacked)

```

### **Practice Code**

```python
# Task 1: Create two arrays: 'x' = [10, 20] and 'y' = [30, 40]


# Task 2: Use np.concatenate() to join them into one long array [10, 20, 30, 40]


# Task 3: Use np.vstack() to stack them into a 2x2 matrix


# Task 4: Print both results


```

---

## **4. Splitting Arrays (`numpy.split`)**

### **Concept & Use**

The opposite of joining. You might use this to separate data into "Training" and "Testing" sets, or to break a large image into smaller patches. `numpy.array_split` is a safer version that handles uneven splits, but `numpy.split` is the standard for equal division.

### **Sample Code**

```python
import numpy as np

# Create an array with 10 numbers
data = np.arange(10)

# Split into 2 equal sub-arrays
# Returns a LIST of arrays
chunks = np.split(data, 2) 

print("Original:", data)
print("First Half:", chunks[0])
print("Second Half:", chunks[1])

```

### **Practice Code**

```python
# Task 1: Create an array 'big_array' with numbers 0 to 11 using np.arange(12)


# Task 2: Split 'big_array' into 3 equal parts using np.split(). Store the result in 'parts'.


# Task 3: Print the first part (parts[0]) and the last part (parts[2])


```