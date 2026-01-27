**File Name:** `Project_2_The_Data_Janitor.ipynb`

---

# 🛠️ Mini-Project: The "Dirty Log" Cleaner

**Project Duration:** ~1 Hour
**Goal:** You have received a messy server log file from the IT department. Your job is to build a cleaning pipeline that ingests this raw, dirty data and outputs a clean, usable report of "Critical Errors" for the engineering team.

**The Application Flow:**

1. **Ingest:** Load the dirty CSV file.
2. **Inspect:** Identify the mess (missing values, wrong types, duplicates).
3. **Scrub:** Remove duplicates and standardize text formats.
4. **Fix:** Convert columns to the correct data types (Dates, Numbers).
5. **Filter:** Extract only the specific data we care about (Critical Errors).
6. **Report:** Save the clean data to a new file.

---

### 0. Setup: Generating the Messy Data

*Run this cell first. It creates the "server_logs_dirty.csv" file you will be working on.*

```python
import pandas as pd
import numpy as np

# Creating a messy log dataset
raw_data = {
    'Log_ID': ['1001', '1002', '1003', '1001', '1004', '1005', '1006'], # Duplicate 1001
    'Timestamp': ['2023-10-01 10:00:00', '2023-10-01 10:05:00', 'Error_Date', '2023-10-01 10:00:00', '2023-10-01 10:15:00', None, '2023-10-01 10:25:00'],
    'User_Name': ['admin', 'JohnDoe', 'jane_smith', 'admin', 'JOHNDOE', 'guest', 'Admin'], # Inconsistent casing
    'Status_Code': ['200', '404', '500', '200', '404', '200', '500'], # All strings
    'Response_Time_ms': [120, 45, 'Slow', 120, 50, 90, 3000] # Mixed types (one string 'Slow')
}

df_setup = pd.DataFrame(raw_data)
df_setup.to_csv('server_logs_dirty.csv', index=False)
print("Setup Complete: 'server_logs_dirty.csv' created.")

```

---

### Step 1: Initial Reconnaissance (Inspection)

**Logic:** Before touching the data, we must understand the extent of the damage. We need to load the file and check three things: the size of the data, the column names, and the data types/missing values.

**Task:** Load the CSV and print its `.info()` and `.head()`.

**[Student Input Cell]**

```python
# 1. Import pandas as pd

# 2. Read 'server_logs_dirty.csv' into a DataFrame named 'df_logs'

# 3. Print the shape of the dataframe to see how many rows we start with

# 4. Print the .info() summary to look for nulls and incorrect data types

# 5. Display the first 5 rows to visually inspect the mess

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
import pandas as pd

# 2. Read the file
df_logs = pd.read_csv('server_logs_dirty.csv')

# 3. Print Shape
print("Original Shape:", df_logs.shape)

# 4. Print Info
print("\n--- Info Summary ---")
df_logs.info()

# 5. Display Head
print("\n--- First 5 Rows ---")
print(df_logs.head())

```

---

### Step 2: De-Duplication

**Logic:** During inspection (Step 1), you might have noticed `Log_ID: 1001` appeared twice. Duplicate data corrupts analysis. We need to find them and remove them.

**Task:** Count the duplicates, then drop them.

**[Student Input Cell]**

```python
# 1. Print the number of duplicated rows using .duplicated().sum()

# 2. Remove duplicates using .drop_duplicates(). 
#    IMPORTANT: Remember to re-assign this back to 'df_logs' (e.g., df_logs = ...)

# 3. Print the new shape of df_logs to confirm rows were removed

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Count duplicates
print("Duplicates found:", df_logs.duplicated().sum())

# 2. Drop duplicates
df_logs = df_logs.drop_duplicates()

# 3. Verify shape
print("New Shape:", df_logs.shape)

```

---

### Step 3: Text Standardization (String Cleaning)

**Logic:** In the `User_Name` column, we have "admin", "Admin", "JohnDoe", and "JOHNDOE". To a computer, "admin" and "Admin" are different people. We need to standardize everyone to lowercase so we can group them accurately later.

