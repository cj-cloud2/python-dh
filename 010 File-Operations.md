# **Lab Sheet: Python File Handling**


### **Sub-Topics for File Handling**

1. **Opening Files & Modes:** Understanding `open()` and modes (`r`, `w`, `a`, `x`).
2. **Reading Files:** Methods like `read()`, `readline()`, and `readlines()`.
3. **Writing to Files:** Writing strings vs. lists, and Overwriting (`w`) vs. Appending (`a`).
4. **The `with` Statement:** Best practices for automatically closing files.
5. **File Existence & Deletion:** Using the `os` module to check if files exist and delete them.
6. **Creating & Removing Directories:** Managing folders using `os`.

---



### **Topics Covered**

1. **Setup (Creating a Dummy File)**
2. **Opening & Reading Files**
3. **Reading Lines & Looping**
4. **Writing (Overwriting vs. Appending)**
5. **The `with` Statement (Context Managers)**
6. **Deleting Files & Directories**

---

### **Step 0: Setup (Create Sample Data)**

**Cell Type: Markdown**

> **Concept:** Before we can read a file, one must exist. Let's create a simple text file named `demofile.txt` using Python code so we have something to work with.

**Cell Type: Code**

```python
# Setup: Create a file named 'demofile.txt'
# We use 'w' mode to write content to it.
f = open("demofile.txt", "w")
f.write("Hello! Welcome to Python File Handling.\nThis is the second line.\nThis is the third line.")
f.close()

print("demofile.txt has been created successfully.")

```

---

### **1. Opening & Reading Files**

**Cell Type: Markdown**

> **Concept:**
> * **`open(filename, mode)`**: The key function.
> * **Modes:** `"r"` (Read - Default), `"w"` (Write), `"a"` (Append), `"x"` (Create).
> * **`read()`**: Reads the *entire* content of the file.
> * **`close()`**: You must always close the file to save changes and free up memory.
> 
> 

**Cell Type: Code**

```python
# Open the file in Read mode
f = open("demofile.txt", "r")

# Read the content
content = f.read()
print(content)

# Close the file
f.close()

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Open "demofile.txt" in read mode ("r").
# 2. Read the content and print it.
# 3. Close the file.
# Write your code below:



```

---

### **2. Reading Lines & Looping**

**Cell Type: Markdown**

> **Concept:**
> * **`read(n)`**: Reads only the first *n* characters.
> * **`readline()`**: Reads a single line. calling it twice reads the first two lines.
> * **Looping:** You can loop through the file object itself to read line by line (memory efficient).
> 
> 

**Cell Type: Code**

```python
f = open("demofile.txt", "r")

# Read first 5 characters
print(f.read(5))

# Read one line
print(f.readline())

# Loop through remaining lines
for x in f:
  print("Line:", x)

f.close()

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Open "demofile.txt".
# 2. Read only the first line using readline().
# 3. Print that line.
# 4. Close the file.
# Write your code below:



```

---

### **3. Writing (Overwriting vs. Appending)**

**Cell Type: Markdown**

> **Concept:**
> * **`"w"` (Write):** Overwrites the entire file. If the file doesn't exist, it creates it.
> * **`"a"` (Append):** Adds content to the end of the file. Does not delete existing content.
> 
> 

**Cell Type: Code**

```python
# 1. Append (Add to end)
f = open("demofile.txt", "a")
f.write("\nThis is a new line added via Append!")
f.close()

# 2. Write (Overwrite everything)
f = open("demofile.txt", "w")
f.write("I have deleted the old content and put this here instead.")
f.close()

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Open "demofile.txt" in Append mode ("a").
# 2. Write your name into the file.
# 3. Close the file.
# 4. Open it again in Read mode ("r") and print the content to verify.
# Write your code below:



```

---

### **4. The `with` Statement (Best Practice)**

**Cell Type: Markdown**

> **Concept:** Manually closing files with `f.close()` is risky (if an error occurs before that line, the file stays open).
> * **`with open(...) as f:`**: Automatically closes the file for you, even if the code crashes. This is the professional way to handle files.
> 
> 

**Cell Type: Code**

```python
# No need for f.close() here!
with open("demofile.txt", "r") as f:
    data = f.read()
    print(data)

# File is already closed here

```

**Cell Type: Code (Practice)**

```python
# Practice:
# Use the 'with' statement to open "demofile.txt" in write mode ("w").
# Write "Python Context Managers are cool!" into the file.
# (No need to close it manually).
# Write your code below:



```

---

### **5. Deleting Files & Directories**

**Cell Type: Markdown**

> **Concept:** Python cannot delete files directly; it needs the **OS** module.
> * **`os.remove()`**: Deletes a file.
> * **`os.path.exists()`**: Checks if a file exists (prevents errors before deleting).
> * **`os.rmdir()`**: Removes an *empty* directory.
> 
> 

**Cell Type: Code**

```python
import os

filename = "demofile.txt"

# Check if file exists before deleting
if os.path.exists(filename):
  os.remove(filename)
  print(f"{filename} deleted.")
else:
  print("The file does not exist.")

```

**Cell Type: Code (Practice)**

```python
# Practice:
# 1. Import the 'os' module.
# 2. Try to remove a file named "ghost_file.txt".
# 3. Use an IF check to ensure you don't get an error if it doesn't exist.
# Write your code below:



```