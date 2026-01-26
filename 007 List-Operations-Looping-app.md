# **Capstone Project: The "Data Cleaner & Grade Analyzer"**

### **Goal**

You are a Data Scientist at a university. You have received a "dirty" dataset of student exam scores. The data contains errors (negative numbers), duplicates, and needs to be processed.

Your goal is to build an **Interactive Command-Line Application** that:

1. Loads raw data.
2. Cleans the data (Removes invalid entries and duplicates).
3. Calculates statistics (Average, Max, Min).
4. Assigns letter grades to each score.
5. Allows a user to add new scores dynamically via a menu.

### **Requirements**

* **Data Structures:** Lists.
* **Control Flow:** `For` loops for processing, `While` loops for the menu.
* **Logic:** `If/Elif/Else` for grading and validation.
* **Operations:** Sorting, appending, and mathematical operators.

---

### **Step 0: Setup Sample Data**

First, let's generate the "raw" data file. This represents the messy data you receive from a client.

**Run the cell below to initialize the project.**

```python
# Raw dataset containing student scores
# Includes duplicates (85), invalid negative numbers (-10), and out-of-bound numbers (150)
raw_scores = [85, 92, -10, 55, 85, 150, 42, 78, 92, 105, 60]

print("Raw Data Loaded:", raw_scores)

```

---

### **Step 1: Data Cleaning Pipeline**

**Logical Step:**
We need to separate the valid data from the noise. We will create a new list that only contains scores between 0 and 100. We will also discard any scores that are not valid.

**Task:**

1. Create an empty list for valid scores.
2. Loop through the `raw_scores`.
3. Check if the score is valid (0 to 100).
4. If valid, add it to your new list.

**Write your code in the cell below following the comments:**

```python
# 1. Create an empty list named 'valid_scores'

# 2. Start a FOR loop to iterate through each 'score' in 'raw_scores'

    # 3. Inside the loop, write an IF statement to check if 'score' is greater than or equal to 0 AND less than or equal to 100

        # 4. If the condition is true, APPEND the 'score' to 'valid_scores'

# 5. Print the 'valid_scores' list to check your work

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Create an empty list named 'valid_scores'
valid_scores = []

# 2. Start a FOR loop to iterate through each 'score' in 'raw_scores'
for score in raw_scores:

    # 3. Inside the loop, write an IF statement to check if 'score' is greater than or equal to 0 AND less than or equal to 100
    if score >= 0 and score <= 100:

        # 4. If the condition is true, APPEND the 'score' to 'valid_scores'
        valid_scores.append(score)

# 5. Print the 'valid_scores' list to check your work
print("Valid Scores:", valid_scores)

```

---

### **Step 2: Handling Duplicates**

**Logical Step:**
Our list still has duplicate entries (like `85` and `92`). We need a list of **unique** scores to perform a fair analysis.

**Task:**

1. Create an empty list for unique scores.
2. Loop through the `valid_scores`.
3. Check if the score is **NOT** already in your unique list.
4. If it is new, add it.

**Write your code in the cell below following the comments:**

```python
# 1. Create an empty list named 'unique_scores'

# 2. Start a FOR loop to iterate through each 'score' in 'valid_scores'

    # 3. Write an IF statement to check if 'score' is NOT IN 'unique_scores'

        # 4. If true, APPEND 'score' to 'unique_scores'

# 5. Print 'unique_scores'

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Create an empty list named 'unique_scores'
unique_scores = []

# 2. Start a FOR loop to iterate through each 'score' in 'valid_scores'
for score in valid_scores:

    # 3. Write an IF statement to check if 'score' is NOT IN 'unique_scores'
    if score not in unique_scores:

        # 4. If true, APPEND 'score' to 'unique_scores'
        unique_scores.append(score)

# 5. Print 'unique_scores'
print("Unique Scores:", unique_scores)

```

---

### **Step 3: Advanced Analysis (Sorting & Logic)**

**Logical Step:**
Now we want to organize the data. We will sort the scores, find the top and bottom performers, and calculate the class average.

**Task:**

