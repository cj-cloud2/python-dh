# **Lab Sheet: NumPy Indexing & Logic**

**Target Audience:** Data Scientists (Beginner Python)
**Objective:** Learn how to filter data, extract specific subsets, and perform vectorized text/logic operations.

## **Topics Covered**

1. **Basic Slicing**: Extracting subarrays using `[start:stop:step]`.
2. **Boolean Masking**: Filtering data based on conditions (e.g., "All values > 5").
3. **`numpy.where`**: Conditional logic (IF-THEN for arrays).
4. **`numpy.char`**: Handling text data in arrays.
5. **`numpy.testing`**: Verifying your code results.

---

## **1. Basic Slicing (`[start:stop:step]`)**

### **Concept & Use**

Just like Python lists, you can "slice" NumPy arrays to grab specific chunks of data. The syntax is `[start_index : stop_index : step]`.

* **Start**: Inclusive (The index you begin at).
* **Stop**: Exclusive (The slice stops *before* this index).
* **Step**: How many items to skip (e.g., 2 means take every second item).

### **Sample Code**

```python
import numpy as np

# Create an array of 10 numbers (0 to 9)
data = np.arange(10)

# Slice from index 2 to 7
subset = data[2:7]

# Slice from index 0 to end, taking every 2nd number (Evens)
evens = data[::2]

# Reverse the array (Step = -1)
reversed_data = data[::-1]

print("Original:", data)
print("Subset (2:7):", subset)
print("Evens:", evens)
print("Reversed:", reversed_data)

```

### **Practice Code**

```python
# Task 1: Create an array 'my_arr' with numbers 10 to 29 using np.arange(10, 30)


# Task 2: Slice the first 5 elements (indices 0 to 5) and store in 'first_five'


# Task 3: Slice the last 5 elements (Using negative indexing like -5:)


# Task 4: Extract every 3rd number from the entire array


```

---

## **2. Boolean Masking (Advanced Indexing)**

### **Concept & Use**

This is one of the most powerful features for Data Science. Instead of asking for "Index 0 to 5", you ask for "All data where value > 50".
This works by creating a **Mask**: A True/False array that acts like a filter. Only "True" positions are kept.

### **Sample Code**

```python
import numpy as np

arr = np.array([10, 55, 20, 80, 30])

# 1. Create a Mask (Logic condition)
# This checks every number: Is it greater than 50?
mask = arr > 50
print("Mask:", mask) # [False, True, False, True, False]

# 2. Apply the Mask
# We use the mask inside the brackets []
high_values = arr[mask]

print("High Values:", high_values)

```

### **Practice Code**

```python
# Task 1: Create an array 'scores' with values [35, 88, 92, 45, 60, 12, 99]


# Task 2: Create a boolean mask called 'pass_mask' where scores are greater than or equal to 50


# Task 3: Use the mask to extract the passing scores into a new array called 'passed'


# Task 4: Print the 'passed' array


```

---

## **3. Conditional Selection (`numpy.where`)**

### **Concept & Use**

`numpy.where` is the vectorized version of an Excel "IF" statement or SQL "CASE WHEN".

* **Syntax**: `np.where(condition, value_if_true, value_if_false)`
It allows you to modify data based on a condition without writing a slow loop.

### **Sample Code**

```python
import numpy as np

salaries = np.array([40000, 55000, 30000, 80000])

# Logic: If salary < 50000, give a "Bonus", else "No Bonus"
status = np.where(salaries < 50000, "Bonus", "No Bonus")

print("Salaries:", salaries)
print("Status:", status)

```

### **Practice Code**

```python
# Task 1: Create an array 'temps' with temperatures [100, 30, 40, 120, 15]


# Task 2: Use np.where to create a 'sensor_status' array. 
# If temp > 90, it should say "Overheat", otherwise "Normal"


# Task 3: Print 'sensor_status'


```

---

## **4. String Operations (`numpy.char`)**

### **Concept & Use**

NumPy can handle text arrays, though it's less common than numbers. The `numpy.char` module provides fast string operations (like uppercase, replace, split) that apply to the entire array at once.

### **Sample Code**

```python
import numpy as np

# Create an array of names
names = np.array(["alice", "bob", "charlie","amber","anny"])

# Convert all to Uppercase
upper_names = np.char.upper(names)

# Check if they start with 'A'
starts_with_a = np.char.startswith(names, "a")

print("Uppercase:", upper_names)
print("Starts with 'a' mask:", starts_with_a)

```

### **Practice Code**

```python
# Task 1: Create an array 'files' with ["data.csv", "image.jpg", "backup.csv"]


# Task 2: Use np.char.endswith() to find which files end with ".csv"


# Task 3: Use np.char.replace() to change ".csv" to ".txt" in the 'files' array


```

---

## **5. Testing & Verification (`numpy.testing`)**

### **Concept & Use**

In scientific computing, floating-point math isn't always perfect (e.g., 0.1 + 0.2 is not exactly 0.3 in computers). `numpy.testing` provides tools to check if two arrays are "close enough" to be considered equal, which is essential for writing robust code.

### **Sample Code**

```python
import numpy as np

calculated = np.array([1.0000001, 2.0])
expected = np.array([1.0, 2.0])


# This would FAIL because they are not identical
# np.testing.assert_array_equal(calculated, expected) 



# This will PASS because they are very close  ($0.00001* (10^{-5})
np.testing.assert_allclose(calculated, expected, rtol=1e-5)
print("First test passed (Arrays are close enough)")


#Breaking Down the Parameters
#1. calculated and expectedcalculated: 
#The result your code produced.expected: The "Ground Truth" or known correct result you are comparing against.
#2. rtol=1e-5 (Relative Tolerance)This is the Relative Tolerance. 
#It handles the comparison based on the scale of the numbers.1e-5 is scientific notation for $0.00001$ ($10^{-5}$).
#It means: "The difference should not be more than 0.001% of the expected value.
#"Why use it? If you are comparing billions, a difference of 10 is tiny. 
#If you are comparing decimals like 0.0001, a difference of 10 is massive. rtol scales automatically.
#3. atol (Absolute Tolerance)While not in your specific snippet, it defaults to 0.It is a fixed number that defines the #maximum allowed difference regardless of size.
#It is useful when expected is zero, because rtol multiplied by zero is always zero.


```

### **Practice Code**

```python
# Task 1: Create two arrays: 'a' = [0.1 + 0.2] and 'b' = [0.3]


# Task 2: Print 'a' and 'b' (Notice Python might print 0.30000000000000004 for 'a')


# Task 3: Use np.testing.assert_allclose(a, b) to verify they are mathematically effectively equal
# (If it runs without error, it passed)


```