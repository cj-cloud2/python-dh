# **Lab Project: The "E-Commerce Receipt Generator"**

**Time Allocation:** 1 Hour

### **The Goal**

You are building the backend logic for a Point-of-Sale (POS) system.
The system needs to take raw, messy input from a cashier and generate a perfectly formatted, centered, and professional receipt string to be printed.

### **Application Requirements**

1. **Store Header:** The store name must be perfectly centered on the receipt. The address (which might be multi-line) needs to be processed line-by-line.
2. **Transaction ID:** The cashier scans a raw code (e.g., "txn-55"). You must parse it and format it into a standardized 8-digit ID (e.g., "00000055").
3. **Item Formatting:** The item name and price must be aligned to opposite sides of the receipt (Left vs. Right) to look professional.
4. **Validation:** You must check if a discount code is valid (starts with "SAVE") and if the cashier left a "Notes" section empty (whitespace check).

---

### **Step 1: The Header (Center & Splitlines)**

**Logic:**
We need to create the top of the receipt. The store name should be centered within a specific width (let's say 40 characters). The address might be entered with newlines (e.g., "Street\nCity"), so we need to split it to print each line separately.

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Define a variable 'receipt_width' and set it to 40.

# 2. Ask the user for 'store_name'.

# 3. Ask the user for 'store_address'. Tell them they can use \n for new lines.
#    (Example input: 123 Main St\nNew York, NY)

# 4. Create 'header_centered': Use .center() to center the store_name within 'receipt_width'.

# 5. Create 'address_lines': Use .splitlines() on the store_address variable.
#    (This creates a list of strings).

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 1 Solution:**

```python
# 1. Configuration
receipt_width = 40

# 2. Inputs
store_name = input("Enter Store Name: ")
store_address = input("Enter Address (use \\n for new lines): ")

# 3. Processing
header_centered = store_name.center(receipt_width)
address_lines = store_address.splitlines()

# Note: We aren't printing yet, just preparing the variables!

```

---

### **Step 2: Parsing the Transaction ID (Partition & Zfill)**

**Logic:**
The scanning gun returns a raw string like `txn-402`. We need to separate the prefix (`txn`) from the number (`402`) using `partition`. Then, we need to take that number and pad it with zeros using `zfill` so it looks like a secure ID (`00000402`).

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Ask the user to input the 'raw_txn' (e.g., "txn-50").

# 2. Use .partition("-") on 'raw_txn' to split it.
#    Save the result into a variable called 'txn_parts'.

# 3. Extract the number part.
#    Hint: partition returns a tuple (part_before, separator, part_after).
#    You want the part_after, which is at index 2.
#    Save this to 'txn_number'.

# 4. Create 'clean_id': Apply .zfill(8) to the 'txn_number'.

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 2 Solution:**

```python
# 1. Input
raw_txn = input("Scan Transaction Code (e.g., txn-50): ")

# 2. Partition
txn_parts = raw_txn.partition("-")

# 3. Extraction (Index 2 holds the part AFTER the dash)
txn_number = txn_parts[2]

# 4. Padding
clean_id = txn_number.zfill(8)

```

---

### **Step 3: Item Alignment (Ljust & Rjust)**

**Logic:**
A receipt looks good because the Item Name is on the Left, and the Price is on the Right. We will use `ljust` and `rjust` to push text to the edges of our 40-character width.

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Ask user for 'item_name'.

# 2. Ask user for 'item_price'.

# 3. Create 'display_item': Use .ljust(30) on item_name to occupy the left 30 chars.
#    (We use 30 so there is room left for the price).

# 4. Create 'display_price': Use .rjust(10) on item_price to occupy the remaining 10 chars.

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 3 Solution:**

```python
# 1. Inputs
item_name = input("Enter Item Name: ")
item_price = input("Enter Price: ")

# 2. Formatting
# Total width is 40. We give 30 to name, 10 to price.
display_item = item_name.ljust(30)
display_price = item_price.rjust(10)

```

---

### **Step 4: Validation (Startswith & Isspace)**

**Logic:**
We need to check if a discount code is applicable. Valid codes must start with "SAVE". We also check if the cashier added any notes; if the notes are just empty spaces, we ignore them (or flag them).

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Ask user for 'promo_code'.

# 2. Create boolean variable 'is_valid_promo': Check if promo_code .startswith("SAVE").

# 3. Ask user for 'cashier_notes' (e.g., "  ").

# 4. Create boolean variable 'is_empty_note': Check if cashier_notes .isspace().

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 4 Solution:**

```python
# 1. Inputs
promo_code = input("Enter Promo Code: ")
cashier_notes = input("Enter Notes (or leave blank): ")

# 2. Validation Logic
is_valid_promo = promo_code.startswith("SAVE")
is_empty_note = cashier_notes.isspace()

```

---

### **Step 5: Assemble the Receipt Printer**

Now, combine all the logic into one final script. We will add the `print` statements at the end to generate the actual visual receipt.

**⬇️ Paste all code below and run it! ⬇️**

```python
# --- CONFIGURATION ---
receipt_width = 40
border = "=" * receipt_width

# --- INPUTS ---
print("--- DATA ENTRY ---")


# --- PROCESSING & LOGIC ---


# --- RECEIPT OUTPUT ---
print("\n\n")
print(border)
# Print the centered header
print(header_centered)
print("-" * receipt_width)

# Print the address lines (Since we can't loop yet, we assume 2 lines max or just print the list)
# For this lab, let's just print the raw list to see the splitlines result
print(f"Store Loc: {address_lines}")

print(border)
print(f"TXN ID: {clean_id}")
print("-" * receipt_width)

# Print the aligned item row
# Combining left aligned name + right aligned price
print(f"{display_item}{display_price}")

print("-" * receipt_width)
print(f"Promo Valid: {is_valid_promo}")
print(f"Notes Empty: {is_empty_note}")
print(border)

```