1. Sort the unique list in descending order (High to Low).
2. Identify the Max and Min scores using indexing (since it's sorted).
3. Calculate the average (Sum of scores / Number of scores).

**Write your code in the cell below following the comments:**

```python
# 1. Use the .sort() method on 'unique_scores' with reverse=True to sort descending

# 2. Get the highest score. Since it's sorted descending, it's at index 0. Assign to variable 'max_score'

# 3. Get the lowest score. It is at index -1. Assign to variable 'min_score'

# 4. Calculate the sum of all scores using sum() and divide by the len() of the list. Assign to 'avg_score'

# 5. Print max_score, min_score, and avg_score with descriptive text

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Use the .sort() method on 'unique_scores' with reverse=True to sort descending
unique_scores.sort(reverse=True)

# 2. Get the highest score. Since it's sorted descending, it's at index 0. Assign to variable 'max_score'
max_score = unique_scores[0]

# 3. Get the lowest score. It is at index -1. Assign to variable 'min_score'
min_score = unique_scores[-1]

# 4. Calculate the sum of all scores using sum() and divide by the len() of the list. Assign to 'avg_score'
avg_score = sum(unique_scores) / len(unique_scores)

# 5. Print max_score, min_score, and avg_score with descriptive text
print(f"Max: {max_score}, Min: {min_score}, Average: {avg_score}")

```

---

### **Step 4: Grading Logic**

**Logical Step:**
We need to automate the grading process. We will iterate through the scores and print a letter grade for each one based on a grading scale:

* 90+ : A
* 80-89: B
* 70-79: C
* Below 70: F

**Task:**
Use a loop and an `if-elif-else` chain.

**Write your code in the cell below following the comments:**

```python
# 1. Loop through each 'score' in 'unique_scores'

    # 2. IF score is greater than or equal to 90
        # Print "Score: [score] - Grade: A"

    # 3. ELIF score is greater than or equal to 80
        # Print "Score: [score] - Grade: B"

    # 4. ELIF score is greater than or equal to 70
        # Print "Score: [score] - Grade: C"

    # 5. ELSE
        # Print "Score: [score] - Grade: F"

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Loop through each 'score' in 'unique_scores'
for score in unique_scores:

    # 2. IF score is greater than or equal to 90
    if score >= 90:
        print(f"Score: {score} - Grade: A")

    # 3. ELIF score is greater than or equal to 80
    elif score >= 80:
        print(f"Score: {score} - Grade: B")

    # 4. ELIF score is greater than or equal to 70
    elif score >= 70:
        print(f"Score: {score} - Grade: C")

    # 5. ELSE
    else:
        print(f"Score: {score} - Grade: F")

```

---

### **Step 5: The Interactive Application (The "While" Loop)**

**Logical Step:**
We will wrap everything into an interactive menu. The program should run indefinitely until the user chooses to "Exit". This requires a `while` loop that listens for user input.

**Task:**

1. Initialize a boolean variable `app_running = True`.
2. Start a `while` loop.
3. Ask for user input (1. Add Score, 2. Show Stats, 3. Exit).
4. Perform actions based on input.

**Write your code in the cell below following the comments:**

```python
# 1. Create a boolean variable 'app_running' and set it to True
# 2. Create a list 'class_scores' and initialize it with some starter numbers like [80, 90]

# 3. Start a WHILE loop that runs as long as 'app_running' is True

    # 4. Print a separator line "--- Menu ---"
    # 5. Print options: "1. Add Score", "2. Show Stats", "3. Exit"

    # 6. Create a variable 'choice' and capture user INPUT with the prompt "Enter choice: "

    # 7. Check IF 'choice' is equal to "1" (Remember input returns a string)
        # 8. Ask user for a new number using input(), convert it to int, and assign to 'new_val'
        # 9. Append 'new_val' to 'class_scores'
        # 10. Print "Score added!"

    # 11. Check ELIF 'choice' is equal to "2"
        # 12. Calculate average (sum / len) and print "Class Average: [value]"
        # 13. Print the raw list 'class_scores'

    # 14. Check ELIF 'choice' is equal to "3"
        # 15. Print "Exiting..."
        # 16. Set 'app_running' to False (This stops the loop)

    # 17. ELSE (if they type anything else)
        # 18. Print "Invalid choice, try again."

```






















**⬇️ SCROLL DOWN FOR SOLUTION ⬇️**






















**Solution:**

```python
# 1. Create a boolean variable 'app_running' and set it to True
app_running = True
# 2. Create a list 'class_scores' and initialize it with some starter numbers
class_scores = [80, 90, 75]

# 3. Start a WHILE loop that runs as long as 'app_running' is True
while app_running:

    # 4. Print a separator line "--- Menu ---"
    print("\n--- Menu ---")
    # 5. Print options
    print("1. Add Score")
    print("2. Show Stats")
    print("3. Exit")

    # 6. Create a variable 'choice' and capture user INPUT
    choice = input("Enter choice: ")

    # 7. Check IF 'choice' is equal to "1"
    if choice == "1":
        # 8. Ask user for a new number, convert to int
        new_val = int(input("Enter new score: "))
        # 9. Append 'new_val' to 'class_scores'
        class_scores.append(new_val)
        # 10. Print confirmation
        print("Score added!")

    # 11. Check ELIF 'choice' is equal to "2"
    elif choice == "2":
        # 12. Calculate and print average
        avg = sum(class_scores) / len(class_scores)
        print(f"Class Average: {avg}")
        # 13. Print the raw list
        print(f"Scores: {class_scores}")

    # 14. Check ELIF 'choice' is equal to "3"
    elif choice == "3":
        # 15. Print exiting
        print("Exiting...")
        # 16. Set 'app_running' to False to stop the loop
        app_running = False

    # 17. ELSE
    else:
        # 18. Print invalid
        print("Invalid choice, try again.")

```

---

### **Final Challenge: The Complete Application**

**Goal:** Combine **Step 1 (Cleaning)**, **Step 2 (Uniques)**, **Step 4 (Grading)**, and **Step 5 (Menu)** into one giant block of code.

**Instructions:**

1. Copy the code from the "Interactive Application" (Step 5) as your base.
2. Inside Option "2" (Show Stats):
* Add the logic to filter valid scores (0-100) first.
* Add the logic to remove duplicates.
* Sort the cleaned list.
* Print the stats (Max/Min/Avg).
* Loop through and print the letter grade for every score.



**This is your final exam! Try to assemble it below.**

```python
# Combine all your logic here!

```