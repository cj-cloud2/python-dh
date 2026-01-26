# **Lab Sheet: Python Conditions and Loops**

### **Topics Covered**

1. **Logical Conditions & If Statements**
2. **Indentation & Scope**
3. **Elif and Else**
4. **Short Hand If & Ternary Operators**
5. **Logical Operators (And, Or, Not)**
6. **Nested If & Pass Statement**
7. **The While Loop**
8. **Break & Continue (While Loop)**
9. **Else in While Loop**
10. **The For Loop (Lists & Strings)**
11. **Break & Continue (For Loop)**
12. **The Range() Function**
13. **Else in For Loop**
14. **Nested Loops**

---

### **1. Logical Conditions & If Statements**

**Cell Type: Markdown**

> **Concept:** Python supports standard logical conditions from mathematics:
> * Equals: `a == b`
> * Not Equals: `a != b`
> * Less than: `a < b`
> * Greater than: `a > b`
> 
> 
> An `if` statement allows you to execute code *only* if a condition is true.

**Cell Type: Code**

```python
a = 33
b = 200

if b > a:
  print("b is greater than a")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Define two variables: x = 50, y = 100.
# Write an if statement to print "y is larger" if y is greater than x.
# Write your code below:



```

---

### **2. Indentation & Scope**

**Cell Type: Markdown**

> **Concept:** Python relies on **indentation** (whitespace at the start of a line) to define scope. Unlike other languages that use curly brackets `{}`.
> * **Error:** If you skip indentation inside an `if` statement, Python will raise an error.
> 
> 

**Cell Type: Code**

```python
a = 33
b = 200

if b > a:
  print("b is greater than a") # Correct indentation

# if b > a:
# print("b is greater than a") # This would raise an error

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Write a valid if statement checking if 5 > 2.
# Ensure you indent the print statement correctly.
# Write your code below:



```

---

### **3. Elif and Else**

**Cell Type: Markdown**

> **Concept:**
> * **`elif`**: "Else If" - tries this condition if the previous ones were not true.
> * **`else`**: Catches anything not caught by preceding conditions.
> 
> 

**Cell Type: Code**

```python
a = 200
b = 33

if b > a:
  print("b is greater than a")
elif a == b:
  print("a and b are equal")
else:
  print("a is greater than b")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: score = 75
# Write a chain:
# - If score > 90, print "A"
# - Elif score > 70, print "B"
# - Else, print "C"
# Write your code below:



```

---

### **4. Short Hand If & Ternary Operators**

**Cell Type: Markdown**

> **Concept:**
> * **Short Hand If:** Put the statement on the same line if there is only one.
> * **Ternary Operator (Short Hand If...Else):** `print("A") if a > b else print("B")`.
> 
> 

**Cell Type: Code**

```python
a = 2
b = 330

# Short Hand If
if a < b: print("a is smaller")

# Ternary Operator (One line If-Else)
print("A") if a > b else print("B")

# Multiple Else on one line
print("A") if a > b else print("=") if a == b else print("B")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: age = 18
# Use a one-line ternary operator to print "Adult" if age >= 18 else "Minor".
# Write your code below:



```

---

### **5. Logical Operators (And, Or, Not)**

**Cell Type: Markdown**

> **Concept:** Used to combine conditional statements.
> * **`and`**: Returns True if **both** statements are true.
> * **`or`**: Returns True if **one** of the statements is true.
> * **`not`**: Reverses the result (returns False if the result is true).
> 
> 

**Cell Type: Code**

```python
a = 200
b = 33
c = 500

# AND
if a > b and c > a:
  print("Both conditions are True")

# OR
if a > b or a > c:
  print("At least one is True")

# NOT
if not a > c:
  print("a is NOT greater than c")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: x = 10, y = 20, z = 30
# Write an if statement using 'and' to check if x is less than y AND y is less than z.
# Write your code below:



```

---

### **6. Nested If & Pass Statement**

**Cell Type: Markdown**

> **Concept:**
> * **Nested If:** You can have `if` statements inside `if` statements.
> * **Pass:** `if` statements cannot be empty. Use `pass` as a placeholder to avoid errors.
> 
> 

**Cell Type: Code**

```python
x = 41

if x > 10:
  print("Above ten,")
  if x > 20:
    print("and also above 20!")
  else:
    print("but not above 20.")

# Pass statement
if x > 50:
  pass

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: num = 15
# Write a nested if:
# 1. Check if num is odd (num % 2 != 0).
# 2. Inside that, check if num > 10.
# Write your code below:



```

---

### **7. The While Loop**

