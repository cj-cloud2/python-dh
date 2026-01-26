# **Lab Sheet: Python Dictionaries**

### **Topics Covered**

1. **Dictionary Creation & Characteristics**
2. **Accessing Items (Keys, Values, Items)**
3. **Checking Key Existence**
4. **Changing Dictionary Values**
5. **Adding Items**
6. **Removing Items**
7. **Looping Through Dictionaries**
8. **Copying Dictionaries**
9. **Nested Dictionaries**

---

### **1. Dictionary Creation & Characteristics**

**Cell Type: Markdown**

> **Concept:** Dictionaries are used to store data values in `key:value` pairs. They are written with **curly brackets** `{}`.
> * **Ordered:** Items have a defined order (as of Python 3.7+).
> * **Changeable:** You can add, change, or remove items.
> * **No Duplicates:** Duplicate keys are not allowed (the last one overwrites previous ones).
> * **Data Types:** Values can be any data type (String, int, boolean, list).
> 
> 

**Cell Type: Code**

```python
# Create a dictionary
mydict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
print(mydict)

# Duplicate keys overwrite existing values
dup_dict = {
  "brand": "Ford",
  "year": 1964,
  "year": 2020
}
print(dup_dict) # year will be 2020

# Check Length and Type
print(len(mydict))
print(type(mydict))

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Create a dictionary called 'employee' with keys: "name", "id", "salary".
# 2. Add a duplicate key "salary" with a different value to see what happens.
# 3. Print the dictionary and its length.
# Write your code below:



```

---

### **2. Accessing Items (Keys, Values, Items)**

**Cell Type: Markdown**

> **Concept:**
> * **Access by Key:** Use `dict["key"]` or `dict.get("key")`.
> * **`keys()`**: Returns a list containing the dictionary's keys.
> * **`values()`**: Returns a list of all the values in the dictionary.
> * **`items()`**: Returns each item in a dictionary as tuples in a list.
> * **View Object:** These methods return a "view". If you change the dictionary later, these lists update automatically.
> 
> 

**Cell Type: Code**

```python
car = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}

# Access Value
print(car["model"])

# Get Keys
x = car.keys()
print(x)

# Get Values
y = car.values()
print(y)

# Get Items (Key-Value pairs)
z = car.items()
print(z)

# Demonstrate View Update
car["color"] = "white"
print(x) # Keys list is automatically updated

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: data = {"A": 10, "B": 20}
# 1. Print the value of key "B".
# 2. Store the keys in a variable 'k' and print it.
# 3. Add a new key "C": 30 to the dictionary.
# 4. Print 'k' again to see the update.
# Write your code below:



```

---

### **3. Checking Key Existence**

**Cell Type: Markdown**

> **Concept:** Use the `in` keyword to determine if a specified key is present in a dictionary.

**Cell Type: Code**

```python
mydict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

if "model" in mydict:
  print("Yes, 'model' is one of the keys")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Check if "score" is a key in the dictionary {"name": "John", "score": 95}.
# If yes, print "Score found".
# Write your code below:



```

---

### **4. Changing Dictionary Values**

**Cell Type: Markdown**

> **Concept:**
> * **Direct Assignment:** Refer to the key name: `dict["key"] = new_value`.
> * **`update()`**: Updates the dictionary with items from a given argument (another dictionary or iterable).
> 
> 

**Cell Type: Code**

```python
mydict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

# Method 1: Direct Assignment
mydict["year"] = 2018

# Method 2: Update Method
mydict.update({"year": 2020})

print(mydict)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: profile = {"role": "intern", "status": "active"}
# 1. Change "role" to "developer" using direct assignment.
# 2. Change "status" to "inactive" using the update() method.
# Write your code below:



```

---

### **5. Adding Items**

**Cell Type: Markdown**

> **Concept:**
> * **New Key:** Use a new index key and assign a value: `dict["new_key"] = value`.
> * **`update()`**: If the key in the argument does not exist, it will be added.
> 
> 

**Cell Type: Code**

```python
mydict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

# Method 1: New Key Assignment
mydict["color"] = "red"

# Method 2: Update Method (Adding new key)
mydict.update({"transmission": "manual"})

print(mydict)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create an empty dictionary: settings = {}
# 1. Add "theme": "dark".
# 2. Add "notifications": True using update().
# Write your code below:



```

---

### **6. Removing Items**

**Cell Type: Markdown**

> **Concept:**
> * **`pop("key")`**: Removes the item with the specified key name.
> * **`popitem()`**: Removes the **last inserted** item.
> * **`del dict["key"]`**: Removes the item with the specified key name.
> * **`del dict`**: Deletes the dictionary completely.
> * **`clear()`**: Empties the dictionary (content removed, object remains).
> 
> 

**Cell Type: Code**

```python
mydict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964,
  "color": "red"
}

mydict.pop("model")      # Removes model
mydict.popitem()         # Removes color (last inserted)
del mydict["year"]       # Removes year
# mydict.clear()         # Would empty the dict
print(mydict)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: config = {"a": 1, "b": 2, "c": 3}
# 1. Remove "b" using pop.
# 2. Remove the last inserted item using popitem.
# 3. Clear the dictionary.
# Write your code below:



```

---

### **7. Looping Through Dictionaries**

**Cell Type: Markdown**

> **Concept:**
> * **Standard Loop:** Returns the **keys**.
> * **`values()`**: Loop through values.
> * **`items()`**: Loop through both keys and values.
> 
> 

**Cell Type: Code**

```python
mydict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

# Loop Keys
print("Keys:")
for x in mydict:
  print(x)

# Loop Values
print("\nValues:")
for x in mydict.values():
  print(x)

# Loop Key-Value Pairs
print("\nItems:")
for x, y in mydict.items():
  print(x, y)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Given: prices = {"apple": 0.50, "banana": 0.30}
# Loop through the dictionary and print statements like: "The price of apple is 0.5".
# Write your code below:



```

---

### **8. Copying Dictionaries**

**Cell Type: Markdown**

> **Concept:** You cannot copy by simple assignment (`dict2 = dict1`) because changes will reflect in both.
> * **`copy()`**: Built-in method to create a copy.
> * **`dict()`**: Constructor function to create a copy.
> 
> 

**Cell Type: Code**

```python
mydict = {
  "brand": "Ford",
  "model": "Mustang"
}

# Method 1
dict1 = mydict.copy()

# Method 2
dict2 = dict(mydict)

print(dict1)

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a dictionary original = {"x": 1}.
# Create a copy called copy_dict.
# Change original["x"] to 99.
# Print both dictionaries to prove copy_dict didn't change.
# Write your code below:



```

---

### **9. Nested Dictionaries**

**Cell Type: Markdown**

> **Concept:** A dictionary can contain other dictionaries.
> * **Access:** Use multiple brackets `dict["outer"]["inner"]`.
> * **Looping:** Loop through outer, then loop through inner logic if needed.
> 
> 

**Cell Type: Code**

```python
myfamily = {
  "child1" : { "name" : "Emma", "year" : 2004 },
  "child2" : { "name" : "Jack", "year" : 2007 }
}

# Accessing
print(myfamily["child2"]["name"])

# Looping
for x, obj in myfamily.items():
  print(x)
  for y in obj:
    print(y + ':', obj[y])

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Create a nested dictionary representing 2 students.
# students = {
#    "s1": {"name": "Alice", "grade": "A"},
#    "s2": {"name": "Bob", "grade": "B"}
# }
# Print Bob's grade.
# Write your code below:



```