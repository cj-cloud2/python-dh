# Lab Sheet 2: Wrangling the Data

This lab focuses on the two most critical skills for a data scientist: **Inspection** (understanding what you have) and **Cleaning** (fixing errors/omissions).

### Topics Covered:

1. **Setup Phase** (Creating sample data)
2. **Data Inspection Attributes** (`.shape`, `.columns`, `.info()`)
3. **Statistical Summary** (`.describe()`)
4. **Selecting Data by Label** (`.loc`)
5. **Selecting Data by Position** (`.iloc`)
6. **Boolean Indexing** (Filtering data)
7. **Handling Missing Data** (Finding and filling `NaN` values)
8. **Data Type Conversion** (Fixing dates and numbers)
9. **Removing Duplicates**
10. **String Operations** (Cleaning text)

---

### 0. Setup Phase: Generate Sample Data

*Run this cell first to create the dataset we will use for the rest of the lab.*

```python
import pandas as pd
import numpy as np

# Creating a messy dataset for practice
data = {
    'Transaction_ID': ['TX100', 'TX101', 'TX102', 'TX103', 'TX104', 'TX100', 'TX105'], # Note the duplicate TX100
    'Date': ['2023-01-01', '2023-01-02', '2023-01-02', 'not_a_date', '2023-01-05', '2023-01-01', '2023-01-06'],
    'Customer_Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Alice', 'Frank'],
    'Product': ['Laptop', 'Mouse', 'Monitor', 'Laptop', 'Mouse', 'Laptop', 'Monitor'],
    'Price': [1200, 25, 300, 1200, '25', 1200, 300], # Price for Eve is a string '25'
    'Quantity': [1, 10, np.nan, 2, 5, 1, np.nan] # Missing values (NaN) in Quantity
}

df = pd.DataFrame(data)
# Saving to a file so we can treat it like a real external dataset
df.to_csv('sales_data_messy.csv', index=False)

print("Setup Complete: 'sales_data_messy.csv' created.")
print(df)

```

---

## 1. Data Inspection Attributes

**Concept:** Before analyzing, you need a high-level overview.

* `.shape`: Tells you the dimensions (Rows, Columns).
* `.columns`: Lists the column names.
* `.info()`: The most useful command. It checks for missing values (non-null count) and data types (Dtype).

**Sample Code:**

```python
# Load the data we just created
df = pd.read_csv('sales_data_messy.csv')

print("Shape:", df.shape)
print("Columns:", df.columns)
print("-" * 30)
df.info()

```

**Practice Cell:**

```python
# 1. Print the shape of the dataframe 'df'

# 2. Print the list of column names

# 3. Run .info() to see how many missing values exist in 'Quantity'


```

---

## 2. Statistical Summary

**Concept:** `.describe()` gives you a quick statistical summary of your **numerical** columns (Mean, Std Dev, Min, Max, Percentiles). It helps spot outliers immediately (e.g., if the 'Age' max is 200).

**Sample Code:**

```python
# Describe numerical columns
print(df.describe())

# Bonus: Describe ALL columns (including strings) to see unique counts
print(df.describe(include='all'))

```

**Practice Cell:**

```python
# 1. Run describe on the dataframe to see the stats for 'Quantity'

# 2. Look at the output. Why is 'Price' missing from the stats? (Hint: Remember we made one value a string in the setup?)


```

---

## 3. Selecting Data by Label (`.loc`)

**Concept:** `.loc[row_label, column_label]` is used when you know the **names** of the rows or columns you want. It is "Label-based".

* Format: `df.loc[rows, columns]`

**Sample Code:**

```python
# Set Transaction_ID as index first so we have meaningful labels
df_labeled = df.set_index('Transaction_ID')

# Select the row for 'TX102' and column 'Customer_Name'
print(df_labeled.loc['TX102', 'Customer_Name'])

# Select all rows for columns 'Product' and 'Price'
print(df_labeled.loc[:, ['Product', 'Price']].head())

```

**Practice Cell:**

```python
# 1. Create 'df_labeled' by setting 'Transaction_ID' as the index of 'df'

# 2. Use .loc to select the 'Product' purchased in transaction 'TX104'


```

---

