# Lab Sheet 3: Transformation, Aggregation & Combining Data

### Topics Covered:

1. **Setup Phase** (Creating relational datasets)
2. **Column Operations** (Creating new features)
3. **Mapping Values** (`.map`)
4. **Custom Transformations** (`.apply`)
5. **Sorting Data** (`.sort_values`)
6. **Grouping Data** (`.groupby`)
7. **Advanced Aggregation** (`.agg`)
8. **Pivot Tables** (`pd.pivot_table`)
9. **Concatenating Data** (`pd.concat`)
10. **Merging/Joining Data** (`pd.merge`)

---

### 0. Setup Phase: Generate Sample Data

*Run this cell first. We are creating three datasets: Sales data for analysis, and Employee/Department tables for merging practice.*

```python
import pandas as pd
import numpy as np

# 1. Sales Data (For Transformation & Grouping)
sales_data = {
    'Region': ['North', 'North', 'South', 'South', 'East', 'East', 'West', 'West'],
    'Product': ['A', 'B', 'A', 'B', 'A', 'B', 'A', 'B'],
    'Sales_Amount': [1000, 1500, 500, 750, 1200, 1100, 1300, 900],
    'Cost': [600, 900, 300, 450, 700, 600, 800, 500]
}
df_sales = pd.DataFrame(sales_data)

# 2. Employee Data (For Merging)
employees = {
    'Emp_ID': [101, 102, 103, 104],
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Dept_ID': ['D1', 'D2', 'D1', 'D3'] # Note D3 exists here
}
df_emps = pd.DataFrame(employees)

# 3. Department Data (For Merging)
departments = {
    'Dept_ID': ['D1', 'D2', 'D4'], # Note D4 exists here (but not D3)
    'Dept_Name': ['HR', 'IT', 'Marketing']
}
df_depts = pd.DataFrame(departments)

print("Setup Complete.")
print("df_sales:\n", df_sales.head(3))

```

---

## 1. Column Operations

**Concept:** The fastest way to manipulate data in Pandas is using "Vectorized Operations". You can add, subtract, multiply, or divide entire columns just like they were single numbers.

**Sample Code:**

```python
# Calculate Profit by subtracting Cost from Sales_Amount
df_sales['Profit'] = df_sales['Sales_Amount'] - df_sales['Cost']

# Calculate Profit Margin percentage
df_sales['Margin_Pct'] = (df_sales['Profit'] / df_sales['Sales_Amount']) * 100

print(df_sales.head())

```

**Practice Cell:**

```python
# 1. Create a new column 'Total_Transaction' which is Sales_Amount + Cost (Just for practice)

# 2. Create a column 'Discounted_Sales' that represents 90% of the 'Sales_Amount' (multiply by 0.9)


```

---

## 2. Mapping Values (`.map`)

**Concept:** `.map()` is used to substitute each value in a Series with another value. It is commonly used with a Dictionary where `{old_value : new_value}`. It is great for coding categorical data (e.g., changing 'M' to 'Male').

**Sample Code:**

```python
# Let's map Region names to Codes
region_codes = {'North': 'N', 'South': 'S', 'East': 'E', 'West': 'W'}

df_sales['Region_Code'] = df_sales['Region'].map(region_codes)
print(df_sales[['Region', 'Region_Code']].head())

```

**Practice Cell:**

```python
# 1. Create a dictionary named 'product_map' that maps 'A' to 'Standard' and 'B' to 'Premium'

# 2. Use .map() to create a new column 'Product_Category' in 'df_sales' using that dictionary


```

---

## 3. Custom Transformations (`.apply`)

**Concept:** When you need to perform a complex logic that isn't a simple math operation, use `.apply()`. It allows you to "apply" a Python function to every single row or element.

**Sample Code:**

```python
# Define a custom function
def tax_calculator(amount):
    if amount > 1000:
        return amount * 0.15 # High tax
    else:
        return amount * 0.05 # Low tax

# Apply it to the Sales_Amount column
df_sales['Tax'] = df_sales['Sales_Amount'].apply(tax_calculator)
print(df_sales[['Sales_Amount', 'Tax']].head())

```

**Practice Cell:**

```python
# 1. Define a function 'performance_rating' that returns "High" if profit is > 400, else "Normal"

# 2. Use .apply() on the 'Profit' column to create a new column 'Rating'


```

---

## 4. Sorting Data (`.sort_values`)

