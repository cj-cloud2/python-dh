## **Lab Sheet: String Operations & Formatting**

**Time Allocation:** 90 Minutes

### **Topics Covered**

1. **String Concatenation (`+`)**: Combining text.
2. **String Repetition (`*`)**: Repeating text patterns.
3. **Membership Operators (`in`, `not in`)**: Checking content.
4. **The F-String**: Injecting data into text.
5. **Number Formatting**: Controlling decimals in text.
6. **Math inside Strings**: Calculations on the fly.
7. **Escape Characters**: Handling special symbols (Newlines, Tabs).
8. **Case Conversion Methods**: `upper()`, `lower()`, `title()`, `capitalize()`.
9. **Cleaning Methods**: `strip()`, `lstrip()`, `rstrip()`.
10. **Search & Replace**: `find()`, `count()`, `replace()`.
11. **Splitting & Joining**: `split()`, `join()`.
12. **Validation Methods**: `isdigit()`, `isalpha()`, `isalnum()`.

---

### **1. String Concatenation (`+`)**

We cannot "add" strings like numbers, but we can glue them together. This is called concatenation.

```python
# Sample Code
first_part = "Data"
second_part = "Science"
full_word = first_part + " " + second_part
print(full_word)

```

```python
# Practice: Create variables for 'First Name' and 'Last Name'.
# Create a variable 'Full Name' by combining them with a space in between.
# Print the result.

```

---

### **2. String Repetition (`*`)**

You can use the multiplication operator `*` on a string to repeat it. This is useful for creating visual separators in reports.

```python
# Sample Code
separator = "=" * 20
print(separator)
print("SECTION 1")
print(separator)

```

```python
# Practice: Create a variable containing a hyphen "-".
# Print it 50 times to create a line.

```

---

### **3. Membership Operators (`in`, `not in`)**

These boolean operators check if a specific sequence of characters exists inside another string. They return `True` or `False`.

```python
# Sample Code
email = "user@gmail.com"
print("@" in email)      # Returns True
print(".org" in email)   # Returns False

```

```python
# Practice: Define a variable 'sentence' with the text "The quick brown fox".
# Check if the word "fox" is in the sentence.
# Check if the word "dog" is NOT in the sentence.

```

---

### **4. The F-String (Formatting)**

F-Strings (formatted string literals) allow you to embed variables directly into strings. You simply put an `f` before the quotes and wrap variables in `{}`.

```python
# Sample Code
name = "Alice"
role = "Analyst"
intro = f"Employee {name} is a {role}."
print(intro)

```

```python
# Practice: Create variables 'item' (e.g., "Laptop") and 'qty' (e.g., 5).
# Use an f-string to print: "We have 5 units of Laptop in stock."

```

---

### **5. Number Formatting (`:.2f`)**

In Data Science, you often deal with long decimal numbers. You can control how many decimal places show using `:.nf` inside the curly braces.

```python
# Sample Code
pi = 3.1415926535
print(f"Pi rounded is {pi:.2f}")

```

```python
# Practice: Create a variable 'cost' = 19.99 and 'tax' = 0.08.
# Print the total (cost * tax) formatted to exactly 2 decimal places.

```

---

### **6. Math inside Strings**

You can perform Python arithmetic directly inside the curly braces `{}` of an f-string.

```python
# Sample Code
a = 10
b = 5
print(f"The sum of {a} and {b} is {a + b}")

```

```python
# Practice: Print a string that calculates the area of a square (side=4) directly inside the print statement.
# Output should look like: "The area of a square with side 4 is 16"

```

---

### **7. Escape Characters**

Some characters are "illegal" or invisible. We use a backslash `\` to escape them.

* `\n`: New Line
* `\t`: Tab (indentation)
* `\"`: Double quote (inside a double-quoted string)

```python
# Sample Code
print("Column1\tColumn2\tColumn3") # Tab separated
print("Line 1\nLine 2")            # New Line
print("He said, \"Python is easy\"") # Quotes inside quotes

```

```python
# Practice: Print a shopping list where every item is on a new line using a single print() statement.

```

---

### **8. Case Conversion Methods**

Python has built-in methods to change the capitalization of text.

* `upper()`: ALL CAPS
* `lower()`: all lowercase
* `title()`: Title Case
* `capitalize()`: First letter only
* `swapcase()`: Inverts case

```python
# Sample Code
text = "pyTHon proGRAMming"
print(text.upper())
print(text.title())

```

```python
# Practice: Create a variable with mixed case text: "dAtA sCiEnCe".
# Print it in all lower case.
# Print it in Title Case.

```

---

### **9. Cleaning Methods (Stripping)**

Data often comes with extra spaces at the start or end. These methods remove them.

* `strip()`: Removes spaces from both ends.
* `lstrip()`: Removes from left.
* `rstrip()`: Removes from right.

```python
# Sample Code
messy_data = "   Result: 45   "
clean_data = messy_data.strip()
print(f"|{messy_data}|")
print(f"|{clean_data}|")

```

```python
# Practice: Create a variable with extra spaces around it: "  admin  ".
# Clean the spaces and print the result showing it is clean.

```

---

### **10. Search & Replace**

* `replace(old, new)`: Swaps text.
* `count(value)`: Counts occurrences.
* `find(value)`: Returns the index position of the first occurrence (or -1 if not found).

```python
# Sample Code
txt = "I like apples, apples are red."
print(txt.replace("apples", "oranges"))
print(txt.count("apples"))

```

```python
# Practice: Variable text = "Error 404: Page not found".
# Replace "404" with "500".
# Find the index position of the word "Page".

```

---

### **11. Splitting & Joining**

These are critical for processing CSV or sentence data.

* `split(separator)`: Breaks a string into a **List**.
* `join(iterable)`: Joins a List into a **String**.

```python
# Sample Code
# Split
csv_line = "John,Doe,25,Engineer"
data_list = csv_line.split(",")
print(data_list)

# Join
words = ["Python", "is", "fun"]
sentence = " ".join(words)
print(sentence)

```

```python
# Practice: Create a string "apple#banana#cherry".
# Split it into a list using the "#" separator.
# Print the list.

```

---

### **12. Validation Methods**

These check the content of the string and return `True` or `False`.

* `isdigit()`: Only numbers?
* `isalpha()`: Only letters?
* `isalnum()`: Only letters and numbers (no special chars)?

```python
# Sample Code
print("12345".isdigit()) # True
print("123a".isdigit())  # False
print("Python".isalpha()) # True

```

```python
# Practice: Ask the user to input their age using input().
# Check if what they entered is a digit using .isdigit() and print the True/False result.

```

---
