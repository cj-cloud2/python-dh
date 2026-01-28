# **Lab Sheet: Seaborn Essentials (Relational & Distribution)**

**Objective:** Learn to visualize statistical relationships and data distributions using Seaborn. Unlike Matplotlib, Seaborn handles complex data structures (DataFrames) and statistical aggregation automatically.

**Topics Covered:**

1. **Relational Plots (`relplot`, `scatterplot`)**: Visualizing how two numeric variables relate to each other using semantic mappings like `hue` and `style`.
2. **Line Plots (`lineplot`)**: Visualizing trends over time with automatic confidence intervals.
3. **Distribution Basics (`histplot`, `kdeplot`)**: Understanding the spread of data using Histograms and Kernel Density Estimation.
4. **Figure-Level Distributions (`displot`)**: A unified interface for creating histograms, KDEs, and ECDFs.

---

### **0. Setup and Data Creation**

*Run this cell first to generate the sample dataset we will use for the lab.*

```python
# Import the seaborn library for statistical plotting
import seaborn as sns
# Import pandas for handling data frames
import pandas as pd
# Import numpy for generating random numbers
import numpy as np
# Import matplotlib to display the final plots
import matplotlib.pyplot as plt

# Set the visual theme to seaborn's default style
sns.set_theme(style="darkgrid")

# --- DATA GENERATION ---
# Set seed for reproducibility
np.random.seed(42)
# Generate 200 rows of data
n = 200
# Create a dictionary of lists to form our dataset
data = {
    'day_index': np.arange(n),
    'total_bill': np.random.normal(20, 5, n),   # Numeric: Bill amount
    'tip': np.random.normal(3, 1, n),           # Numeric: Tip amount
    'group_size': np.random.randint(1, 6, n),   # Numeric: Size of group
    'time': np.random.choice(['Lunch', 'Dinner'], n), # Categorical: Time of day
    'customer_type': np.random.choice(['Regular', 'New'], n) # Categorical: Type
}
# Convert the dictionary into a Pandas DataFrame
df = pd.DataFrame(data)
# Add a relationship: tip is roughly 15% of bill plus noise
df['tip'] = df['total_bill'] * 0.15 + np.random.normal(0, 0.5, n)

print("Setup Complete. DataFrame 'df' created.")
print(df.head())

```

---

### **1. Relational Plots: `scatterplot()` and `relplot()**`

**Concept:**

* **`scatterplot()`**: Draws points to show the relationship between two numeric variables (Bivariate analysis).
* **`relplot()`**: A "Figure-level" function. It can create scatter plots but also allows you to split charts into multiple subplots (columns/rows) easily.
* **Semantic Grouping (`hue`, `style`)**: We use color (`hue`) or shape (`style`) to add a 3rd or 4th dimension to the 2D chart (e.g., coloring points based on "Lunch" vs "Dinner").

#### **Sample Code**

```python
# Create a simple scatter plot using the DataFrame 'df'
sns.scatterplot(data=df, x='total_bill', y='tip')

# Create a complex relational plot with semantic groupings
# 'kind' sets the type of plot (scatter or line)
# 'hue' colors points by 'time' (Lunch vs Dinner)
# 'style' changes marker shapes by 'customer_type'
sns.relplot(data=df, x='total_bill', y='tip', kind='scatter', hue='time', style='customer_type')

# Display the plots
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 1: Relational Plots
# ---------------------------------------------------------

# 1. Create a basic scatterplot comparing 'total_bill' (x) and 'group_size' (y).


# 2. Use sns.relplot() to plot 'total_bill' vs 'tip'.


# 3. Inside relplot, use 'hue' to color the dots based on 'customer_type'.


# 4. (Optional) Try adding 'size'='group_size' to make the dots bigger for larger groups.


```

---

### **2. Line Plots: `lineplot()**`

**Concept:**

* **`lineplot()`**: Best for tracking changes over a sequence (like time).
* **Aggregation**: If there are multiple values for a single x-point (e.g., multiple sales on "Day 1"), Seaborn automatically calculates the **mean** (solid line) and the **confidence interval** (shaded area around the line).

#### **Sample Code**

```python
# Create a line plot showing the trend of tips over the 'day_index'
# 'markevery' adds a marker every 20 data points to make it readable
sns.lineplot(data=df, x='day_index', y='tip', markevery=20)

# Create a line plot showing the relationship between group_size and total_bill
# Seaborn automatically aggregates: it shows the AVERAGE bill for group size 1, 2, 3, etc.
# The shaded area represents the uncertainty (confidence interval)
sns.lineplot(data=df, x='group_size', y='total_bill')

# Display the plot
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 2: Line Plots & Trends
# ---------------------------------------------------------

# 1. Create a line plot with 'day_index' on x-axis and 'total_bill' on y-axis.


# 2. Create another line plot comparing 'group_size' (x) vs 'tip' (y).


# 3. Observe the shaded region. What does it represent? (Write a comment below).


# 4. Add 'hue'='time' to the line plot to see if Lunch trends differ from Dinner trends.


```

---

### **3. Distribution Basics: `histplot()` and `kdeplot()**`

**Concept:**

* **`histplot()`**: Draws a histogram (bars) to show counts of data in bins. Good for seeing where most data falls.
* **`kdeplot()`**: (Kernel Density Estimate) Draws a smooth curve representing the probability density. Good for seeing the "shape" of the data.
* **Rugs**: Small tick marks at the bottom of the chart showing exact data points.

#### **Sample Code**

```python
# Create a histogram to see the distribution of 'total_bill'
# 'kde=True' adds a smooth curve on top of the bars
sns.histplot(data=df, x='total_bill', kde=True, bins=20)

# Create a pure density plot for 'tip'
# 'fill=True' colors the area under the curve
sns.kdeplot(data=df, x='tip', fill=True)

# Display the plots
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 3: Histograms and Density
# ---------------------------------------------------------

# 1. Create a histogram (histplot) for the 'tip' column.


# 2. Set 'bins' to 10 inside the histplot function.


# 3. Create a KDE plot (kdeplot) for 'total_bill'.


# 4. Add 'hue'='time' to the kdeplot to compare Lunch vs Dinner distributions.


```

---

### **4. Figure-Level Distributions: `displot()**`

**Concept:**

* **`displot()`**: The master function for distributions. It can draw histograms, KDEs, or ECDFs (Empirical Cumulative Distribution Functions) by changing the `kind` parameter.
* It is designed to create multiple subplots easily using `col` or `row`.

#### **Sample Code**

```python
# Create a distribution plot (histogram by default)
# 'col' creates a separate chart for each 'time' category (Lunch vs Dinner)
sns.displot(data=df, x='total_bill', col='time', kde=True)

# Create an ECDF plot (shows proportion of data below a value)
# 'kind' parameter changes the plot type to 'ecdf'
sns.displot(data=df, x='total_bill', kind='ecdf', hue='customer_type')

# Display the plots
plt.show()

```

#### **Practice Area**

```python
# PRACTICE 4: Advanced Distributions
# ---------------------------------------------------------

# 1. Use sns.displot() to analyze 'tip'.


# 2. Use 'col'='customer_type' to split the chart into two side-by-side plots.


# 3. Change the 'kind' to 'kde' to see smooth curves instead of bars.


# 4. Run the code and analyze: Do Regular customers tip differently than New ones?


```