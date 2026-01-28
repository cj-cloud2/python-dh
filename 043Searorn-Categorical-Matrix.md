# **Lab Sheet: Seaborn Categorical & Matrix Plots**

**Objective:** Learn to visualize non-numeric (categorical) data and complex matrices. While histograms show distribution for *one* variable, these plots allow you to compare distributions *across* different groups (e.g., Salary distribution *by* Department).

**Topics Covered:**

1. **Categorical Estimates (`barplot`, `countplot`)**: Calculating and visualizing aggregates (means, counts) for categories.
2. **Categorical Distributions (`boxplot`, `violinplot`)**: Visualizing spread, quartiles, and outliers per category.
3. **Figure-Level Interface (`catplot`)**: The unified interface for creating any categorical plot with subplot support.
4. **Matrix Plots (`heatmap`)**: Visualizing correlations and data matrices using color intensity.

---

### **0. Setup and Data Creation**

*Run this cell first to generate the sample dataset we will use for the lab.*

```python
# Import the seaborn library for statistical plotting
import seaborn as sns
# Import pandas for handling data frames
import pandas as pd
# Import numpy for random number generation
import numpy as np
# Import matplotlib to display the final plots
import matplotlib.pyplot as plt

# Set the visual theme to seaborn's default style
sns.set_theme(style="whitegrid")

# --- DATA GENERATION ---
# Set seed for reproducibility
np.random.seed(101)
# Number of employees
n = 300
# Generate Random Data
data = {
    'Department': np.random.choice(['Sales', 'HR', 'IT', 'Marketing'], n),
    'Gender': np.random.choice(['Male', 'Female'], n),
    'Performance_Rating': np.random.randint(1, 6, n), # 1 to 5 stars
    'Years_Experience': np.random.randint(1, 15, n),
    'Salary': np.nan # Placeholder
}
# Create DataFrame
df = pd.DataFrame(data)

# Generate salary based on experience + noise (to create correlation)
df['Salary'] = 40000 + (df['Years_Experience'] * 2000) + np.random.normal(0, 5000, n)
# Add outlier to IT department for boxplot demonstration
df.loc[0, 'Salary'] = 150000
df.loc[0, 'Department'] = 'IT'

print("Setup Complete. Employee DataFrame 'df' created.")
print(df.head())

```

---

### **1. Categorical Estimates: `barplot()` and `countplot()**`

**Concept:**

* **`seaborn.barplot()`**: Displays the **mean** (average) of a numeric variable for each category. It automatically draws error bars showing the confidence interval.
* **`seaborn.countplot()`**: A special case of a bar plot that only counts the number of occurrences. (Like a histogram, but for categories).

#### **Sample Code**

```python
# Create a figure with 2 subplots (1 row, 2 columns)
fig, ax = plt.subplots(1, 2, figsize=(12, 5))

# 1. Bar Plot: Average Salary by Department
# 'estimator' defaults to mean. It calculates average salary per Dept.
sns.barplot(data=df, x='Department', y='Salary', ax=ax[0], palette='viridis')
# Set title for the first plot
ax[0].set_title("Average Salary by Dept")

# 2. Count Plot: Number of Employees per Department
# No 'y' variable needed, it just counts rows.
sns.countplot(data=df, x='Department', ax=ax[1], palette='pastel')
# Set title for the second plot
ax[1].set_title("Employee Count by Dept")

# Display the plots
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 1: Estimates and Counts
# ---------------------------------------------------------

# 1. Create a barplot showing Average 'Performance_Rating' (y) by 'Gender' (x).


# 2. Create a countplot showing how many employees have each 'Performance_Rating' (x).


# 3. (Optional) Try adding 'hue'='Gender' to the countplot to split the bars.


# 4. Use plt.show() to render.


```

---

### **2. Categorical Distributions: `boxplot()` and `violinplot()**`

**Concept:**

* **`seaborn.boxplot()`**: Shows the "Five Number Summary" (Minimum, First Quartile, Median, Third Quartile, Maximum). It is excellent for detecting **outliers** (points beyond the whiskers).
* **`seaborn.violinplot()`**: Combines a boxplot with a KDE (density curve). It shows the shape of the distribution (where the data is "fat" or "thin").

#### **Sample Code**

```python
# Create a figure for side-by-side comparison
fig, ax = plt.subplots(1, 2, figsize=(14, 6))

# 1. Boxplot: Salary Distribution by Department
# Dots outside the whiskers represent outliers (anomalies)
sns.boxplot(data=df, x='Department', y='Salary', ax=ax[0])

# 2. Violinplot: Salary Distribution by Department
# The width represents the density of employees at that salary level
sns.violinplot(data=df, x='Department', y='Salary', ax=ax[1], hue='Gender', split=True)

# Display the plots
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 2: Box and Violin Plots
# ---------------------------------------------------------

# 1. Create a boxplot for 'Years_Experience' (y) grouped by 'Department' (x).


# 2. Create a violinplot for 'Performance_Rating' (y) grouped by 'Gender' (x).


# 3. In the boxplot code, try setting 'showfliers=False' to hide outliers.


# 4. Use plt.show()


```

---

### **3. Figure-Level Interface: `catplot()**`

**Concept:**

* **`seaborn.catplot()`**: This is the "master" function for categorical plots.
* Instead of separate functions, you use `catplot` and specify `kind='bar'`, `kind='box'`, `kind='violin'`, etc.
* **Superpower**: It can create subplots automatically using the `col` parameter (Faceting).

#### **Sample Code**

```python
# Create a faceted plot using catplot
# kind='strip' creates a jittered scatter plot (good for seeing all points)
# col='Department' creates a separate chart for every department automatically
sns.catplot(data=df, x='Gender', y='Salary', kind='strip', col='Department', col_wrap=2)

# Create a boxplot using catplot
# We simply change 'kind' to 'box'
sns.catplot(data=df, x='Department', y='Salary', kind='box', hue='Gender')

# Display plots
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 3: The catplot Interface
# ---------------------------------------------------------

# 1. Use sns.catplot to create a 'bar' chart (kind='bar').


# 2. Map 'Gender' to x and 'Salary' to y.


# 3. Use 'col'='Department' to split the charts into columns.


# 4. Run the code to see 4 separate bar charts.


```

---

### **4. Matrix Plots: `heatmap()**`

**Concept:**

* **`seaborn.heatmap()`**: Visualizes a matrix of numbers where the value is represented by color intensity.
* **Correlation Matrix**: The most common use case. It shows how strongly pairs of variables are related (1.0 = perfect positive correlation, -1.0 = perfect negative).

#### **Sample Code**

```python
# First, calculate the correlation matrix for numeric columns only
# This creates a square table showing how variables relate to each other
corr_matrix = df.select_dtypes(include='number').corr()

# Create a figure
plt.figure(figsize=(8, 6))

# Draw the heatmap
# 'annot=True' writes the actual number in the box
# 'cmap' sets the color scheme (coolwarm is standard for correlation)
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', fmt=".2f")

# Add a title
plt.title("Correlation Matrix: Experience vs Salary vs Rating")
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 4: Heatmaps
# ---------------------------------------------------------

# 1. Create a pivot table: Average Salary for every Department/Gender combination
# (Run this line: pivot = df.pivot_table(index='Department', columns='Gender', values='Salary') )


# 2. Create a heatmap using this 'pivot' variable.


# 3. Set 'annot=True' to see the salary numbers.


# 4. Set 'cmap' to 'Greens' to see money-themed colors.


```