**File Name:** `Project_3_Retail_Analyst.ipynb`

---

# 🛠️ Mini-Project: The Retail Analytics Dashboard

**Project Duration:** ~1 Hour
**Goal:** You are a Data Analyst for a retail chain. You have data scattered across multiple CSV files (January Sales, February Sales, Product Info, and Customer Info). Your task is to build a unified dataset, calculate profitability, categorise your customers, and generate a summary report for the CEO.

**The Application Flow:**

1. **Consolidate:** Combine monthly transaction files into one master list (`concat`).
2. **Enrich:** Merge product and customer details into the transactions (`merge`).
3. **Calculate:** Create new columns for Revenue and Profit (Column Ops).
4. **Decode:** Map short region codes (e.g., 'N') to full names ('North') (`map`).
5. **Classify:** Tag orders as "High Value" or "Standard" based on revenue (`apply`).
6. **Analyze:** Group data to find top-performing regions (`groupby`, `agg`).
7. **Report:** Create a pivot table for product performance and save the best deals (`pivot`, `sort`).

---

### 0. Setup: Generating the Scattered Data

*Run this cell first. It simulates the real-world problem of having data split across multiple files.*

```python
import pandas as pd
import numpy as np

# 1. Product Database (Cost Price info)
products = pd.DataFrame({
    'Prod_ID': [101, 102, 103],
    'Category': ['Electronics', 'Home', 'Clothing'],
    'Cost_Price': [500, 40, 20] 
})
products.to_csv('products.csv', index=False)

# 2. Customer Database (Demographics)
customers = pd.DataFrame({
    'Cust_ID': ['C1', 'C2', 'C3', 'C4'],
    'Region_Code': ['N', 'S', 'E', 'W']
})
customers.to_csv('customers.csv', index=False)

# 3. January Transactions
trans_jan = pd.DataFrame({
    'Trans_ID': ['T1', 'T2'],
    'Cust_ID': ['C1', 'C2'],
    'Prod_ID': [101, 102],
    'Qty': [1, 5],
    'Sale_Price': [800, 80] # Selling price is higher than Cost_Price
})
trans_jan.to_csv('sales_jan.csv', index=False)

# 4. February Transactions
trans_feb = pd.DataFrame({
    'Trans_ID': ['T3', 'T4', 'T5'],
    'Cust_ID': ['C3', 'C1', 'C4'],
    'Prod_ID': [103, 101, 102],
    'Qty': [10, 1, 2],
    'Sale_Price': [50, 800, 80]
})
trans_feb.to_csv('sales_feb.csv', index=False)

print("Setup Complete: 4 CSV files created.")

```

---

### Step 1: Consolidating History (`concat`)

**Logic:** We cannot analyze January and February separately. We need to stack them vertically into a single "Year-to-Date" dataframe.

**Task:** Load both sales CSVs and concatenate them into one dataframe named `df_sales`.

**[Student Input Cell]**

```python
# 1. Import pandas

# 2. Read 'sales_jan.csv' into a variable named 'jan_df'

# 3. Read 'sales_feb.csv' into a variable named 'feb_df'

# 4. Use pd.concat() to combine them into a list. Assign result to 'df_sales'.
#    Hint: pd.concat([df1, df2], ignore_index=True)

# 5. Print the shape of df_sales (Should be 5 rows total)

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
import pandas as pd

# 2 & 3. Read files
jan_df = pd.read_csv('sales_jan.csv')
feb_df = pd.read_csv('sales_feb.csv')

# 4. Concatenate
df_sales = pd.concat([jan_df, feb_df], ignore_index=True)

# 5. Check shape
print("Total Rows:", df_sales.shape[0])

```

---

### Step 2: Enriching the Data (`merge`)

**Logic:** `df_sales` currently only has IDs (`Prod_ID`, `Cust_ID`). This is not useful for a human reading the report. We need to join this with our `products` and `customers` files to get names and costs.

**Task:** Perform two merges. First with Products, then with Customers.

**[Student Input Cell]**

```python
# 1. Read 'products.csv' into 'prod_df' and 'customers.csv' into 'cust_df'

# 2. Merge 'df_sales' with 'prod_df' on the column 'Prod_ID'. 
#    Use an 'left' join (we want to keep all sales even if product info is missing).
#    Overwrite 'df_sales' with this new result.

# 3. Merge the result ('df_sales') with 'cust_df' on 'Cust_ID'.
#    Again, use a 'left' join. Overwrite 'df_sales'.

# 4. Print the first 5 rows. You should now see 'Category' and 'Region_Code' columns.

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Load lookups
prod_df = pd.read_csv('products.csv')
cust_df = pd.read_csv('customers.csv')

# 2. Merge Products
df_sales = pd.merge(df_sales, prod_df, on='Prod_ID', how='left')

# 3. Merge Customers
df_sales = pd.merge(df_sales, cust_df, on='Cust_ID', how='left')

# 4. Verify
print(df_sales.head())

```

---

### Step 3: Financial Metrics (Column Ops)

**Logic:** We have `Qty`, `Sale_Price`, and `Cost_Price`. We need to calculate how much money we made.

* `Revenue` = Qty * Sale_Price
* `Total_Cost` = Qty * Cost_Price
* `Profit` = Revenue - Total_Cost

**Task:** Create these three columns.

**[Student Input Cell]**