**Cell Type: Markdown**

> **Concept:** The `while` loop executes a set of statements as long as a condition is true.
> * **Important:** You must manually increment the indexing variable (e.g., `i += 1`), otherwise the loop will run forever.
> 
> 

**Cell Type: Code**

```python
i = 1
while i < 6:
  print(i)
  i += 1

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Initialize count = 0.
# Write a while loop that prints "Running..." as long as count < 3.
# Increment count by 1 in each iteration.
# Write your code below:



```

---

### **8. Break & Continue (While Loop)**

**Cell Type: Markdown**

> **Concept:**
> * **`break`**: Stops the loop immediately, even if the condition is still true.
> * **`continue`**: Stops the *current* iteration and jumps to the next one.
> 
> 

**Cell Type: Code**

```python
# Break Example
i = 1
while i < 6:
  print(i)
  if i == 3:
    break
  i += 1

# Continue Example
i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a while loop from i = 1 to 10.
# Use 'break' to stop the loop when i equals 5.
# Write your code below:



```

---

### **9. Else in While Loop**

**Cell Type: Markdown**

> **Concept:** You can add an `else` block to a while loop. It runs **once** when the condition becomes false.

**Cell Type: Code**

```python
i = 1
while i < 6:
  print(i)
  i += 1
else:
  print("i is no longer less than 6")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Write a while loop that prints numbers 1 to 3.
# Add an else block that prints "Done!" when finished.
# Write your code below:



```

---

### **10. The For Loop (Lists & Strings)**

**Cell Type: Markdown**

> **Concept:** A `for` loop iterates over a sequence (list, tuple, string, etc.).
> * No indexing variable needs to be set beforehand.
> * Even strings are iterable sequences of characters.
> 
> 

**Cell Type: Code**

```python
# Loop through a list
fruits = ["apple", "banana", "cherry"]
for x in fruits:
  print(x)

# Loop through a string
for x in "banana":
  print(x)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given list: colors = ["Red", "Green", "Blue"]
# Write a for loop to print each color.
# Write your code below:



```

---

### **11. Break & Continue (For Loop)**

**Cell Type: Markdown**

> **Concept:**
> * **`break`**: Exits the loop completely.
> * **`continue`**: Skips the rest of the current iteration and moves to the next item.
> 
> 

**Cell Type: Code**

```python
fruits = ["apple", "banana", "cherry"]

# Break before print
for x in fruits:
  if x == "banana":
    break
  print(x)

# Continue (Skip banana)
for x in fruits:
  if x == "banana":
    continue
  print(x)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Loop through numbers [10, 20, 30, 40].
# Skip the number 20 using continue.
# Write your code below:



```

---

### **12. The Range() Function**

**Cell Type: Markdown**

> **Concept:** Generates a sequence of numbers.
> * `range(6)`: 0 to 5 (6 is excluded).
> * `range(start, stop)`: e.g., `range(2, 6)`.
> * `range(start, stop, step)`: e.g., `range(2, 30, 3)`.
> 
> 

**Cell Type: Code**

```python
# Default (0 to 5)
for x in range(6):
  print(x)

# Start and Stop (2 to 5)
for x in range(2, 6):
  print(x)

# Step (Increment by 3)
for x in range(2, 30, 3):
  print(x)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Use range() to print even numbers from 0 to 10 (0, 2, 4, 6, 8, 10).
# Write your code below:



```

---

### **13. Else in For Loop**

**Cell Type: Markdown**

> **Concept:** The `else` block executes when the loop finishes **normally**.
> * **Important:** The `else` block is **NOT** executed if the loop is stopped by a `break`.
> 
> 

**Cell Type: Code**

```python
# Normal completion
for x in range(6):
  print(x)
else:
  print("Finally finished!")

# Broken loop (Else won't run)
for x in range(6):
  if x == 3: break
  print(x)
else:
  print("This won't print")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Write a for loop from 0 to 3.
# Add an else statement that prints "Loop Complete".
# Write your code below:



```

---

### **14. Nested Loops**

**Cell Type: Markdown**

> **Concept:** A loop inside a loop. The "inner loop" executes one complete cycle for **each** iteration of the "outer loop".

**Cell Type: Code**

```python
adj = ["red", "big", "tasty"]
fruits = ["apple", "banana", "cherry"]

for x in adj:
  for y in fruits:
    print(x, y)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given:
# sizes = ["Small", "Large"]
# types = ["Shirt", "Pants"]
# Write a nested loop to print every combination (e.g., Small Shirt, Small Pants...).
# Write your code below:



```