**Task:** Convert the `User_Name` column to lowercase and strip whitespace.

**[Student Input Cell]**

```python
# 1. Access the 'User_Name' column via the .str accessor and convert it to lowercase.
#    Assign this result back to df_logs['User_Name']

# 2. (Optional but good practice) Chain the .strip() method to remove accidental spaces.

# 3. Print the unique values in 'User_Name' to verify they are clean.

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Convert to lowercase and strip whitespace
df_logs['User_Name'] = df_logs['User_Name'].str.lower().str.strip()

# 3. Verify unique values
print("Unique Users:", df_logs['User_Name'].unique())

```

---

### Step 4: Type Casting & Error Handling

**Logic:**

1. `Timestamp` is currently an Object (string) because of bad data like "Error_Date". We need to force it to Datetime.
2. `Response_Time_ms` is an Object because of the string "Slow". We need to force it to Numeric.
We will use `errors='coerce'` to turn un-convertible garbage into `NaN` (Not a Number).

**Task:** Convert Timestamp to datetime and Response_Time_ms to numeric.

**[Student Input Cell]**

```python
# 1. Convert 'Timestamp' column using pd.to_datetime().
#    Pass errors='coerce' to handle the bad dates.

# 2. Convert 'Response_Time_ms' column using pd.to_numeric().
#    Pass errors='coerce' to handle the text 'Slow'.

# 3. Check df_logs.info() again. You should see 'datetime64' and 'float64' types now.

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Fix Timestamp
df_logs['Timestamp'] = pd.to_datetime(df_logs['Timestamp'], errors='coerce')

# 2. Fix Response Time
df_logs['Response_Time_ms'] = pd.to_numeric(df_logs['Response_Time_ms'], errors='coerce')

# 3. Verify types
df_logs.info()

```

---

### Step 5: Handling the Fallout (Missing Data)

**Logic:** Because we forced our type conversions in Step 4, the bad data ("Error_Date", "Slow", and original missing values) have all turned into `NaN`. We cannot report on missing data. We must remove these broken rows.

**Task:** Drop any row that contains a `NaN` value.

**[Student Input Cell]**

```python
# 1. Print the total number of missing values per column (isnull().sum())

# 2. Drop all rows containing missing values using .dropna()
#    Assign the result back to df_logs

# 3. Print the shape to see how many valid rows remain

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1. Check nulls
print("Missing values:\n", df_logs.isnull().sum())

# 2. Drop nulls
df_logs = df_logs.dropna()

# 3. Final Shape
print("Final Clean Shape:", df_logs.shape)

```

---

### Step 6: The "Critical Error" Filter

**Logic:** The engineering team only wants to see transactions where the **Status_Code is 500** (Server Error). We need to filter our clean dataset to find only these specific rows.

**Task:** Filter the data for Status Code "500".

**[Student Input Cell]**

```python
# 1. Create a boolean filter/mask where 'Status_Code' equals "500" 
#    (Note: Check if Status_Code is a string "500" or number 500 based on your initial info, it is likely a string).

# 2. Apply this filter to df_logs and store the result in a new dataframe 'df_critical'

# 3. Print 'df_critical'

```








**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**








**[Solution Cell]**

```python
# 1 & 2. Filter for Status Code 500
# Note: In the raw data, Status_Code was created as a string.
df_critical = df_logs[df_logs['Status_Code'] == '500']

# 3. Show result
print(df_critical)

```

---

### 🏁 Final Step: The Full Pipeline

**Instructions:** Combine all the logic above into one script. This script will take the raw file, clean it, and save the critical errors to `critical_report.csv`.

**[Student Input Cell]**

```python
# COPY AND PASTE YOUR PREVIOUS CODE BLOCKS HERE TO RUN AS ONE PIPELINE

# 1. Load Data
# ...

# 2. Drop Duplicates
# ...

# 3. Clean User Strings
# ...

# 4. Convert Types (Coerce errors)
# ...

# 5. Drop NaN values
# ...

# 6. Filter for '500' errors
# ...

# 7. Save the result to 'critical_report.csv'
# ...

print("Pipeline Finished. Report generated.")

```