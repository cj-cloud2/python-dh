# **Capstone Project: The "Library Management System"**

### **Goal**

You are a Librarian who is tired of tracking books on paper. You want to build a digital **Library Management System**.
Your goal is to build an interactive command-line app that:

1. **Loads** the current library inventory from a text file.
2. **Converts** that file data into a Python **Dictionary** for fast lookup.
3. Allows you to **Search**, **Checkout**, and **Return** books (updating the dictionary).
4. **Saves** the updated inventory back to the file (Writing/Overwriting).
5. **Backs up** the old inventory file before saving (File Management).

### **Requirements**

* **File Handling:** Reading (`r`), Writing (`w`), Appending (`a`), `with` statement, `os` module for backups.
* **Dictionaries:** Nested dictionary structure `{ "BookTitle": {"Author": "Name", "Status": "Available"} }`.
* **Logic:** Loops for the menu, If/Else for checking availability.

---

### **Step 0: Setup Sample Data**

First, we need to create a dummy "database" file. This represents the library's current stock.

**Run the cell below to initialize the project.**

```python
# Open a file named "library_db.txt" in write mode to create sample data
with open("library_db.txt", "w") as f:
    # Write book data in the format: Title,Author,Status
    f.write("The Great Gatsby,F. Scott Fitzgerald,Available\n")
    f.write("1984,George Orwell,Checked Out\n")
    f.write("Python Crash Course,Eric Matthes,Available\n")
    f.write("Clean Code,Robert Martin,Available")

# Print confirmation
print("Setup Complete: 'library_db.txt' created.")

```

---

### **Step 1: Loading Data (File to Dictionary)**

**Logical Step:**
We cannot edit a text file easily line-by-line. We need to load it into a Python **Dictionary** where the *Key* is the Book Title and the *Value* is another dictionary containing Author and Status.

* **Structure:** `{'1984': {'Author': 'George Orwell', 'Status': 'Checked Out'}}`

**Topics Covered:** Reading Files (`readlines`), String Manipulation (`strip`, `split`), Nested Dictionary Creation.

**Task:**

1. Create an empty dictionary `library`.
2. Open `library_db.txt` in read mode.
3. Loop through lines, split them by comma `,`.
4. Store data into the dictionary.

**Write your code in the cell below following the comments:**

```python
# 1. Create an empty dictionary named 'library'

# 2. Use 'with' to open "library_db.txt" in read mode 'r' as 'file'

    # 3. Read all lines using .readlines() and store in variable 'lines'

# 4. Loop through each 'line' in 'lines'

    # 5. Strip whitespace (.strip()) and Split the line by comma ",". Assign to title, author, status

    # 6. Add to 'library' dict: Key is 'title', Value is a dict {'Author': author, 'Status': status}

# 7. Print the 'library' dictionary to verify

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Create an empty dictionary named 'library'
library = {}

# 2. Use 'with' to open "library_db.txt" in read mode 'r' as 'file'
with open("library_db.txt", "r") as file:

    # 3. Read all lines using .readlines() and store in variable 'lines'
    lines = file.readlines()

# 4. Loop through each 'line' in 'lines'
for line in lines:

    # 5. Strip whitespace (.strip()) and Split the line by comma ",". Assign to title, author, status
    title, author, status = line.strip().split(",")

    # 6. Add to 'library' dict: Key is 'title', Value is a dict {'Author': author, 'Status': status}
    library[title] = {"Author": author, "Status": status}

# 7. Print the 'library' dictionary to verify
print(library)

```

---

### **Step 2: The "Checkout" Feature (Dictionary Update)**

**Logical Step:**
We need to let a user borrow a book. We ask for the title. If it exists AND is "Available", we change its status to "Checked Out".

**Topics Covered:** Checking Key Existence, Accessing Nested Values, Changing Dictionary Values.

**Task:**

1. Ask user for a book title.
2. Check if book is in `library`.
3. Check if status is "Available".
4. Update status.

**Write your code in the cell below following the comments:**