## 4. Selecting Data by Position (`.iloc`)

**Concept:** `.iloc[row_position, column_position]` uses **Integer** positions (0, 1, 2...). It is used when you don't care about labels but want specific slices (e.g., "Give me the first 5 rows and the first 2 columns").

**Sample Code:**

```python
# Select the first row (index 0)
print(df.iloc[0])

# Select the first 3 rows and first 2 columns
# Syntax: [start_row : end_row, start_col : end_col]
print(df.iloc[0:3, 0:2])

```

**Practice Cell:**

```python
# 1. Use .iloc to fetch the row at position 2 (the 3rd row)

# 2. Use .iloc to fetch the first 5 rows and the last column only


```

---

## 5. Boolean Indexing (Filtering)

**Concept:** This is how you ask questions of your data. You create a "Condition" (True/False), and pass it to the DataFrame. It only keeps rows where the condition is True.

**Sample Code:**

```python
# Step 1: Create the condition
# check_laptop = df['Product'] == 'Laptop'

# Step 2: Pass it to the dataframe
laptops_only = df[df['Product'] == 'Laptop']
print(laptops_only)

```

**Practice Cell:**

```python
# 1. Filter the dataframe to show only rows where 'Customer_Name' is 'Alice'

# 2. (Advanced) Try to filter where 'Quantity' is greater than 1


```

---

## 6. Handling Missing Data

**Concept:** Real data has holes.

* `.isnull()`: Returns True if data is missing.
* `.dropna()`: Removes rows with missing data (Nuclear option).
* `.fillna()`: Fills missing data with a specific value (Safe option).

**Sample Code:**

```python
# Check for nulls
print(df.isnull().sum())

# Fill missing Quantity with 0
df['Quantity'] = df['Quantity'].fillna(0)
print(df)

```

**Practice Cell:**

```python
# 1. Check how many null values exist in the 'Quantity' column now (should be 0)

# 2. Create a test dataframe 'df_temp' that is a copy of 'df'

# 3. Use .dropna() on 'df_temp' to remove any rows that still have ANY missing values


```

---

## 7. Data Type Conversion

**Concept:** Sometimes numbers look like strings ("25" vs 25), or dates are just text. You cannot do math on strings.

* `.astype()`: Converts types (e.g., float to int).
* `pd.to_datetime()`: Converts text to understanding time.

**Sample Code:**

```python
# Fix Price: It was an 'object' (string) because of that one '25' value.
# coerce_errors='coerce' turns un-convertible text into NaN
df['Price'] = pd.to_numeric(df['Price'], errors='coerce')

# Fix Date:
df['Date'] = pd.to_datetime(df['Date'], errors='coerce')

print(df.info()) # Now Price is float/int and Date is datetime

```

**Practice Cell:**

```python
# 1. Convert the 'Quantity' column to type 'int' (integers) using .astype(int)

# 2. Print df.info() again to verify 'Quantity' is now an Integer


```

---

## 8. Removing Duplicates

**Concept:** Duplicate entries distort analysis (e.g., counting the same sale twice).

* `.duplicated()`: Marks duplicates.
* `.drop_duplicates()`: Removes them.

**Sample Code:**

```python
# Check for duplicates
print("Duplicates found:", df.duplicated().sum())

# Remove them
df = df.drop_duplicates()
print("Shape after removing duplicates:", df.shape)

```

**Practice Cell:**

```python
# 1. Check if there are any duplicates left in the dataframe

# 2. (Optional) Read the documentation or help for .drop_duplicates() to see how to keep the 'last' occurrence instead of 'first'


```

---

## 9. String Operations (`.str`)

**Concept:** When cleaning text columns, you must access them via the `.str` accessor. You can then use standard string methods like `upper()`, `lower()`, `strip()`, or `contains()`.

**Sample Code:**

```python
# Make all names uppercase
df['Customer_Name'] = df['Customer_Name'].str.upper()

# Find rows where Product contains 'Mon' (like Monitor)
monitors = df[df['Product'].str.contains('Mon')]
print(monitors)

```

**Practice Cell:**

```python
# 1. Convert the 'Product' column to all lowercase letters

# 2. Create a filter to find all rows where 'Customer_Name' contains the letter "A"


```