# **Lab Sheet: Python Lists**

### **Topics Covered**

1. Creating Lists & List Constructor
2. List Characteristics (Ordered, Changeable, Duplicates)
3. List Length & Data Types
4. Accessing Items (Indexing & Slicing)
5. Checking Existence
6. Changing Items (Single & Range)
7. Adding Items (Append, Insert, Extend)
8. Removing Items (Remove, Pop, Del, Clear)
9. Looping Through Lists
10. List Comprehension
11. Sorting & Reversing
12. Copying Lists
13. Joining Lists
14. Additional Methods: Count & Index

---

### **1. Creating Lists**

**Cell Type: Markdown**

> **Concept:** Lists are created using square brackets. They are used to store multiple items in a single variable. You can also use the `list()` constructor to create a new list.

**Cell Type: Code**

```python
# Method 1: Square Brackets
mylist = ["apple", "banana", "cherry"]
print(mylist)

# Method 2: list() Constructor
mylist2 = list(("apple", "banana", "cherry"))
print(mylist2)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a list named 'ds_tools' containing "Python", "R", and "SQL" using square brackets.
# 2. Create the same list using the list() constructor.
# Write your code below:



```

---

### **2. List Characteristics**

**Cell Type: Markdown**

> **Concept:**
> * **Ordered:** Items have a defined order that will not change. New items are placed at the end.
> * **Changeable:** We can add, change, and remove items after creation.
> * **Allow Duplicates:** Since lists are indexed, they can have items with the same value.
> 
> 

**Cell Type: Code**

```python
# Lists allow duplicate values
mylist = ["apple", "banana", "cherry", "apple", "cherry"]
print(mylist)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a list with duplicate values representing dataset scores: [98, 55, 98, 76].
# Print the list.
# Write your code below:



```

---

### **3. List Length & Data Types**

**Cell Type: Markdown**

> **Concept:**
> * Use `len()` to determine how many items a list has.
> * List items can be of any data type (String, int, boolean), and a single list can contain different data types.
> * From Python's perspective, lists are objects with the data type `<class 'list'>`.
> 
> 

**Cell Type: Code**

```python
# Length
list1 = ["apple", "banana", "cherry"]
print(len(list1))

# Mixed Data Types
list2 = ["abc", 34, True, 40, "male"]
print(type(list2))

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a list containing your name (string), age (int), and is_student status (boolean).
# Print the length of this list and the type of the list.
# Write your code below:



```

---

### **4. Accessing Items (Indexing & Slicing)**

**Cell Type: Markdown**

> **Concept:**
> * **Indexing:** Access items by referring to the index number (starts at 0).
> * **Negative Indexing:** `-1` refers to the last item, `-2` the second last, etc.
> * **Slicing (Range):** Specify a start and end index `[start:end]`. The return value is a new list. Note that the item at the `end` index is **not** included.
> 
> 

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]

print(mylist[1])      # Second item
print(mylist[-1])     # Last item
print(mylist[2:5])    # From index 2 up to (but not including) 5
print(mylist[:4])     # From start to index 4 (not included)
print(mylist[2:])     # From index 2 to the end
print(mylist[-4:-1])  # Negative range

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given the list: data = [10, 20, 30, 40, 50, 60, 70]
# 1. Print the first item.
# 2. Print the last item using negative indexing.
# 3. Print the sub-list [30, 40, 50] using slicing.
# Write your code below:



```

---

### **5. Checking Item Exists**

**Cell Type: Markdown**

> **Concept:** To determine if a specified item is present in a list, use the `in` keyword.

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry"]
if "apple" in mylist:
  print("Yes, 'apple' is in the fruits list")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Check if "Python" exists in the list ["Java", "C++", "Python"].
# If yes, print "Found it!".
# Write your code below:



```

---

### **6. Changing Items**

**Cell Type: Markdown**

> **Concept:**
> * **Single Item:** Refer to the index number to change a specific value.
> * **Range of Items:** Define a list with new values and refer to the range of index numbers. If you insert more or fewer items than you replace, the list length will change.
> 
> 

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry", "orange", "kiwi", "mango"]

# Change single item
mylist[1] = "blackcurrant"

# Change range (replace 2 items with 2 items)
mylist[1:3] = ["blackcurrant", "watermelon"]

# Change range (replace 1 item with 2 items - insert occurs)
mylist[1:2] = ["blackcurrant", "watermelon"]

print(mylist)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: colors = ["red", "blue", "green"]
# 1. Change "blue" to "yellow".
# 2. Change "green" to "purple" and "orange" using a slice assignment.
# Write your code below:



```

---

### **7. Adding Items**

**Cell Type: Markdown**

> **Concept:**
> * **`append()`**: Adds an item to the end of the list.
> * **`insert()`**: Adds an item at a specified index.
> * **`extend()`**: Appends elements from another list (or any iterable like a tuple) to the current list.
> 
> 

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry"]

# Append
mylist.append("orange")

# Insert at index 1
mylist.insert(1, "orange")

# Extend with another list
tropical = ["mango", "pineapple", "papaya"]
mylist.extend(tropical)

print(mylist)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create an empty list called 'results'.
# 2. Append the number 95.
# 3. Insert the number 80 at the beginning (index 0).
# 4. Extend 'results' with the list [88, 92].
# Write your code below:



```

---

### **8. Removing Items**

