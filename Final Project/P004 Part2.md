## Lab 2: The Engine (NumPy High-Performance Computing)

In the previous lab, you used standard Python loops to process data row-by-row. That works for small files, but in Data Engineering, we often handle millions of rows. Loops are too slow for that.

In this lab, you will upgrade your pipeline using NumPy. You will convert your data into high-performance arrays and perform "Vectorized Operations"—math that happens on the entire dataset instantly, without loops.

### Detailed Requirements for Lab 2

1. **Array Conversion:** Transform standard Python lists of ridership and revenue into NumPy arrays.
2. **Data Type Enforcement:** Ensure numerical precision by explicitly setting data types (e.g., `float64` for revenue, `int32` for counts).
3. **Handling Anomalies:** Identify invalid data points (like 0 riders with high revenue) using boolean masks and replace them with the statistical mean (Imputation).
4. **Vectorized Calculation:** Apply a system-wide "Peak Hour Surcharge" of 15% to all revenue figures simultaneously.
5. **Statistical Profiling:** Calculate the Standard Deviation of ridership to identify volatile stations.

---

### Step 1: Setup & Data Simulation

Since we are focusing on NumPy, we will simulate the "Cleaned Output" from Lab 1 so we have numerical lists ready to go.

**Step Description:**
Import the NumPy library and create raw lists representing the columns extracted from our CSV file.

**Logic & Planning:**

```python
# Import the numpy library and give it the alias 'np'.
# Create a python list containing passenger counts (integers and zeros).
# Create a python list containing revenue figures (floats).

```

**Solution:**

```python
# Import the numpy library and assign it the standard alias 'np'
import numpy as np

# Define a standard python list representing passenger counts (0 represents missing data)
riders_list = [45, 120, 38, 310, 0, 55, 22, 150, 0, 280]

# Define a standard python list representing revenue associated with those riders
revenue_list = [112.50, 360.00, 115.00, 930.00, 450.00, 137.50, 66.00, 450.00, 100.00, 840.00]

```

---

### Step 2: Creating NumPy Arrays

Python lists are flexible but slow. NumPy arrays are rigid (fixed type) but incredibly fast.

**Step Description:**
Convert the Python lists into NumPy arrays. We will cast the ridership data to `float` temporarily to handle missing values (NaNs) later.

**Logic & Planning:**

```python
# Convert the riders_list into a numpy array with data type float.
# Convert the revenue_list into a numpy array with data type float.
# Print the type of the new object to confirm it is a numpy array.

```

**Solution:**

```python
# Use np.array to convert the list to an array and set dtype to float for flexibility
riders_array = np.array(riders_list, dtype=float)

# Use np.array to convert the revenue list to a numpy array of floats
revenue_array = np.array(revenue_list, dtype=float)

# Use the type function to verify that the object is now a numpy.ndarray
print(f"Object Type: {type(riders_array)}")

```

---

### Step 3: Handling Anomalies (Imputation)

In our data, a `0` in ridership might actually mean "Missing Sensor Data," especially if there is associated revenue. We need to fix this.

**Step Description:**
Replace all `0` values in the `riders_array` with `NaN` (Not a Number), calculate the average of the valid data, and then fill the holes with that average.

**Logic & Planning:**

```python
# Create a mask (boolean check) where riders_array equals 0.
# Use the mask to replace all 0s in the array with np.nan.
# Calculate the mean (average) of the array ignoring the NaNs.
# Create a mask identifying where the NaNs are located.
# Fill the NaNs with the calculated mean value.
# Print the cleaned array.

```

**Solution:**

```python
# Use boolean indexing to set values to np.nan where the array is 0
riders_array[riders_array == 0] = np.nan

# Use np.nanmean to calculate the average while ignoring NaN values
mean_ridership = np.nanmean(riders_array)

# Use np.isnan to find indices where the value is NaN
nan_mask = np.isnan(riders_array)

# Assign the calculated mean to the indices identified by the mask
riders_array[nan_mask] = mean_ridership

# Use print to display the array with the imputed values
print(f"Cleaned Ridership: {riders_array}")

```

---

### Step 4: Vectorized Calculations (Broadcasting)

This is the power of NumPy. We will apply a math operation to the *entire* array at once. Imagine a new "15% Infrastructure Tax" is applied to all fares.

**Step Description:**
Multiply the entire `revenue_array` by 1.15 to apply the tax. This replaces the slow `for` loop from Lab 1.

**Logic & Planning:**

```python
# Multiply the entire revenue_array by 1.15 (broadcasting).
# Store the result in a new variable called adjusted_revenue.
# Print the first 5 elements to check the result.

```

**Solution:**

```python
# Multiply every element in revenue_array by 1.15 simultaneously
adjusted_revenue = revenue_array * 1.15

# Use array slicing [:5] to print only the first 5 elements
print(f"Adjusted Revenue: {adjusted_revenue[:5]}")

```

---

### Step 5: Statistical Filtering

We need to find "High Performance" stations. We will filter for stations where ridership is significantly above the mean.

**Step Description:**
Calculate the standard deviation and filter the array to return only the values that are greater than the `Mean + 1 Standard Deviation`.

**Logic & Planning:**

```python
# Calculate the standard deviation of the riders_array.
# Define a threshold value equal to the mean plus one standard deviation.
# Create a new array containing only values greater than the threshold.
# Print the high traffic values.

```

**Solution:**

```python
# Use np.std to calculate the standard deviation of the ridership
std_dev = np.std(riders_array)

# Calculate the numeric threshold for high traffic (Mean + Std Dev)
threshold = mean_ridership + std_dev

# Use boolean masking to select only elements greater than the threshold
high_traffic_stations = riders_array[riders_array > threshold]

# Print the resulting high traffic counts
print(f"High Traffic Counts: {high_traffic_stations}")

```

---

### Final Instructions: Run the Application

Combine the blocks below into a single script to see the NumPy pipeline efficiency.

```python
import numpy as np

# 1. Setup Data
riders_list = [45, 120, 38, 310, 0, 55, 22, 150, 0, 280]
revenue_list = [112.50, 360.00, 115.00, 930.00, 450.00, 137.50, 66.00, 450.00, 100.00, 840.00]

# 2. Conversion
riders_array = np.array(riders_list, dtype=float)
revenue_array = np.array(revenue_list, dtype=float)

# 3. Cleaning (Imputation)
riders_array[riders_array == 0] = np.nan
mean_ridership = np.nanmean(riders_array)
riders_array[np.isnan(riders_array)] = mean_ridership
print(f"Cleaned Data: {riders_array}")

# 4. Vectorized Transformation
adjusted_revenue = revenue_array * 1.15
print(f"Projected Revenue (+15%): {adjusted_revenue}")

# 5. Analysis
threshold = mean_ridership + np.std(riders_array)
high_traffic = riders_array[riders_array > threshold]
print(f"Busiest Stations: {high_traffic}")

```