```python
# 1. Capture user input for "Enter book title to checkout: " into variable 'book_name'

# 2. Check IF 'book_name' is IN the 'library' dictionary

    # 3. Check IF library[book_name]["Status"] is equal to "Available"

        # 4. Update the status: Set library[book_name]["Status"] to "Checked Out"
        # 5. Print "You have successfully borrowed [book_name]"

    # 6. ELSE (If status was not Available)
        # 7. Print "Sorry, this book is currently checked out."

# 8. ELSE (If book not in library)
    # 9. Print "Book not found."

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Capture user input for "Enter book title to checkout: " into variable 'book_name'
book_name = input("Enter book title to checkout: ")

# 2. Check IF 'book_name' is IN the 'library' dictionary
if book_name in library:

    # 3. Check IF library[book_name]["Status"] is equal to "Available"
    if library[book_name]["Status"] == "Available":

        # 4. Update the status: Set library[book_name]["Status"] to "Checked Out"
        library[book_name]["Status"] = "Checked Out"
        # 5. Print "You have successfully borrowed [book_name]"
        print(f"You have successfully borrowed {book_name}")

    # 6. ELSE (If status was not Available)
    else:
        # 7. Print "Sorry, this book is currently checked out."
        print("Sorry, this book is currently checked out.")

# 8. ELSE (If book not in library)
else:
    # 9. Print "Book not found."
    print("Book not found.")

```

---

### **Step 3: Creating a Backup (OS Module)**

**Logical Step:**
Before we save our changes to the main file, we should backup the old one just in case. We will create a directory called `backups` and copy the current file there.

**Topics Covered:** `os` module, Creating Directories, File Existence.

**Task:**

1. Import `os`.
2. Check if `backups` folder exists; if not, make it.
3. Read the current `library_db.txt` and write it to `backups/library_backup.txt`.

**Write your code in the cell below following the comments:**

```python
# 1. Import the 'os' module
import os

# 2. Check IF the directory "backups" does NOT exist
if not os.path.exists("backups"):
    # 3. Create the directory "backups"
    os.mkdir("backups")

# 4. Open "library_db.txt" in read mode ('r') as 'original'
with open("library_db.txt", "r") as original:
    # 5. Read data from 'original'
    data = original.read()

# 6. Open "backups/library_backup.txt" in write mode ('w') as 'backup'
with open("backups/library_backup.txt", "w") as backup:
    # 7. Write 'data' to 'backup'
    backup.write(data)

# 8. Print "Backup created successfully."

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Import the 'os' module
import os

# 2. Check IF the directory "backups" does NOT exist
if not os.path.exists("backups"):
    # 3. Create the directory "backups"
    os.mkdir("backups")

# 4. Open "library_db.txt" in read mode ('r') as 'original'
with open("library_db.txt", "r") as original:
    # 5. Read data from 'original'
    data = original.read()

# 6. Open "backups/library_backup.txt" in write mode ('w') as 'backup'
with open("backups/library_backup.txt", "w") as backup:
    # 7. Write 'data' to 'backup'
    backup.write(data)

# 8. Print "Backup created successfully."
print("Backup created successfully.")

```

---

### **Step 4: Saving Changes (Dict to File)**

**Logical Step:**
Now that we've updated our dictionary (checked out a book) and backed up the old file, we need to save the dictionary back to `library_db.txt`. This overwrites the old text file with the new status.

**Topics Covered:** Writing Files (Overwrite), Looping through Dictionaries.

**Task:**

1. Open `library_db.txt` in write (`w`) mode.
2. Loop through the dictionary.
3. Format the string as `Title,Author,Status`.
4. Write to file.

**Write your code in the cell below following the comments:**

```python
# 1. Use 'with' to open "library_db.txt" in write mode 'w' as 'file'

    # 2. Loop through 'title' and 'info' in library.items()

        # 3. Create a formatted string: f"{title},{info['Author']},{info['Status']}\n"

        # 4. Write the string to 'file'

# 5. Print "Library database updated."

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Use 'with' to open "library_db.txt" in write mode 'w' as 'file'
with open("library_db.txt", "w") as file:

    # 2. Loop through 'title' and 'info' in library.items()
    for title, info in library.items():

        # 3. Create a formatted string: f"{title},{info['Author']},{info['Status']}\n"
        line = f"{title},{info['Author']},{info['Status']}\n"

        # 4. Write the string to 'file'
        file.write(line)

# 5. Print "Library database updated."
print("Library database updated.")

```

