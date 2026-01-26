# **Project: The "Resume Cleaner" Application**

**Time:** 40 min

### **The Goal**

You are building a tool for HR.
You receive raw, messy text input from resumes (simulated by user input). Your job is to extract the name, clean it, format the job title, calculating salary expectations, and generate a clean ID tag.

### **Application Requirements**

1. **Input:** Ask for a messy name (e.g., "  jOhn dOe "), a job title, and a desired monthly salary.
2. **Clean:** Remove spaces and standardize name capitalization.
3. **Validate:** Check if the salary entered is actually a number.
4. **Format:** Convert monthly salary to annual, formatted with commas.
5. **Report:** Print a "Candidate Card" using string repetition for borders and f-strings for layout.

---

### **Step 1: Input & Basic Cleaning**

**Logic:** Get the inputs. Use `strip()` to remove accidental spaces users might type, and `title()` to fix the name casing immediately.

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Ask user for full name (store in 'raw_name').

# 2. Ask user for job title (store in 'raw_job').

# 3. Ask user for monthly salary expectation (store in 'raw_salary').

# 4. Create 'clean_name': Strip spaces from 'raw_name' and convert to Title Case.

# 5. Create 'clean_job': Strip spaces from 'raw_job' and convert to Upper Case.

```

<div style="height: 300px; background-color: #f9f9f9; text-align: center; padding-top: 100px;">
<p><strong>🛑 SCROLL DOWN FOR SOLUTION 🛑</strong></p>
</div>

**✅ Step 1 Solution:**

```python
# 1. Inputs
raw_name = input("Enter Full Name: ")
raw_job = input("Enter Job Title: ")
raw_salary = input("Enter Monthly Salary: ")

# 2. Cleaning
clean_name = raw_name.strip().title()
clean_job = raw_job.strip().upper()

```

---

### **Step 2: Validation & Math**

**Logic:** We need to ensure the salary is a number before doing math. If it is, we calculate the annual salary. *Note: Since we haven't learned "if" statements yet, we will assume the user is good and types a number, but we will print the result of the validation check.*

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Print a boolean check: "Salary input is valid number: [True/False]" using .isdigit()

# 2. Convert 'raw_salary' to an integer (store in 'int_salary').

# 3. Calculate 'annual_salary' (int_salary * 12).

```

<div style="height: 300px; background-color: #f9f9f9; text-align: center; padding-top: 100px;">
<p><strong>🛑 SCROLL DOWN FOR SOLUTION 🛑</strong></p>
</div>

**✅ Step 2 Solution:**

```python
# 1. Validation check
print(f"Salary input is valid number: {raw_salary.isdigit()}")

# 2. Conversion
int_salary = int(raw_salary)

# 3. Math
annual_salary = int_salary * 12

```

---

### **Step 3: ID Generation & Formatting**

**Logic:** Generate a User ID by taking the first 3 letters of their name and the length of their job title. Then print everything beautifully.

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Create 'user_id': Concatenate first 3 letters of 'clean_name' + length of 'clean_job'.
#    Hint: clean_name[0:3] + str(len(clean_job))

# 2. Create a 'separator' line using "-" repeated 30 times.

# 3. Print the separator.
# 4. Print "CANDIDATE CARD".
# 5. Print the separator again.
# 6. Print Name (using f-string).
# 7. Print Job (using f-string).
# 8. Print Annual Salary (using f-string). 
#    Try to use the comma format for thousands separator: {annual_salary:,}
# 9. Print User ID.
# 10. Print the separator.

```

<div style="height: 300px; background-color: #f9f9f9; text-align: center; padding-top: 100px;">
<p><strong>🛑 SCROLL DOWN FOR SOLUTION 🛑</strong></p>
</div>

**✅ Step 3 Solution:**

```python
# 1. ID Generation
user_id = clean_name[0:3] + str(len(clean_job))

# 2. Formatting
separator = "-" * 30

# 3. Report
print(separator)
print("CANDIDATE CARD")
print(separator)
print(f"Name:   {clean_name}")
print(f"Role:   {clean_job}")
print(f"Annual: ${annual_salary:,}") # The :, adds commas like 120,000
print(f"ID Tag: {user_id}")
print(separator)

```

---

### **Step 4: Final Assembly**

Combine all the logic into one script below to see your Resume Cleaner in action!

**⬇️ Paste all code below ⬇️**

```python
# --- INPUTS ---


# --- CLEANING & LOGIC ---


# --- OUTPUT REPORT ---



```
---