```python
# 1. Create a column 'Revenue' by multiplying 'Qty' * 'Sale_Price'

# 2. Create a column 'Total_Cost' by multiplying 'Qty' * 'Cost_Price'

# 3. Create a column 'Profit' by subtracting 'Total_Cost' from 'Revenue'

# 4. Print df_sales[['Revenue', 'Profit']].head() to check

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Revenue
df_sales['Revenue'] = df_sales['Qty'] * df_sales['Sale_Price']

# 2. Cost
df_sales['Total_Cost'] = df_sales['Qty'] * df_sales['Cost_Price']

# 3. Profit
df_sales['Profit'] = df_sales['Revenue'] - df_sales['Total_Cost']

# 4. Check
print(df_sales[['Revenue', 'Profit']].head())

```

---

### Step 4: Decoding Regions (`map`)

**Logic:** The `Region_Code` is "N", "S", etc. The CEO wants to read "North", "South". We will use `.map()` to fix this.

**Task:** Create a dictionary and map the column.

**[Student Input Cell]**

```python
# 1. Create a dictionary 'region_map' where:
#    'N': 'North', 'S': 'South', 'E': 'East', 'W': 'West'

# 2. Create a new column 'Region_Name'. 
#    Fill it by using .map(region_map) on the existing 'Region_Code' column.

# 3. Print the 'Region_Name' column to verify.

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Dictionary
region_map = {'N': 'North', 'S': 'South', 'E': 'East', 'W': 'West'}

# 2. Map
df_sales['Region_Name'] = df_sales['Region_Code'].map(region_map)

# 3. Check
print(df_sales['Region_Name'])

```

---

### Step 5: Classifying Orders (`apply`)

**Logic:** We want to flag "High Value" orders. If an order's Revenue is over 500, it is "High", otherwise it is "Standard". Since this involves "If/Else" logic, we use `.apply()`.

**Task:** Define a python function and apply it to the dataframe.

**[Student Input Cell]**

```python
# 1. Define a function named 'label_deal' that takes one input 'amount'.
#    Inside: If amount > 500 return "High Value", else return "Standard"

# 2. Create a new column 'Order_Type'.
#    Fill it by using .apply(label_deal) on the 'Revenue' column.

# 3. Print the 'Order_Type' column count using .value_counts()

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Function
def label_deal(amount):
    if amount > 500:
        return "High Value"
    else:
        return "Standard"

# 2. Apply
df_sales['Order_Type'] = df_sales['Revenue'].apply(label_deal)

# 3. Count
print(df_sales['Order_Type'].value_counts())

```

---

### Step 6: Executive Summary (`groupby` & `agg`)

**Logic:** The CEO asks: "Which Region is the most profitable, and how many sales did we have there?" We need to group by Region and aggregate the data.

**Task:** Group by `Region_Name` and calculate Sum of Profit and Count of IDs.

**[Student Input Cell]**

```python
# 1. Group 'df_sales' by 'Region_Name'.
#    Select the 'Profit' column.
#    Chain .sum() to it. Assign this to 'profit_by_region'.

# 2. Print 'profit_by_region'

# 3. (Advanced) Try using .agg() to calculate 'sum' of Profit AND 'count' of Trans_ID at the same time.
#    Syntax: df.groupby('Region_Name').agg({'Profit': 'sum', 'Trans_ID': 'count'})

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Simple Groupby
profit_by_region = df_sales.groupby('Region_Name')['Profit'].sum()
print("Total Profit by Region:\n", profit_by_region)

# 3. Advanced Aggregation
summary = df_sales.groupby('Region_Name').agg({
    'Profit': 'sum',
    'Trans_ID': 'count'
})
print("\nDetailed Summary:\n", summary)

```

---

### Step 7: The Product Matrix (`pivot_table` & `sort`)

**Logic:** We need a grid showing which Categories sell best in which Regions. A Pivot Table is perfect for this. Finally, we want to see our single most profitable transaction.

**Task:** Create a pivot table and sort the main dataframe.

**[Student Input Cell]**

```python
# 1. Create a pivot table named 'matrix'.
#    - data: df_sales
#    - index: 'Region_Name'
#    - columns: 'Category'
#    - values: 'Revenue'
#    - aggfunc: 'sum'

# 2. Print the pivot table

# 3. Sort 'df_sales' by 'Profit' in Descending order (ascending=False).
#    Print the top 3 rows.

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Pivot Table
matrix = pd.pivot_table(df_sales, 
                        index='Region_Name', 
                        columns='Category', 
                        values='Revenue', 
                        aggfunc='sum')
# 2. Print
print("Revenue Matrix:\n", matrix)

# 3. Sorting for top deals
top_deals = df_sales.sort_values(by='Profit', ascending=False).head(3)
print("\nTop 3 Profitable Transactions:\n", top_deals)

```

---

### 🏁 Final Step: Run the Full Report

**Instructions:** Combine the code blocks to generate the full dashboard.

**[Student Input Cell]**

```python
# COPY AND PASTE YOUR CODE HERE
# 1. Load & Concat
# ...
# 2. Merge Data
# ...
# 3. Calculate Metrics
# ...
# 4. Map & Apply Labels
# ...
# 5. Groupby Summary
# ...
# 6. Pivot Table
# ...
# 7. Sort Top Deals
# ...

print("Dashboard Analysis Complete!")

```