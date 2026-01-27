
# **Lab Sheet: Python Functions**


### **Sub-Topics for Python Functions**

---


### **Topics Covered**

1. **Defining and Calling Functions**
2. **Parameters vs. Arguments**
3. **Arbitrary Arguments (*args)**
4. **Keyword Arguments (key=value)**
5. **Default Parameters**
6. **Return Values**
7. **Recursion**
8. **Lambda Functions**

---

### **1. Defining and Calling Functions**

**Cell Type: Markdown**

> **Concept:**
> * A **function** is a block of code which only runs when it is called.
> * You can pass data, known as parameters, into a function.
> * A function can return data as a result.
> * **Creating:** Use the `def` keyword.
> * **Calling:** Use the function name followed by parenthesis `()`.
> 
> 

**Cell Type: Code**

```python
# Define the function
def my_function():
  print("Hello from a function")

# Call the function
my_function()

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Define a function called 'greet_class'.
# 2. Inside the function, print "Welcome to Python Data Science".
# 3. Call the function.
# Write your code below:



```

---

### **2. Parameters and Arguments**

**Cell Type: Markdown**

> **Concept:**
> * **Information** can be passed into functions as arguments.
> * Arguments are specified after the function name, inside the parentheses. You can add as many arguments as you want, separated by a comma.
> * **Parameter:** The variable listed inside the parentheses in the function definition.
> * **Argument:** The value that is sent to the function when it is called.
> 
> 

**Cell Type: Code**

```python
# Function with one parameter (fname)
def my_function(fname):
  print(fname + " Refsnes")

# Calling with arguments
my_function("Emil")
my_function("Tobias")
my_function("Linus")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a function 'square_number' that takes one parameter 'num'.
# 2. Inside, print the square of that number (num * num).
# 3. Call the function with the argument 5.
# Write your code below:



```

---

### **3. Arbitrary Arguments (`*args`)**

**Cell Type: Markdown**

> **Concept:**
> * If you do not know how many arguments that will be passed into your function, add a `*` before the parameter name in the function definition.
> * This way the function will receive a **tuple** of arguments, and can access the items accordingly.
> 
> 

**Cell Type: Code**

```python
# The function receives a tuple of arguments
def my_function(*kids):
  print("The youngest child is " + kids[2])

my_function("Emil", "Tobias", "Linus")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a function 'sum_all' that takes *numbers as an argument.
# 2. Print the first number and the last number from the tuple passed.
# 3. Call it with inputs: 10, 20, 30, 40, 50.
# Write your code below:



```

---

### **4. Keyword Arguments (`key=value`)**

**Cell Type: Markdown**

> **Concept:**
> * You can also send arguments with the `key = value` syntax.
> * This way the order of the arguments does not matter.
> 
> 

**Cell Type: Code**

```python
def my_function(child3, child2, child1):
  print("The youngest child is " + child3)

# Order doesn't matter here
my_function(child1 = "Emil", child2 = "Tobias", child3 = "Linus")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Define a function 'describe_pet' with parameters 'animal_type' and 'pet_name'.
# 2. Print "I have a {animal_type} named {pet_name}".
# 3. Call it using keywords, passing pet_name="Harry" first, then animal_type="Hamster".
# Write your code below:



```

---

### **5. Default Parameter Value**

**Cell Type: Markdown**

> **Concept:**
> * If we call the function without argument, it uses the **default value**.
> * Defined using assignment `=` in the parameter list.
> 
> 

**Cell Type: Code**

```python
def my_function(country = "Norway"):
  print("I am from " + country)

my_function("Sweden")
my_function("India")
my_function() # Uses default "Norway"

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Define a function 'power' that takes a number 'base' and an 'exponent' with a default value of 2.
# 2. Print base ** exponent.
# 3. Call it once with (3, 3) and once with just (5) to use the default.
# Write your code below:



```

---

### **6. Return Values**

**Cell Type: Markdown**

> **Concept:**
> * To let a function return a value, use the `return` statement.
> * This allows you to store the result in a variable or use it in another calculation.
> 
> 

**Cell Type: Code**

```python
def my_function(x):
  return 5 * x

print(my_function(3))
print(my_function(5))

# Storing result
result = my_function(9)
print("Result is:", result)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Define a function 'add_five' that takes a number 'x'.
# 2. Return x + 5.
# 3. Call the function with 10, store the result in a variable 'final', and print 'final'.
# Write your code below:



```

---

### **7. Recursion**

**Cell Type: Markdown**

> **Concept:**
> * Python accepts function recursion, which means a defined function can **call itself**.
> * This is often used for mathematical problems (like Factorials or Fibonacci sequences).
> * **Warning:** You must have a condition to stop the recursion (base case), otherwise it will run forever (infinite recursion).
> 
> 

**Cell Type: Code**

```python
# Calculate Factorial (e.g., 3! = 3 * 2 * 1 = 6)
def tri_recursion(k):
  if(k > 0):
    result = k + tri_recursion(k - 1)
    print(result)
  else:
    result = 0
  return result

print("\n\nRecursion Example Results")
tri_recursion(6)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# (Simpler Example) Define a function 'countdown(n)'.
# 1. If n <= 0, print "Blastoff!".
# 2. Else, print n, then call countdown(n-1).
# 3. Call countdown(3).
# Write your code below:



```

---

### **8. Lambda Functions**

**Cell Type: Markdown**

> **Concept:**
> * A **lambda** function is a small anonymous function.
> * It can take any number of arguments, but can only have **one expression**.
> * **Syntax:** `lambda arguments : expression`
> * These are very commonly used in Data Science (e.g., inside Pandas `apply()` methods).
> 
> 

**Cell Type: Code**

```python
# Standard function
def add(a):
    return a + 10

# Lambda equivalent
x = lambda a : a + 10

print(x(5))

# Lambda with multiple arguments
y = lambda a, b : a * b
print(y(5, 6))

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a lambda function named 'cube' that takes one argument 'a' and returns a * a * a.
# 2. Print the result of cube(3).
# Write your code below:



```