# **Lab: Mastering Jupyter Notebook**

**Goal:** Become a keyboard ninja and master the notebook environment.
**Time:** 45 Minutes

---

## **Part 1: The Basics (Modes)**

### **1.1 Understanding Modes**

Jupyter has two modes.

1. **Command Mode (Blue Border):** You are controlling the notebook structure. Press `Esc` to enter this.
2. **Edit Mode (Green Border):** You are typing inside a cell. Press `Enter` to enter this.

**⬇️ Action Drill ⬇️**

```python
# 1. Click inside this cell (Border turns Green).
# 2. Press 'Esc' (Border turns Blue).
# 3. Press 'Enter' (Border turns Green again).
# 4. Type your name below to prove you are in Edit Mode.


```

---

## **Part 2: Command Mode Shortcuts (Blue Bar)**

*Ensure you press `Esc` before doing these steps so your cell border is Blue.*

### **2.1 The "God Mode" Key (`h`)**

The most important shortcut. It shows you every available shortcut.

**⬇️ Action Drill ⬇️**

```python
# 1. Click this cell.
# 2. Press 'Esc'.
# 3. Press 'h'.
# 4. Scroll through the help menu that pops up.
# 5. Press 'Esc' again to close the menu.

```

### **2.2 Inserting Cells (`a` and `b`)**

We need more space. Let's add cells Above and Below.

**⬇️ Action Drill ⬇️**

```python
# 1. Click this cell.
# 2. Press 'Esc'.
# 3. Press 'a' (Observe a new empty cell appears ABOVE this one).
# 4. Press 'b' (Observe a new empty cell appears BELOW this one).

```

### **2.3 Deleting and Undoing (`dd` and `z`)**

Sometimes we make mistakes. Let's delete the cell below and bring it back.

**⬇️ Action Drill ⬇️**

```python
# 1. Click the cell BELOW this one (the one with "DELETE ME").
# 2. Press 'Esc'.
# 3. Press 'd' twice quickly (The cell will vanish).
# 4. Press 'z' (The cell will reappear).

```

```python
# DELETE ME! I am a mistake.

```

### **2.4 Cut, Copy, Paste (`x`, `c`, `v`)**

Moving cells around without using the mouse.

**⬇️ Action Drill ⬇️**

```python
# 1. Click this cell.
# 2. Press 'Esc'.
# 3. Press 'c' (Copy).
# 4. Press 'v' (Paste). 
# Result: You should see a duplicate of this cell appear below.

```

### **2.5 Navigation (`Up` and `Down`)**

Moving without the mouse.

**⬇️ Action Drill ⬇️**

```python
# 1. Press 'Esc'.
# 2. Use the Up Arrow key to move to the cell above.
# 3. Use the Down Arrow key to come back here.

```

### **2.6 Changing Cell Types (`m` and `y`)**

Converting Code to Markdown (Text) and back.

**⬇️ Action Drill ⬇️**

```python
print("I am currently Python Code. Make me Markdown!")

# 1. Click this cell.
# 2. Press 'Esc'.
# 3. Press 'm'. (The code highlighting disappears, it becomes raw text).
# 4. Press 'Shift + Enter' to render it.
# 5. Select it again, press 'y' to turn it back into code.

```

### **2.7 Toggle Line Numbers (`L`)**

Essential for debugging errors (e.g., "Error on line 4").

**⬇️ Action Drill ⬇️**

```python
# 1. Click this cell.
# 2. Press 'Esc'.
# 3. Press 'L'.
# Result: You should see line numbers (1, 2, 3...) appear on the left side.
line_1 = "code"
line_2 = "code"
line_3 = "code"

```

### **2.8 Merging Cells (`Shift + M`)**

Combine two cells into one.

**⬇️ Action Drill ⬇️**

```python
# 1. Click this cell.
# 2. Hold 'Shift' and press 'Down Arrow' to select the cell below it too.
# 3. Press 'Shift + M'.
# Result: The cell below should merge into this one.

```

```python
# I want to be merged with the cell above!

```

---

## **Part 3: Edit Mode Shortcuts (Green Bar)**

*Ensure you press `Enter` to be inside the cell.*

### **3.1 Autocomplete (`Tab`)**

Don't type full words. Let Jupyter do it.

**⬇️ Coding Drill ⬇️**

```python
# 1. Type 'pri' below and press 'Tab'. It should suggest 'print'.
# 2. Select print and hit Enter.


```

### **3.2 Tooltips (`Shift + Tab`)**

The most useful learning tool. It shows you how a function works.

**⬇️ Coding Drill ⬇️**

```python
# 1. Type 'len(' below.
# 2. With your cursor inside the parenthesis, press 'Shift + Tab'.
# 3. Read the popup to see what len() does.


```

### **3.3 Indenting (`Ctrl + ]` and `Ctrl + [`)**

Moving code blocks left or right.

