# **Project: The Automated Inventory Manager**

**Time:** ~1 Hour
**Objective:** Build a tool that takes messy raw product data, cleans the text, applies dynamic pricing rules using logic, and filters out critical stock items for a report.

**Scenario:**
You are working for an e-commerce startup. The warehouse system sends you a messy export of daily inventory:

1. **Product Names** are inconsistent (mixed case, extra spaces).
2. **Prices** need to be adjusted: If we have too much stock (>50 units), we give a 10% discount to clear it.
3. **Stock Levels** need monitoring: We need a report of all items with low stock (< 10 units).
4. **Validation**: We must ensure no price is negative (data error).

---

## **Step 1: Data Cleaning (String Operations)**

**Logical Step:**
The raw product names have extra spaces and mixed capitalization (e.g., `"  lapTOP "`, `"iphone  "`). We need to standardize them to be fully Uppercase and stripped of extra whitespace using `numpy.char`.

**Student Task:**

```python
import numpy as np

# 1. Create an array 'raw_names' with values: ["  lapTOP ", "iphone  ", "  TabLET", "Monitor"]


# 2. Use np.char.strip() to remove leading/trailing spaces from 'raw_names'. Store in 'clean_names'.


# 3. Use np.char.upper() to convert 'clean_names' to uppercase. Store in 'final_names'.


# 4. Print 'final_names'. Result should be ["LAPTOP", "IPHONE", "TABLET", "MONITOR"]


```

**Solution:**

```python
import numpy as np

# 1. Raw Data
raw_names = np.array(["  lapTOP ", "iphone  ", "  TabLET", "Monitor"])

# 2. Strip Whitespace
clean_names = np.char.strip(raw_names)

# 3. Convert to Uppercase
final_names = np.char.upper(clean_names)

# 4. Print
print("Cleaned Names:", final_names)

```

---

## **Step 2: Dynamic Pricing (Conditional Logic)**

**Logical Step:**
We have `prices` and `stock`. We want to create a **New Price** array.

* **Rule:** If `stock` > 50, apply a 10% discount (Price * 0.9).
* **Otherwise:** Keep the original Price.
We will use `numpy.where` to implement this "If-Then" logic across the whole array at once.

**Student Task:**

```python
# 1. Create a 'prices' array: [1000.0, 800.0, 300.0, 150.0]


# 2. Create a 'stock' array: [10, 60, 5, 100] (Note: 2nd and 4th items are > 50)


# 3. Use np.where() to create 'new_prices'.
#    Condition: stock > 50
#    If True: prices * 0.9
#    If False: prices


# 4. Print the 'new_prices'. (Check if 800 became 720, and 150 became 135)


```

**Solution:**

```python
# 1. Setup Data
prices = np.array([1000.0, 800.0, 300.0, 150.0])
stock = np.array([10, 60, 5, 100])

# 2. Apply Dynamic Pricing Logic
# Logic: IF stock > 50, THEN price * 0.9, ELSE keep price
new_prices = np.where(stock > 50, prices * 0.9, prices)

print("Original Prices:", prices)
print("Adjusted Prices:", new_prices)

```

---

## **Step 3: Low Stock Alert (Masking)**

**Logical Step:**
We need to generate a report of items that are running low. We will use **Boolean Masking**.

1. Create a mask (True/False) where `stock < 10`.
2. Use this mask to filter the `final_names` array we created in Step 1.

**Student Task:**

```python
# 1. Create a boolean mask called 'low_stock_mask' where 'stock' is less than 10


# 2. Print the mask (Should look like [True, False, True, False])


# 3. Use the mask to select only the names from 'final_names' that are low stock.
#    Store in 'critical_items'.


# 4. Print 'critical_items'.


```

**Solution:**

```python
# 1. Create Mask
low_stock_mask = stock < 10
print("Mask:", low_stock_mask)

# 2. Filter Names
critical_items = final_names[low_stock_mask]

# 3. Print Report
print("Critical Low Stock Items:", critical_items)

```

---

## **Step 4: Data Validation (`numpy.testing`)**

**Logical Step:**
Before we save our data, we must ensure integrity. A price can never be negative. We will use `numpy.testing.assert_array_equal` (or logic with assertions) to ensure our data is valid.
*Note: In this specific step, we will use a simple logical check with `assert` combined with `np.all`.*

**Student Task:**

```python
# 1. Use np.all() to check if ALL 'new_prices' are greater than 0. Store in 'is_valid'.


# 2. Use a standard Python assert statement to check if 'is_valid' is True.
#    Message: "Error: Negative prices detected!"


# 3. If the assert passes (no error), print "Data Validation Passed: All prices valid."


```

**Solution:**

```python
# 1. Check validity
# np.all() returns True only if EVERY item in the array is True
is_valid = np.all(new_prices > 0)

# 2. Assert
assert is_valid == True, "Error: Negative prices detected!"

# 3. Success message
print("Data Validation Passed: All prices valid.")

```

---

## **Step 5: The Final Application**

**Logical Step:**
Combine all steps into a function `inventory_report(names, prices, stock)`. This function should return a dictionary containing the cleaned names, the new prices, and a list of critical items.

**Student Task:**

```python
def inventory_manager(raw_names_list, prices_list, stock_list):
    # 1. Convert inputs to NumPy arrays
    names_arr = np.array(raw_names_list)
    prices_arr = np.array(prices_list)
    stock_arr = np.array(stock_list)
    
    # 2. Clean Names (Strip and Upper)
    
    # 3. Calculate New Prices (Apply 10% discount if stock > 50)
    
    # 4. Find Critical Items (Names where stock < 10)
    
    # 5. Validate Prices (Check all > 0) - Raise error if not
    
    # 6. Return a Dictionary with keys: 'CleanedNames', 'FinalPrices', 'CriticalItems'
    pass # Remove pass

# Test Data
n = ["  apple ", "banana", "Cherry  ", "  date"]
p = [1.0, 0.5, 2.0, 5.0]
s = [100, 5, 60, 2] # Critical: Banana (5) and Date (2)

# Run Application
# result = inventory_manager(n, p, s)
# print(result)

```

**Solution:**

```python
def inventory_manager(raw_names_list, prices_list, stock_list):
    # 1. Convert
    names_arr = np.array(raw_names_list)
    prices_arr = np.array(prices_list)
    stock_arr = np.array(stock_list)
    
    # 2. Clean
    clean_names = np.char.upper(np.char.strip(names_arr))
    
    # 3. Pricing Logic
    final_prices = np.where(stock_arr > 50, prices_arr * 0.9, prices_arr)
    
    # 4. Critical Items
    mask = stock_arr < 10
    critical_items = clean_names[mask]
    
    # 5. Validation
    if not np.all(final_prices > 0):
        raise ValueError("Invalid Data: Negative prices found")
        
    # 6. Return
    return {
        "CleanedNames": clean_names,
        "FinalPrices": final_prices,
        "CriticalItems": critical_items
    }

# Test
n = ["  apple ", "banana", "Cherry  ", "  date"]
p = [1.0, 0.5, 2.0, 5.0]
s = [100, 5, 60, 2]

result = inventory_manager(n, p, s)
print("Full Report:\n", result)

```