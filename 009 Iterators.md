# **Lab Sheet: Python Iterators**


### **Sub-Topics for Python Iterators**

1. **Iterables vs. Iterators:** Understanding the difference (Lists/Tuples vs. the Iterator object).
2. **The Iterator Protocol:** The `__iter__()` and `__next__()` methods.
3. **Manual Iteration:** Using the `iter()` and `next()` built-in functions.
4. **StopIteration Exception:** How Python signals the end of a sequence.
5. **Under the Hood of For Loops:** How a `for` loop actually uses iterators and handles errors.

---

### **Topics Covered**

1. **Iterables vs. Iterators**
2. **Manual Iteration (iter() and next())**
3. **StopIteration Exception**
4. **Understanding the For Loop (The "Under the Hood" Logic)**
5. **Creating Custom Iterator Classes**
6. **Infinite Iterators**

---

### **1. Iterables vs. Iterators**

**Cell Type: Markdown**

> **Concept:**
> * **Iterable:** An object capable of returning its members one at a time (e.g., Lists, Tuples, Strings). You can loop over them, but they don't keep track of "where you are."
> * **Iterator:** An object representing a stream of data. It remembers its state (current position) and knows how to get the *next* value.
> * **`iter()`**: Converts an iterable into an iterator.
> * **`next()`**: Retrieves the next item from an iterator.
> 
> 

**Cell Type: Code**

```python
# 1. An Iterable (List)
mytuple = ("apple", "banana", "cherry")

# 2. Convert to Iterator
myit = iter(mytuple)

# 3. Get values one by one
print(next(myit)) # apple
print(next(myit)) # banana
print(next(myit)) # cherry

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a list called 'nums' with values [10, 20, 30].
# 2. Create an iterator from it called 'num_iter' using iter().
# 3. Print the first two values using next().
# Write your code below:



```

---

### **2. StopIteration Exception**

**Cell Type: Markdown**

> **Concept:** When an iterator runs out of items, it raises a `StopIteration` exception. This is not an error in the traditional sense; it's a signal to Python that "there is no more data."

**Cell Type: Code**

```python
mytuple = ("A", "B")
myit = iter(mytuple)

print(next(myit)) # A
print(next(myit)) # B

# This next line would crash the program if uncommented:
# print(next(myit)) # Raises StopIteration

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a string "Hi".
# 2. Create an iterator from it.
# 3. Call next() 3 times. Observe the error on the 3rd time (You can leave the error or comment it out).
# Write your code below:



```

---

### **3. Under the Hood of For Loops**

**Cell Type: Markdown**

> **Concept:** A `for` loop is actually syntactic sugar. It does the following automatically:
> 1. Calls `iter()` on your object.
> 2. Calls `next()` repeatedly.
> 3. Catches the `StopIteration` exception to stop the loop gracefully.
> 
> 

**Cell Type: Code**

```python
# What a FOR loop actually does:
my_list = [1, 2, 3]

# Manual implementation
iterator_obj = iter(my_list)

while True:
    try:
        # Get next item
        item = next(iterator_obj)
        print(item)
    except StopIteration:
        # Stop loop when empty
        break

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Manually simulate a loop over the string "Python" using the while True / try-except structure above.
# Write your code below:



```

---