**Concept:** Arranging data to find the highest or lowest values.

* `.sort_values(by='Column')`: Sorts by column.
* `ascending=False`: Used for descending order (highest on top).

**Sample Code:**

```python
# Sort by Sales Amount (Highest first)
df_sorted = df_sales.sort_values(by='Sales_Amount', ascending=False)
print(df_sorted.head())

```

**Practice Cell:**

```python
# 1. Sort the dataframe by 'Profit' in ascending order (lowest profit first)

# 2. (Advanced) Try sorting by two columns: ['Region', 'Sales_Amount']


```

---

## 5. Grouping Data (`.groupby`)

**Concept:** This is the "Split-Apply-Combine" strategy. You **Split** the data into groups (e.g., by Region), **Apply** a function (e.g., sum), and **Combine** the results. It answers questions like "What is the total sales per Region?".

**Sample Code:**

```python
# Group by Region and Sum the numeric columns
region_group = df_sales.groupby('Region').sum()
print(region_group)

# Note: The 'Region' becomes the Index of the new dataframe.

```

**Practice Cell:**

```python
# 1. Group 'df_sales' by 'Product'

# 2. Calculate the .mean() (average) for each product group


```

---

## 6. Advanced Aggregation (`.agg`)

**Concept:** Sometimes `.sum()` or `.mean()` isn't enough. You might want the Sum of Sales AND the Average Cost at the same time. The `.agg()` method allows multiple calculations at once.

**Sample Code:**

```python
# Get the Count, Mean, and Max of Sales_Amount for each Region
summary = df_sales.groupby('Region')['Sales_Amount'].agg(['count', 'mean', 'max'])
print(summary)

```

**Practice Cell:**

```python
# 1. Group by 'Product'

# 2. Use .agg() to find the 'min' and 'max' of the 'Profit' column


```

---

## 7. Pivot Tables (`pd.pivot_table`)

**Concept:** A Pivot Table allows you to group by **two** different categories at once (Rows and Columns), exactly like Excel.

**Sample Code:**

```python
# Index (Rows) = Region, Columns = Product, Values = Sales_Amount
pivot = pd.pivot_table(df_sales, 
                       values='Sales_Amount', 
                       index='Region', 
                       columns='Product', 
                       aggfunc='sum')
print(pivot)

```

**Practice Cell:**

```python
# 1. Create a pivot table showing the 'mean' (average) 'Profit'

# 2. Use 'Region' as the Index and 'Product' as the Columns


```

---

## 8. Concatenating Data (`pd.concat`)

**Concept:** Stacking two dataframes on top of each other. This is common when you have "January Data" in one file and "February Data" in another, and they have the same column names.

**Sample Code:**

```python
# Let's split our dataset into two parts to simulate this
part1 = df_sales.iloc[0:2] # First 2 rows
part2 = df_sales.iloc[5:7] # Rows 5 and 6

# Glue them back together vertically
combined_df = pd.concat([part1, part2])
print(combined_df)

```

**Practice Cell:**

```python
# 1. Create a variable 'top_rows' with the first 3 rows of df_sales

# 2. Create a variable 'bottom_rows' with the last 3 rows of df_sales

# 3. Use pd.concat() to combine them into 'df_combined'


```

---

## 9. Merging/Joining Data (`pd.merge`)

**Concept:** Joining two **different** tables based on a shared "Key" (ID). This is exactly like SQL JOINs.

* **Inner Join**: Keeps only IDs found in BOTH tables.
* **Left Join**: Keeps all IDs from the Left table, and matches found in Right.

**Sample Code:**

```python
# Reminder of our data:
# df_emps has Dept_ID: D1, D2, D1, D3
# df_depts has Dept_ID: D1, D2, D4

# INNER JOIN: Only D1 and D2 match. D3 (David) and D4 (Marketing) are lost.
inner_join = pd.merge(df_emps, df_depts, on='Dept_ID', how='inner')
print("Inner Join:\n", inner_join)

# LEFT JOIN: Keeps all Employees (Left table). David (D3) stays, but Dept_Name is NaN.
left_join = pd.merge(df_emps, df_depts, on='Dept_ID', how='left')
print("\nLeft Join:\n", left_join)

```

**Practice Cell:**

```python
# 1. Perform an OUTER join using how='outer' on 'df_emps' and 'df_depts'
#    (This should keep David AND Marketing, filling gaps with NaN)

# 2. Print the result to analyze the missing values


```