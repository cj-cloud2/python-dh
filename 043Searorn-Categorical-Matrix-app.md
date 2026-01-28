# **Project Lab: The HR Analytics Dashboard**

**Time Allocation:** 60 Minutes

### **The End Goal**

You have been promoted to Lead HR Data Analyst. The Director of Human Resources has asked for a report to understand the company's workforce structure, compensation fairness, and performance metrics.

You will build a dashboard that displays:

1. **Headcount Analysis:** Visualizing how many employees are in each department.
2. **Compensation Structure:** Comparing salary distributions across roles to detect outliers.
3. **Performance Grid:** A multi-chart view showing how satisfaction relates to performance in every department.
4. **Correlation Heatmap:** A matrix showing how variables like Experience, Salary, and Satisfaction are linked.

### **Requirements**

* Use `seaborn.countplot` for headcount.
* Use `seaborn.boxplot` or `violinplot` for salary distributions.
* Use `seaborn.catplot` for the multi-department grid.
* Use `seaborn.heatmap` for the correlation matrix.
* Use a consistent color palette (e.g., "Set2" or "viridis").

---

### **0. Setup: Create the HR Data**

*Run this cell first. It generates the synthetic employee records we will analyze.*

```python
# Import seaborn for statistical plotting
import seaborn as sns
# Import pandas for data manipulation
import pandas as pd
# Import numpy for random number generation
import numpy as np
# Import matplotlib for figure customization
import matplotlib.pyplot as plt

# Set the visual style to whitegrid
sns.set_theme(style="whitegrid")

# Create a sample dataset of 400 employees
n = 400
# Generate Departments
depts = np.random.choice(['R&D', 'Sales', 'HR'], n, p=[0.5, 0.4, 0.1])
# Generate Gender
gender = np.random.choice(['Male', 'Female'], n)
# Generate Years at Company (0 to 20)
years = np.random.randint(0, 20, n)
# Generate Performance Rating (1 to 5)
perf = np.random.randint(1, 6, n)
# Generate Job Satisfaction (1 to 10)
satisfaction = np.random.randint(1, 11, n)

# Generate Salaries based on Dept and Years (plus noise)
base_salary = {'R&D': 50000, 'Sales': 45000, 'HR': 40000}
salaries = [base_salary[d] + (y * 2000) + np.random.normal(0, 5000) for d, y in zip(depts, years)]

# Add some outliers (Executives)
salaries[0] = 150000
salaries[1] = 145000

# Create DataFrame
df = pd.DataFrame({
    'Department': depts,
    'Gender': gender,
    'Years_Experience': years,
    'Performance_Rating': perf,
    'Job_Satisfaction': satisfaction,
    'Salary': salaries
})

print("HR Database Loaded: 'df' is ready for analysis.")

```

---

### **Logical Step 1: Workforce Distribution (Counts & Bars)**

**Explanation:** First, we need the "Big Picture." We need two charts side-by-side.

1. A **Count Plot** to show how many people are in each Department.
2. A **Bar Plot** to show the Average Job Satisfaction by Department.

#### **Exercise 1: Headcount & Satisfaction**

```python
# Create a figure with 1 row and 2 columns, size 12x5.
# On axis 0 (left): Create a countplot using 'Department'.
# Color the bars using palette 'Set2'.
# Set the title to "Headcount by Dept".
# On axis 1 (right): Create a barplot showing Average 'Job_Satisfaction' by 'Department'.
# Separate the bars by 'Gender' (hue).
# Set the title to "Satisfaction by Dept & Gender".

```

























#### **Solution 1**

```python
# Initialize a figure with two subplots
fig, ax = plt.subplots(1, 2, figsize=(12, 5))

# Create a count plot on the first axis
sns.countplot(data=df, x='Department', palette='Set2', ax=ax[0])
# Set title for the first plot
ax[0].set_title("Headcount by Dept")

# Create a bar plot on the second axis comparing satisfaction
sns.barplot(data=df, x='Department', y='Job_Satisfaction', hue='Gender', palette='Set2', ax=ax[1])
# Set title for the second plot
ax[1].set_title("Satisfaction by Dept & Gender")

```

---

### **Logical Step 2: Salary fairness (Box & Violin)**

**Explanation:** We need to check if salaries are fair and identify outliers (people earning suspiciously high or low amounts). We will use a **Boxplot** to find outliers and a **Violinplot** to see if the salary "shape" is the same for Men and Women.

#### **Exercise 2: Compensation Analysis**

```python
# Create a figure with 1 row and 2 columns, size 14x6.
# On axis 0: Create a boxplot of 'Salary' grouped by 'Department'.
# This helps us see the outliers (dots).
# On axis 1: Create a violinplot of 'Salary' grouped by 'Department'.
# Add 'hue'='Gender' to split the violins.
# Set 'split=True' so the male/female violins are merged into one shape.
# Set inner='quart' to show quartile lines inside the violin.

```

























