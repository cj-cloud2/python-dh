# **Lab Project: The "Market Volatility" Forecaster**

**Time Allocation:** 1 Hour

### **The Goal**

You are going to build a **Financial Projection Tool**.
As Data Scientists, you often deal with uncertainty. In this app, you will simulate how an investment might perform based on a random "market factor."
Since we haven't covered loops or logic (`if/else`) yet, this application will be a **linear simulation script**.

### **Application Requirements**

1. **Accept User Data:** The app must ask the user for their name, their initial investment amount (USD), and a fixed interest rate they *hope* to get.
2. **Generate Randomness:** The app will simulate "Market Volatility" by generating a random actual interest rate (different from what the user hoped for).
3. **Perform Calculations:** It will calculate the "Expected Return" vs. the "Actual Return" (based on the random number).
4. **Report Results:** It will display the difference (Profit or Loss) between the expected and actual outcome.

---

### **Step 1: Setup and Inputs**

**Logic:**
We need to bring in the `random` library to generate numbers later. Then, we need to capture data from the user. Remember, `input()` always gives you a **string**, so if you want to do math with money, you must convert (cast) it to a **float** or **int**.

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Import the random module so we can use it later

# 2. Ask the user for their name and assign it to a variable called 'user_name'

# 3. Ask the user for their investment amount.
#    (Wrap this input in a float() function so we can do math with it).
#    Assign it to a variable called 'principal'

# 4. Ask the user for their expected interest rate (e.g., enter 10 for 10%).
#    (Wrap this input in an int() or float() function).
#    Assign it to a variable called 'expected_rate'

# 5. Print a message saying "Calculation started for [user_name]..."

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 1 Solution:**

```python
# 1. Import the random module
import random

# 2. Input name
user_name = input("Please enter your name: ")

# 3. Input Principal (Casting to float immediately)
principal = float(input("Enter your investment amount ($): "))

# 4. Input Rate (Casting to int or float)
expected_rate = int(input("Enter your expected interest rate (%): "))

# 5. Confirmation print
print(f"Calculation started for {user_name}...")

```

---

### **Step 2: The "Safe" Calculation**

**Logic:**
Now we need to calculate what the user *thinks* they will earn.

* *Formula:* `Interest = Principal * (Rate / 100)`
* *Formula:* `Total = Principal + Interest`

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Calculate the 'expected_interest' amount.
#    (Hint: Multiply 'principal' by 'expected_rate', then divide by 100)

# 2. Calculate the 'expected_total' amount.
#    (Hint: Add 'principal' and 'expected_interest')

# 3. Print the Expected Total amount.

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 2 Solution:**

```python
# 1. Calculate interest amount
expected_interest = principal * (expected_rate / 100)

# 2. Calculate total
expected_total = principal + expected_interest

# 3. Print result
print(f"Based on your inputs, you expect to have: ${expected_total}")

```

---

### **Step 3: The "Market Volatility" (Randomness)**

**Logic:**
Markets are unpredictable. We will generate a **random** interest rate to simulate reality. We want a random integer between a low range (e.g., -5% loss) and a high range (e.g., 20% gain).

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Generate a random integer between -5 and 20.
#    Assign this to a variable called 'actual_rate'

# 2. Calculate the 'actual_interest' using this new random rate.
#    (Hint: principal * (actual_rate / 100) )

# 3. Calculate the 'actual_total'.
#    (Hint: principal + actual_interest)

# 4. Print the Actual Rate generated so the user sees it.

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 3 Solution:**

```python
# 1. Generate random rate
actual_rate = random.randint(-5, 20)

# 2. Calculate actual interest
actual_interest = principal * (actual_rate / 100)

# 3. Calculate actual total
actual_total = principal + actual_interest

# 4. Reveal the random rate
print(f"Market Volatility Factor: {actual_rate}%")

```

---

### **Step 4: The Analysis (Comparison)**

**Logic:**
Now we have two futures: the **Expected** (User defined) and the **Actual** (Randomly defined). Let's calculate the difference (Delta) to see if the user made more or less money than predicted.

**⬇️ Your Turn: Write the code below the comments ⬇️**

```python
# 1. Calculate the difference.
#    Variable 'difference' = 'actual_total' minus 'expected_total'

# 2. Print the Final Actual Total.

# 3. Print the Difference value.

```

<div style="height: 500px; background-color: #f9f9f9; text-align: center; padding-top: 200px;">
<p><strong>🛑 SCROLL DOWN ONLY AFTER ATTEMPTING THE CODE 🛑</strong></p>
<p>(Space left intentionally blank to hide the solution)</p>
</div>

**✅ Step 4 Solution:**

```python
# 1. Calculate difference
difference = actual_total - expected_total

# 2. Print final total
print(f"Your ACTUAL final amount is: ${actual_total}")

# 3. Print difference
print(f"Difference from projection: ${difference}")

```

---

### **Step 5: Assemble the Application**

Now, copy your code from the solutions above and paste them into one single cell below. Run it multiple times to see how the Random Market Factor changes your results every time!

**⬇️ Paste all code below ⬇️**

```python
# --- IMPORTS ---
import random

# --- INPUTS ---


# --- EXPECTED CALCULATIONS ---


# --- ACTUAL (RANDOM) CALCULATIONS ---


# --- ANALYSIS & OUTPUT ---
print("---------------------------------")
print("FINAL REPORT")
print("---------------------------------")



```