**⬇️ Coding Drill ⬇️**

```python
# 1. Highlight the 3 print lines below.
# 2. Press 'Ctrl + ]' to indent them right.
# 3. Press 'Ctrl + [' to indent them back left.

print("Move me")
print("Move me")
print("Move me")

```

### **3.4 Commenting (`Ctrl + /`)**

Turn code into comments instantly.

**⬇️ Coding Drill ⬇️**

```python
# 1. Highlight the code line below.
# 2. Press 'Ctrl + /'.

print("I should be a comment")

```

### **3.5 Line Deletion (`Ctrl + D`)**

Delete a messy line instantly.

**⬇️ Coding Drill ⬇️**

```python
# 1. Click anywhere on the line that says "DELETE THIS LINE".
# 2. Press 'Ctrl + D'.

print("Keep me")
print("DELETE THIS LINE")
print("Keep me")

```

### **3.6 Undo Typing (`Ctrl + Z`)**

**⬇️ Coding Drill ⬇️**

```python
# 1. Type "Hello" below.
# 2. Press 'Ctrl + Z' to make it disappear.


```

---

## **Part 4: Execution Shortcuts**

### **4.1 The Three Ways to Run**

1. `Ctrl + Enter`: Run and **Stay**.
2. `Shift + Enter`: Run and **Move Down**.
3. `Alt + Enter`: Run and **Insert New Below**.

**⬇️ Action Drill ⬇️**

```python
# 1. Press 'Ctrl + Enter'. Note that you stay selected on this cell.
print("Run 1")

```

```python
# 2. Press 'Shift + Enter'. Note that you move to the next cell.
print("Run 2")

```

```python
# 3. Press 'Alt + Enter'. Note that a brand new empty cell is created below.
print("Run 3")

```

---

## **Part 5: Introspection (Getting Help)**

### **5.1 The Question Mark (`?`)**

Documentation retrieval.

**⬇️ Coding Drill ⬇️**

```python
# 1. Run this cell to see the help docs for the 'len' function.
len?

```

### **5.2 The Double Question Mark (`??`)**

Source code retrieval.

**⬇️ Coding Drill ⬇️**

```python
import random
# 1. Run this cell to see the actual source code of the randint function.
random.randint??

```

---

## **Part 6: Magic Commands (`%`)**

### **6.1 System Magics**

`%lsmagic`, `%pwd`, `%ls`, `%whos`.

**⬇️ Coding Drill ⬇️**

```python
# 1. Run this cell to see where your notebook is saved.
%pwd

```

```python
# 2. Run this cell to see all variables we have created so far.
%whos

```

### **6.2 Timing Code (`%timeit` and `%%time`)**

See how fast your code is.
`%` = One line.
`%%` = Whole cell.

**⬇️ Coding Drill ⬇️**

```python
# 1. Run this cell to time the whole block.
%%time
for i in range(1000000):
    pass

```

### **6.3 File Creation (`%%writefile`)**

Save cell content to a file.

**⬇️ Coding Drill ⬇️**

```python
# 1. Run this cell. It will create a file named 'hello.py' in your folder.
%%writefile hello.py
print("This file was created by Jupyter!")

```

---

## **Part 7: Shell Commands (`!`)**

Talking to the terminal.

**⬇️ Coding Drill ⬇️**

```python
# 1. Run this to check your Python version.
!python --version

```

```python
# 2. Run this to list files in the folder (Windows uses 'dir', Mac/Linux uses 'ls')
# Uncomment the one that matches your OS.

# !dir 
# !ls

```

---

## **Part 8: Kernel Operations**

*Emergency Controls.*

### **8.1 Interrupt (`I, I`)**

Stop an infinite loop.

**⬇️ Action Drill ⬇️**

```python
# 1. Run this cell (It will run forever because of while True).
# 2. Look at the circle in the top right (it will be filled/busy).
# 3. Press 'Esc', then press 'i' twice quickly.
# 4. The error "KeyboardInterrupt" should appear.

import time
while True:
    time.sleep(1)

```

### **8.2 Restart (`0, 0`)**

Clean slate.

**⬇️ Action Drill ⬇️**

```python
# 1. Define this variable
my_secret_var = 100

```

```python
# 2. Press 'Esc', then press '0' twice quickly.
# 3. Confirm the restart.
# 4. Now Try to run THIS cell. It should give an error because memory was wiped.
print(my_secret_var)

```

---

## **Part 9: Markdown Mastery**

Formatting text.

**⬇️ Action Drill ⬇️**

```python
# 1. Change this cell to Markdown mode (Esc -> m).
# 2. Paste the text below into the cell.
# 3. Run the cell (Shift + Enter).

# My Big Header
## My Sub Header
* Bullet point 1
* Bullet point 2
1. Numbered list
2. Numbered list

**I am Bold**
*I am Italic*

```python
print("I am code inside markdown")

```



```

```