---

### **Step 5: The Main Application Loop**

**Logical Step:**
Let's bring it all together in a `while` loop menu. This is the code you would run to start the app.
We will initialize the library from the file at the start, then enter the loop.

**Task:**
Combine loading, menu choice, checkout logic, and saving into one block.

**Write your code in the cell below following the comments:**

```python
# --- INITIALIZATION ---
# 1. Initialize empty dict 'library'
# 2. Load data from "library_db.txt" (Copy logic from Step 1)

# --- MAIN LOOP ---
# 3. Start a WHILE True loop

    # 4. Print Menu: "1. View Books", "2. Checkout Book", "3. Return Book", "4. Save & Exit"
    # 5. Get user input 'choice'

    # 6. IF choice == "1":
        # 7. Loop through library and print Title and Status

    # 8. ELIF choice == "2":
        # 9. Perform Checkout Logic (Copy Step 2 logic)

    # 10. ELIF choice == "3":
        # 11. Ask for book title
        # 12. If exists, set Status to "Available"
        # 13. Print success message

    # 14. ELIF choice == "4":
        # 15. Perform Backup (Step 3 Logic)
        # 16. Perform Save (Step 4 Logic)
        # 17. Print "Saved and Exiting."
        # 18. BREAK the loop

    # 19. ELSE:
        # 20. Print "Invalid choice"

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# --- INITIALIZATION ---
# 1. Initialize empty dict 'library'
library = {}
# 2. Load data from "library_db.txt"
if os.path.exists("library_db.txt"):
    with open("library_db.txt", "r") as f:
        for line in f:
            if line.strip(): # Check if line is not empty
                title, author, status = line.strip().split(",")
                library[title] = {"Author": author, "Status": status}

# --- MAIN LOOP ---
# 3. Start a WHILE True loop
while True:

    # 4. Print Menu
    print("\n--- Library Menu ---")
    print("1. View Books")
    print("2. Checkout Book")
    print("3. Return Book")
    print("4. Save & Exit")
    
    # 5. Get user input 'choice'
    choice = input("Enter choice: ")

    # 6. IF choice == "1":
    if choice == "1":
        # 7. Loop through library and print Title and Status
        for title, data in library.items():
            print(f"{title} - [{data['Status']}]")

    # 8. ELIF choice == "2":
    elif choice == "2":
        # 9. Perform Checkout Logic
        book = input("Enter book to checkout: ")
        if book in library:
            if library[book]["Status"] == "Available":
                library[book]["Status"] = "Checked Out"
                print("Checkout successful.")
            else:
                print("Book already checked out.")
        else:
            print("Book not found.")

    # 10. ELIF choice == "3":
    elif choice == "3":
        # 11. Ask for book title
        book = input("Enter book to return: ")
        # 12. If exists, set Status to "Available"
        if book in library:
            library[book]["Status"] = "Available"
            # 13. Print success message
            print("Returned successfully.")
        else:
            print("Book not found.")

    # 14. ELIF choice == "4":
    elif choice == "4":
        # 15. Perform Backup
        if not os.path.exists("backups"):
            os.mkdir("backups")
        with open("library_db.txt", "r") as original:
            with open("backups/library_backup.txt", "w") as backup:
                backup.write(original.read())
        
        # 16. Perform Save
        with open("library_db.txt", "w") as file:
            for title, info in library.items():
                line = f"{title},{info['Author']},{info['Status']}\n"
                file.write(line)
        
        # 17. Print "Saved and Exiting."
        print("Saved and Exiting.")
        # 18. BREAK the loop
        break

    # 19. ELSE:
    else:
        # 20. Print "Invalid choice"
        print("Invalid choice.")

```

---

### **Final Challenge: Run the App**

**Goal:** Copy the Initialization and Main Loop code into the single cell below to run your full Library Management System.

```python
# Assemble your full application here!

```