#### **Solution 2**

```python
# Initialize a figure with two subplots
fig, ax = plt.subplots(1, 2, figsize=(14, 6))

# Create a box plot to detect outliers
sns.boxplot(data=df, x='Department', y='Salary', ax=ax[0], palette='pastel')
# Set title for box plot
ax[0].set_title("Salary Ranges & Outliers")

# Create a violin plot to compare distributions shape
sns.violinplot(data=df, x='Department', y='Salary', hue='Gender', split=True, inner='quart', ax=ax[1], palette='pastel')
# Set title for violin plot
ax[1].set_title("Salary Distribution by Gender")

```

---

### **Logical Step 3: Performance Grid (Catplot)**

**Explanation:** We want to investigate if more experienced employees have higher performance ratings. Since we have 3 departments, looking at one chart is messy. We will use `catplot` to create a **separate chart for each Department** automatically.

#### **Exercise 3: Experience vs Performance Grid**

```python
# Use sns.catplot (Figure-level function).
# Set x to 'Performance_Rating' and y to 'Years_Experience'.
# Group the columns by 'Department' (col).
# Color the points by 'Gender' (hue).
# Set kind='strip' (Strip plot shows all data points with some jitter).
# Set height=4 and aspect=0.8 to control size.

```

























#### **Solution 3**

```python
# Create a faceted grid of strip plots
sns.catplot(data=df, x='Performance_Rating', y='Years_Experience', 
            col='Department', hue='Gender', kind='strip', 
            height=4, aspect=0.8, palette='dark:b')

```

---

### **Logical Step 4: The Big Picture (Heatmap)**

**Explanation:** Finally, we want to know: "Does Money buy Happiness?" or "Does Experience equal Performance?". We will calculate the correlation between all numbers and visualize it as a **Heatmap**.

#### **Exercise 4: Correlation Matrix**

```python
# Calculate the correlation matrix of the numeric columns in 'df'.
# Store it in a variable named 'corr'.
# Create a figure of size 8x6.
# Create a heatmap using 'corr'.
# Set annot=True to write the numbers in the boxes.
# Set cmap='coolwarm' for the color scheme (Red=High correlation, Blue=Negative).
# Set linewidths=0.5 to draw lines between the boxes.

```

























#### **Solution 4**

```python
# Calculate correlations for numeric columns only
corr = df.select_dtypes(include='number').corr()
# Initialize figure size
plt.figure(figsize=(8, 6))
# Draw the heatmap with annotations
sns.heatmap(corr, annot=True, cmap='coolwarm', linewidths=0.5, fmt=".2f")
# Add title
plt.title("HR Correlation Matrix")

```

---

### **Final Assembly**

*Copy and paste the solution code from all steps above into this single cell to generate the full HR Dashboard.*

```python
# --- HR ANALYTICS DASHBOARD ---

# 1. HEADCOUNT & SATISFACTION (The Overview)
print("Generating Overview...")
# Create subplot layout
fig, ax = plt.subplots(1, 2, figsize=(14, 5))
# Plot Headcount
sns.countplot(data=df, x='Department', palette='viridis', ax=ax[0])
ax[0].set_title("Total Headcount by Department")
# Plot Satisfaction
sns.barplot(data=df, x='Department', y='Job_Satisfaction', hue='Gender', palette='viridis', ax=ax[1])
ax[1].set_title("Avg Job Satisfaction Score")
plt.show()

# 2. COMPENSATION ANALYSIS (The Fairness Check)
print("Generating Compensation Report...")
# Create subplot layout
fig, ax = plt.subplots(1, 2, figsize=(14, 6))
# Plot Boxplot for Outliers
sns.boxplot(data=df, x='Department', y='Salary', palette='Blues', ax=ax[0])
ax[0].set_title("Salary Outlier Detection")
# Plot Violin for Distribution Shape
sns.violinplot(data=df, x='Department', y='Salary', hue='Gender', 
               split=True, inner='quart', palette='Blues', ax=ax[1])
ax[1].set_title("Salary Distribution Shape")
plt.show()

# 3. PERFORMANCE GRID (The Deep Dive)
print("Generating Performance Grids...")
# Create Faceted Plot
g = sns.catplot(data=df, x='Performance_Rating', y='Years_Experience', 
            col='Department', hue='Gender', kind='strip', 
            height=4, aspect=0.9, palette='deep')
# Add a title to the Figure (adjusted for height)
g.fig.suptitle("Experience vs Performance by Dept", y=1.05)
plt.show()

# 4. CORRELATIONS (The Summary)
print("Generating Correlation Matrix...")
# Calculate Correlation
corr_matrix = df.select_dtypes(include='number').corr()
# Plot Heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(corr_matrix, annot=True, cmap='RdBu_r', linewidths=1)
plt.title("Metric Correlations")
plt.show()

```