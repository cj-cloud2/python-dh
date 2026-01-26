### **Topics Covered in this Lab Sheet** (30 mins)

* Basic Syntax & Printing
* Python Indentation
* Comments
* Variables and Dynamic Typing
* Variable Naming Rules
* Multiple Assignment
* Data Types (int, float, complex)
* Numeric Operators (Arithmetic, Assignment, Comparison)
* Type Casting
* Input from User
* Random Numbers

---

### **1. Basic Syntax & Printing**

The `print()` function is used to output data to the console.

```python
# Sample Code
print("Hello, World!")

```

```python
# Practice: Use the print function to display your name or a welcome message below

```

---

### **2. Python Indentation**

In Python, indentation (spaces at the start of a line) defines a block of code. It is not just for readability; it is a structural requirement.

```python
# Sample Code
if 5 > 2:
    print("Five is greater than two!")

```

```python
# Practice: Correct the indentation below to make the code run
if 10 > 5:
print("Ten is larger!")

```

---

### **3. Comments**

Comments start with a `#`. Python ignores them. They are used to explain code or prevent execution during testing.

```python
# Sample Code
# This is a full line comment
print("Hello!") # This is an end-of-line comment

```

```python
# Practice: Add a comment above the print statement below explaining what it does
print("Python for Data Science")

```

---

### **4. Variables and Dynamic Typing**

Variables are containers for data. Python is dynamically typed, meaning a variable can change its data type simply by assigning a new value.

```python
# Sample Code
x = 5          # x is an integer
print(x)
x = "Data"     # x is now a string
print(x)
print(type(x))

```

```python
# Practice: Create a variable named 'city', assign it a value, then print its type

```

---

### **5. Variable Naming Rules**

Names must start with a letter or underscore, cannot start with a number, and are case-sensitive.

```python
# Sample Code
my_var = "Valid"
_my_var = "Valid"
myVar2 = "Valid"
# 2myvar = "Invalid" (Will cause error)

```

```python
# Practice: Create three valid variables using different naming styles (snake_case, camelCase)

```

---

### **6. Multiple Assignment**

Python allows you to assign values to multiple variables in one line.

```python
# Sample Code
x, y, z = "Orange", "Banana", "Cherry"
a = b = c = "Apple"
print(x, y, a)

```

```python
# Practice: Assign your first name, last name, and age to three variables in one line

```

---

### **7. Numeric Data Types**

Python supports Integers, Floats (decimals), and Complex numbers.

```python
# Sample Code
int_num = 10
float_num = 10.5
complex_num = 3 + 5j
print(type(int_num), type(float_num), type(complex_num))

```

```python
# Practice: Create a float variable and a large integer and print them both

```

---

### **8. Numeric Operators**

Operators allow you to perform calculations.

* **Arithmetic:** `+`, `-`, `*`, `/`, `%` (remainder), `**` (exponent), `//` (floor division)
* **Comparison:** `==`, `!=`, `>`, `<`, `>=`, `<=`

```python
# Sample Code
a = 10
b = 3
print(a + b)  # Addition
print(a ** b) # Power (10 to the power of 3)
print(a // b) # Floor division (gives 3)
print(a > b)  # Comparison (returns True)

```

```python
# Practice: Calculate the area of a circle (radius=7) using the exponent operator (area = 3.14 * r**2)

```

---

### **9. Type Casting**

You can convert variables from one type to another using `int()`, `float()`, and `str()`.

```python
# Sample Code
x = int(2.8)   # Result: 2
y = float("3") # Result: 3.0
z = str(10)    # Result: "10"
print(x, y, z)

```

```python
# Practice: Convert the string "100" to an integer and add 50 to it

```

---

### **10. Accepting Input**

The `input()` function allows users to enter data. Note that `input()` always returns a **string**.

```python
# Sample Code
name = input("Enter your name: ")
age = int(input("Enter your age: ")) # Casting input to int
print(f"Hello {name}, you are {age} years old.")

```

```python
# Practice: Ask the user for two numbers, calculate their sum, and print the result

```

---

### **11. Random Numbers**

Python has a built-in module called `random` to generate random numbers.

```python
# Sample Code
import random
print(random.randrange(1, 100)) # Generates a number between 1 and 99

```

```python
# Practice: Generate a random number between 0 and 10 and print it

```