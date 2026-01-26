# **Lab Sheet: Python Tuples and Sets**

### **Topics Covered**

1. Tuple Creation & Characteristics
2. Tuple Length & Single Item Rule
3. Accessing Tuple Items (Indexing & Slicing)
4. Checking Item Existence in Tuples
5. Updating Tuples (The Workaround)
6. Unpacking Tuples
7. Looping Through Tuples
8. Joining & Multiplying Tuples
9. Set Creation & Characteristics
10. Accessing Sets & Checking Values
11. Adding Items to Sets
12. Removing Items from Sets
13. Set Operations (Union, Pipe, Update)

---

### **1. Tuple Creation & Characteristics**

**Cell Type: Markdown**

> **Concept:** Tuples are used to store multiple items in a single variable. They are written with **round brackets** `()`.
> * **Ordered:** Items have a defined order that will not change.
> * **Unchangeable (Immutable):** You cannot add, change, or remove items after creation.
> * **Allow Duplicates:** Because they are indexed, duplicates are allowed.
> 
> 

**Cell Type: Code**

```python
# Create a Tuple
mytuple = ("apple", "banana", "cherry", "apple") # Duplicates allowed
print(mytuple)

# Check data type
print(type(mytuple))

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a tuple named 'my_data' containing "Data", "Science", "Python".
# 2. Print the tuple.
# Write your code below:



```

---

### **2. Tuple Length & Single Item Rule**

**Cell Type: Markdown**

> **Concept:**
> * Use `len()` to find the number of items.
> * **Important:** To create a tuple with only **one** item, you must add a **comma** after the item. Otherwise, Python treats it as a string or number.
> 
> 

**Cell Type: Code**

```python
# Tuple Length
mytuple = ("apple", "banana", "cherry")
print(len(mytuple))

# One item tuple (Note the comma)
one_item = ("apple",)
print(type(one_item))

# NOT a tuple (Missing comma)
not_tuple = ("apple")
print(type(not_tuple))

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a variable 't1' with a single item "Test" and NO comma. Check its type.
# 2. Create a variable 't2' with a single item "Test" AND a comma. Check its type.
# Write your code below:



```

---

### **3. Accessing Tuple Items (Indexing & Slicing)**

**Cell Type: Markdown**

> **Concept:**
> * **Index:** Access items using `[]`. Index starts at `0`.
> * **Negative Index:** `-1` refers to the last item.
> * **Range:** `[start:end]` creates a new tuple. The item at `end` is **not** included.
> 
> 

**Cell Type: Code**

```python
mytuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")

print(mytuple[1])      # Second item
print(mytuple[-1])     # Last item
print(mytuple[2:5])    # From index 2 up to (not including) 5
print(mytuple[:4])     # From start to index 4 (not included)
print(mytuple[-4:-1])  # Negative range

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: data = (10, 20, 30, 40, 50)
# 1. Print the first item.
# 2. Print the last item using negative indexing.
# 3. Print the sub-tuple (20, 30, 40).
# Write your code below:



```

---

### **4. Checking Item Existence in Tuples**

**Cell Type: Markdown**

> **Concept:** Use the `in` keyword to determine if a specific item exists in a tuple.

**Cell Type: Code**

```python
mytuple = ("apple", "banana", "cherry")
if "apple" in mytuple:
  print("Yes, 'apple' is in the fruits tuple")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Check if "Python" is in the tuple ("Java", "C++", "Python").
# If yes, print "Found it".
# Write your code below:



```

---

### **5. Updating Tuples (The Workaround)**

**Cell Type: Markdown**

> **Concept:** Tuples are immutable (cannot be changed). To modify one, you must:
> 1. Convert the tuple to a **list**.
> 2. Change/Add items in the list.
> 3. Convert the list back to a **tuple**.
> 
> 

**Cell Type: Code**

```python
x = ("apple", "banana", "cherry")

# 1. Convert to list
y = list(x)

# 2. Modify list (Change item and Append item)
y[1] = "kiwi"
y.append("orange")

# 3. Convert back to tuple
x = tuple(y)
print(x)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: nums = (1, 2, 3)
# Use the workaround to change the value 2 to 200.
# Write your code below:



```

---

### **6. Unpacking Tuples**

**Cell Type: Markdown**

> **Concept:** "Packing" is assigning values to a tuple. "Unpacking" is extracting values back into variables.
> * **Asterisk `*`:** If the number of variables is less than the number of values, use `*` to collect the remaining values as a list.
> 
> 

**Cell Type: Code**

```python
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")

# Standard Unpacking (Variables match count)
(f1, f2, f3, f4, f5) = fruits

# Using Asterisk (Variables < count)
(green, yellow, *red) = fruits

print(green)
print(yellow)
print(red) # This becomes a list of the remaining items

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: colors = ("red", "green", "blue", "yellow", "purple")
# Unpack "red" into a variable 'primary', "green" into 'secondary',
# and the rest into 'others'.
# Write your code below:



```