**Cell Type: Markdown**

> **Concept:**
> * **`remove()`**: Removes the specified *value*. (Removes first occurrence only).
> * **`pop()`**: Removes the specified *index* (or the last item if no index is specified).
> * **`del`**: Keyword to remove a specified index or delete the list entirely.
> * **`clear()`**: Empties the list content but the list remains.
> 
> 

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry", "banana", "kiwi"]

mylist.remove("banana") # Removes first 'banana'
mylist.pop(1)           # Removes item at index 1
mylist.pop()            # Removes last item
del mylist[0]           # Deletes item at index 0
mylist.clear()          # Empties the list

print(mylist)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: tasks = ["Train", "Test", "Validate", "Deploy"]
# 1. Remove "Test" by value.
# 2. Pop the last item ("Deploy").
# 3. Clear the remaining items.
# Write your code below:



```

---

### **9. Looping Through Lists**

**Cell Type: Markdown**

> **Concept:**
> * **For Loop:** Iterate directly through list items.
> * **Index Loop:** Use `range()` and `len()` to iterate through index numbers.
> 
> 

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry"]

# Direct loop
for x in mylist:
  print(x)

# Index loop
for i in range(len(mylist)):
  print(mylist[i])

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Iterate through the list [10, 20, 30] and print each number multiplied by 2.
# Use whichever loop method you prefer.
# Write your code below:



```

---

### **10. List Comprehension**

**Cell Type: Markdown**

> **Concept:** List comprehension offers a shorter syntax to create a new list based on existing values.
> * **Syntax:** `newlist = [expression for item in iterable if condition == True]`
> * The condition is optional.
> * The expression is the outcome you can manipulate.
> 
> 

**Cell Type: Code**

```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]

# Only fruits with "a"
newlist = [x for x in fruits if "a" in x]
print(newlist)

# Set all to upper case
upperlist = [x.upper() for x in fruits]
print(upperlist)

# Manipulate outcome (Return orange instead of banana)
sublist = [x if x != "banana" else "orange" for x in fruits]
print(sublist)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given numbers = [1, 2, 3, 4, 5]
# Create a new list called 'squares' containing the square of each number (x*x).
# Write your code below:



```

---

### **11. Sorting Lists**

**Cell Type: Markdown**

> **Concept:**
> * **`sort()`**: Sorts alphanumerically, ascending by default.
> * **Descending:** Use `reverse = True`.
> * **Custom Sort:** Use `key = function`.
> * **Case Insensitive:** Use `key = str.lower`.
> * **`reverse()`**: Reverses the current order of elements (regardless of value).
> 
> 

**Cell Type: Code**

```python
# Sort Alphanumeric
mylist = ["orange", "mango", "kiwi", "pineapple", "banana"]
mylist.sort()
print(mylist)

# Sort Descending
mylist.sort(reverse = True)
print(mylist)

# Custom Key (Sort by closeness to 50)
def myfunc(n):
  return abs(n - 50)
numlist = [100, 50, 65, 82, 23]
numlist.sort(key = myfunc)
print(numlist)

# Case Insensitive
mylist = ["banana", "Orange", "Kiwi", "cherry"]
mylist.sort(key = str.lower)
print(mylist)

# Reverse Order
mylist.reverse()
print(mylist)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: values = [5, 1, 8, 3]
# 1. Sort the list in ascending order.
# 2. Reverse the list so it becomes descending.
# Write your code below:



```

---

### **12. Copying Lists**

**Cell Type: Markdown**

> **Concept:** You cannot copy by typing `list2 = list1` (this only references the memory).
> * **`copy()`**: Built-in method to create a shallow copy.
> * **`list()`**: Built-in constructor method to create a copy.
> * **Slice `[:]**`: Using the slice operator to create a copy.
> 
> 

**Cell Type: Code**

```python
mylist = ["apple", "banana", "cherry"]

# Method 1
newlist1 = mylist.copy()

# Method 2
newlist2 = list(mylist)

# Method 3
newlist3 = mylist[:]

print(newlist1)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a copy of the list [1, 2, 3] using the copy() method.
# Add a number to the copy and prove the original list is unchanged.
# Write your code below:



```

---

### **13. Joining Lists**

**Cell Type: Markdown**

> **Concept:**
> * **`+` Operator:** Easiest way to concatenate.
> * **Append in Loop:** Append items from list2 to list1 one by one.
> * **`extend()`**: Add elements from one list to another.
> 
> 

**Cell Type: Code**

```python
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

# Method 1
joined = list1 + list2
print(joined)

# Method 2 (Extend)
list1.extend(list2)
print(list1)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Join list A = ['x', 'y'] and B = ['z'] into a new list C using the + operator.
# Write your code below:



```

---

### **14. Additional Methods: Count and Index**

**Cell Type: Markdown**

> **Concept:**
> * **`count()`**: Returns the number of elements with the specified value.
> * **`index()`**: Returns the index of the **first** element with the specified value.
> 
> 

**Cell Type: Code**

```python
mylist = [1, 3, 7, 8, 7, 5, 4, 6, 8, 5]

# Count occurrences of 5
x = mylist.count(5)
print(x)

# Find index of the first occurrence of 8
y = mylist.index(8)
print(y)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: data = [10, 20, 10, 30, 10]
# 1. Count how many times 10 appears.
# 2. Find the index of 30.
# Write your code below:



```