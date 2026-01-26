## **Lab Sheet: Advanced String Methods (Extension)**

**Time Allocation:** 35 Minutes

### **Topics Covered**

13. **Prefix & Suffix Checking**: `startswith()`, `endswith()`
14. **Zero Padding (Data Cleaning)**: `zfill()`
15. **Text Alignment**: `center()`, `ljust()`, `rjust()`
16. **Line Splitting**: `splitlines()`
17. **Partitioning**: `partition()` vs `split()`
18. **Reverse Search**: `rfind()`
19. **Case Validation**: `isupper()`, `islower()`, `istitle()`
20. **Whitespace Validation**: `isspace()`

---

### **13. Prefix & Suffix Checking**

In data cleaning, you often need to filter rows that start with specific codes (like country codes) or end with specific extensions (like ".csv").

* `startswith(value)`: Returns True if string starts with value.
* `endswith(value)`: Returns True if string ends with value.

```python
# Sample Code
filename = "report_2024.csv"
print(filename.startswith("report")) # True
print(filename.endswith(".pdf"))     # False

```

```python
# Practice: Create a variable 'url' = "https://www.google.com".
# Check if it starts with "https".
# Check if it ends with ".com".

```

---

### **14. Zero Padding (`zfill`)**

Data Scientists often deal with IDs (like Zip Codes or Employee IDs) that must be a fixed length. If an ID is "45" but needs to be "00045", we use `zfill()`.

* `zfill(width)`: Adds zeros to the beginning until the string reaches the specified width.

```python
# Sample Code
emp_id = "501"
# We want it to be 5 digits long
fixed_id = emp_id.zfill(5)
print(fixed_id)

```

```python
# Practice: Create a variable 'zip_code' = "801".
# Pad it with zeros so it becomes 6 digits long. Print the result.

```

---

### **15. Text Alignment**

When generating text reports (like the Resume Project), you might want to align text within a specific width.

* `center(width)`: Centers text.
* `ljust(width)`: Left aligns.
* `rjust(width)`: Right aligns.

```python
# Sample Code
word = "Python"
print(f"|{word.center(20)}|") # Centers Python in 20 spaces
print(f"|{word.ljust(20)}|")  # Pushes Python to the left

```

```python
# Practice: Create a variable 'title' = "Summary".
# Print it centered within 50 spaces, surrounded by pipes | like the sample above.

```

---

### **16. Line Splitting (`splitlines`)**

When reading raw text files, data often comes as one giant string with hidden "newline" characters (`\n`). `splitlines()` breaks them into a list of lines.

```python
# Sample Code
raw_text = "Line 1\nLine 2\nLine 3"
lines = raw_text.splitlines()
print(lines) # Returns ['Line 1', 'Line 2', 'Line 3']

```

```python
# Practice: Create a string 'address' = "Street 1\nCity\nZip".
# Use splitlines() to convert it into a list. Print the list.

```

---

### **17. Partitioning (`partition`)**

Unlike `split()`, which cuts a string into many parts, `partition()` cuts it into exactly **three** parts: (Before Match, The Match, After Match). This is great for extracting data when you only want the first occurrence.

```python
# Sample Code
email = "user.name@company.com"
# Split at the @ symbol
parts = email.partition("@")
print(parts)
print("Username:", parts[0])
print("Domain:", parts[2])

```

```python
# Practice: Create variable 'config' = "timeout=30".
# Partition it at the "=" sign.
# Print just the value (the part after the equal sign).

```

---

### **18. Reverse Search (`rfind`)**

`find()` looks for the *first* occurrence. `rfind()` looks for the *last* occurrence (searching from the Right).

* Useful for file paths: `C:/users/docs/file.txt` (Finding the last slash).

```python
# Sample Code
text = "apple banana apple mango"
print(text.find("apple"))  # Returns 0 (First one)
print(text.rfind("apple")) # Returns 13 (Last one)

```

```python
# Practice: Create variable 'path' = "folder/subfolder/document.txt".
# Find the position of the LAST slash "/" using rfind().

```

---

### **19. Case Validation**

Checks if the casing matches specific rules.

* `isupper()`: Is it ALL CAPS?
* `islower()`: Is it all lowercase?
* `istitle()`: Is It Title Case?

```python
# Sample Code
print("PYTHON".isupper()) # True
print("Python".islower()) # False
print("The End".istitle()) # True

```

```python
# Practice: Variable password = "PASSWORD123".
# Check if the password is all uppercase. Print the True/False result.

```

---

### **20. Whitespace Validation (`isspace`)**

Checks if a string consists *only* of whitespace (spaces, tabs, newlines). This is crucial for detecting empty lines in messy data.

```python
# Sample Code
blank = "   \t   "
print(blank.isspace()) # True

not_blank = "   .   "
print(not_blank.isspace()) # False (because of the dot)

```

```python
# Practice: Create a variable 'check' with 5 spaces inside quotes.
# Use .isspace() to verify it is empty whitespace.

```