---

### **7. Looping Through Tuples**

**Cell Type: Markdown**

> **Concept:**
> * **For Loop:** Iterate through items directly.
> * **Index Loop:** Use `range(len())` to iterate via index numbers.
> * **While Loop:** Use a counter variable and `len()`.
> 
> 

**Cell Type: Code**

```python
mytuple = ("apple", "banana", "cherry")

# Direct Loop
for x in mytuple:
  print(x)

# Index Loop
for i in range(len(mytuple)):
  print(f"Index {i}: {mytuple[i]}")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a tuple (10, 20, 30).
# Loop through it and print each number divided by 2.
# Write your code below:



```

---

### **8. Joining & Multiplying Tuples**

**Cell Type: Markdown**

> **Concept:**
> * **Join:** Use the `+` operator to combine two tuples.
> * **Multiply:** Use the `*` operator to repeat the content of a tuple.
> 
> 

**Cell Type: Code**

```python
tuple1 = ("a", "b")
tuple2 = (1, 2)

# Join
tuple3 = tuple1 + tuple2
print(tuple3)

# Multiply
mytuple = tuple1 * 2
print(mytuple)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a tuple t1 = ("Hi",)
# Create a new tuple t2 that repeats t1 5 times.
# Write your code below:



```

---

### **9. Set Creation & Characteristics**

**Cell Type: Markdown**

> **Concept:** Sets are written with **curly brackets** `{}`.
> * **Unordered:** Items have no defined order (cannot refer by index).
> * **Unchangeable:** Cannot change items, but can add/remove.
> * **No Duplicates:** Duplicate values are ignored.
> * **Note:** `True` and `1` are considered the same. `False` and `0` are considered the same.
> 
> 

**Cell Type: Code**

```python
# No duplicates allowed
myset = {"apple", "banana", "cherry", "apple"}
print(myset)

# True and 1 treated as duplicates
bool_set = {"apple", True, 1, 2}
print(bool_set)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a set with values {10, 20, 10, 30}.
# Print it to see how Python handles the duplicate '10'.
# Write your code below:



```

---

### **10. Accessing Sets & Checking Values**

**Cell Type: Markdown**

> **Concept:** You cannot access items by index/key.
> * **Access:** Loop through the set.
> * **Check:** Use the `in` keyword to see if a value is present.
> 
> 

**Cell Type: Code**

```python
myset = {"apple", "banana", "cherry"}

# Check existence
print("banana" in myset)

# Loop access
for x in myset:
  print(x)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Check if "Data" is present in the set {"Data", "Science"}.
# Write your code below:



```

---

### **11. Adding Items to Sets**

**Cell Type: Markdown**

> **Concept:**
> * **`add()`**: Adds a single item.
> * **`update()`**: Adds items from another set (or list/tuple).
> 
> 

**Cell Type: Code**

```python
myset = {"apple", "banana"}

# Add single item
myset.add("orange")

# Add multiple items (from a list or set)
myset.update(["mango", "grape"])

print(myset)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a set: nums = {1, 2}
# Add the number 3.
# Add the list [4, 5] using update.
# Write your code below:



```

---

### **12. Removing Items from Sets**

**Cell Type: Markdown**

> **Concept:**
> * **`remove()`**: Removes item. Raises error if item does not exist.
> * **`discard()`**: Removes item. **No error** if item does not exist.
> * **`pop()`**: Removes a **random** item.
> * **`clear()`**: Empties the set.
> 
> 

**Cell Type: Code**

```python
myset = {"apple", "banana", "cherry"}

myset.remove("banana") # Specific remove
myset.discard("kiwi")  # No error even if kiwi doesn't exist
x = myset.pop()        # Removes random item

print(myset)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: s = {"a", "b", "c"}
# Use discard to remove "z" (ensure no error).
# Use pop to remove one item.
# Write your code below:



```

---

### **13. Set Operations (Union, Pipe, Update)**

**Cell Type: Markdown**

> **Concept:**
> * **`union()`**: Returns a **new** set with all items from both sets. (Can join Set + List).
> * **`|` Operator**: Same as union, but only works Set + Set.
> * **`update()`**: Inserts items from one set into the **original** set (modifies it).
> 
> 

**Cell Type: Code**

```python
set1 = {"a", "b"}
set2 = {1, 2}

# Union (New Set)
set3 = set1.union(set2)
print(set3)

# Pipe Operator (New Set)
set4 = set1 | set2
print(set4)

# Update (Modifies set1)
set1.update(set2)
print(set1)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create set A = {10, 20} and B = {30, 40}.
# Create a new set C using the union of A and B.
# Write your code below:



```