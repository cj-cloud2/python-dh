# **Project Lab: The Market Research Dashboard**

**Time Allocation:** 60 Minutes

### **The End Goal**

You have been hired by a startup to analyze their customer data. They want a single dashboard that tells the story of who their customers are and how they spend money. You will build a script that generates:

1. **Spending Power Analysis:** A scatter plot showing the relationship between income and spending score, segmented by age group.
2. **Sales Trends:** A line plot showing how sales have evolved over time, with confidence intervals.
3. **Customer Distribution:** A complex distribution plot (Histogram + KDE) showing the age spread of customers.
4. **Multi-View Analysis:** A grid of charts comparing spending behavior across different regions using `relplot`.

### **Requirements**

* Use `seaborn.scatterplot` to visualize bivariate relationships (Income vs. Spending).
* Use `seaborn.lineplot` to visualize trends (Date vs. Sales).
* Use `seaborn.displot` or `histplot` to visualize univariate distributions (Age).
* Use `seaborn.relplot` to create a multi-column figure (FacetGrid) for regional analysis.
* Apply `hue` and `style` to add depth to your charts.

---

### **0. Setup: Create the Market Data**

*Run this cell first. It generates the synthetic customer dataset we will use.*

```python
# Import seaborn for plotting
import seaborn as sns
# Import pandas for data manipulation
import pandas as pd
# Import numpy for random number generation
import numpy as np
# Import matplotlib for final display settings
import matplotlib.pyplot as plt

# Set the visual theme to 'whitegrid' for a clean look
sns.set_theme(style="whitegrid")

# Create a sample dataset of 500 customers
n = 500
# Generate random ages between 18 and 70
ages = np.random.randint(18, 70, n)
# Generate incomes (correlated with age somewhat)
incomes = ages * 1000 + np.random.normal(0, 10000, n)
# Generate spending scores (1-100)
spending_score = np.random.randint(1, 100, n)
# Assign regions randomly
regions = np.random.choice(['North', 'South', 'East', 'West'], n)
# Assign membership status
membership = np.random.choice(['Gold', 'Silver', 'Bronze'], n)

# Create a DataFrame
df = pd.DataFrame({
    'Age': ages,
    'Annual_Income': incomes,
    'Spending_Score': spending_score,
    'Region': regions,
    'Membership': membership
})

# Create a second DataFrame for Time Series (Trends)
dates = pd.date_range(start='2024-01-01', periods=100)
# Generate daily sales data with some random fluctuation
sales = np.linspace(100, 500, 100) + np.random.normal(0, 50, 100)
# Create the trends DataFrame
trend_df = pd.DataFrame({'Date': dates, 'Daily_Sales': sales})

print("Data Loaded: 'df' (Customers) and 'trend_df' (Sales) are ready.")

```

---

### **Logical Step 1: Understanding the Customer Base (Distributions)**

**Explanation:** Before we look at money, we need to know *who* the customers are. We will use a Distribution Plot to visualize the Age of our customers. We want to see a Histogram (for counts) overlaid with a KDE (for shape).

#### **Exercise 1: Customer Age Distribution**

```python
# Create a figure-level distribution plot using 'df'.
# Set x-axis to 'Age'.
# Enable the Kernel Density Estimate (kde=True).
# Color the bars based on 'Membership' status (hue).
# Separate the charts into columns based on 'Region' (col).
# Set the bin width to 5 years (binwidth=5).

```

























#### **Solution 1**

```python
# Create a distribution plot showing Age, colored by Membership, and split by Region
sns.displot(data=df, x='Age', kde=True, hue='Membership', col='Region', binwidth=5)

```

---

### **Logical Step 2: Income vs. Spending (Relational Scatter)**

**Explanation:** Now we want to answer the big question: "Do richer people spend more?" We will use a Scatter Plot to compare `Annual_Income` and `Spending_Score`. We will use `hue` to differentiate between Gold/Silver/Bronze members and `style` to differentiate Regions.

#### **Exercise 2: The Spending Power Scatter**

```python
# Create a matplotlib figure with a specific size (10x6).
# Create a scatterplot using the 'df' dataset.
# Set x to 'Annual_Income' and y to 'Spending_Score'.
# Map the point colors (hue) to 'Membership'.
# Map the point shapes (style) to 'Region'.
# Set the size of the points to be slightly larger (s=100).
# Add a title "Income vs Spending Analysis".

```

























#### **Solution 2**

```python
# Initialize a matplotlib figure to control the size
plt.figure(figsize=(10, 6))
# Draw a scatter plot with semantic mappings for hue and style
sns.scatterplot(data=df, x='Annual_Income', y='Spending_Score', hue='Membership', style='Region', s=100)
# Add a descriptive title
plt.title("Income vs Spending Analysis")

```

---

### **Logical Step 3: Sales Trends Over Time (Line Plots)**

**Explanation:** Management needs to know if sales are going up or down. We will use `lineplot` to visualize the `trend_df`. Seaborn's `lineplot` is powerful because if we had multiple data points for the same day, it would automatically draw a confidence interval (shadow) around the line.

#### **Exercise 3: The Sales Trend**

```python
# Create a new figure (figsize 12x4).
# Create a line plot using 'trend_df'.
# Set x to 'Date' and y to 'Daily_Sales'.
# Change the line color to 'green'.
# Add markers to the line (marker='o').
# Add a title "Daily Sales Trend (2024)".

```

























#### **Solution 3**

```python
# Set up the figure size for a wide trend chart
plt.figure(figsize=(12, 4))
# Plot the line chart for sales over time
sns.lineplot(data=trend_df, x='Date', y='Daily_Sales', color='green', marker='o')
# Set the title
plt.title("Daily Sales Trend (2024)")

```

---

### **Logical Step 4: Complex Regional Analysis (RelPlot)**

**Explanation:** Sometimes a single chart is too crowded. We want to see the Income/Spending relationship again, but this time, we want a **separate chart for each Membership Tier**. We will use `relplot` (Relational Plot) which is built exactly for this kind of "Facet Grid" layout.

#### **Exercise 4: The Membership Facet Grid**

```python
# Use sns.relplot (figure-level function) with 'df'.
# Set x='Annual_Income' and y='Spending_Score'.
# Split the charts into columns based on 'Membership' (col='Membership').
# Color the points based on 'Region' (hue='Region').
# Use 'kind' to specify this should be a 'scatter' plot.
# Adjust the height of the charts to 5 inches.

```

























#### **Solution 4**

```python
# Create a grid of scatter plots, one for each Membership type
sns.relplot(data=df, x='Annual_Income', y='Spending_Score', col='Membership', hue='Region', kind='scatter', height=5)

```

---

### **Final Assembly**

*Copy and paste the solution code from all steps above into this single cell to run your full Market Research Report.*

```python
# --- MARKET RESEARCH DASHBOARD ---

# 1. DISTRIBUTION ANALYSIS (Age Demographics)
print("Generating Demographics Report...")
# Show distribution of age, broken down by region and membership
sns.displot(data=df, x='Age', kde=True, hue='Membership', col='Region', height=4, aspect=0.8)
plt.show() # Force render of the figure-level plot

# 2. BIVARIATE ANALYSIS (Spending Power)
print("Generating Spending Power Report...")
# Set figure size for the scatter plot
plt.figure(figsize=(10, 6))
# Create detailed scatter plot
sns.scatterplot(data=df, x='Annual_Income', y='Spending_Score', hue='Membership', style='Region', s=100, alpha=0.7)
# Add title
plt.title("Income vs. Spending Score by Membership")
# Move legend outside the box
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()

# 3. TREND ANALYSIS (Time Series)
print("Generating Sales Trend Report...")
# Set figure size for trend line
plt.figure(figsize=(12, 4))
# Plot sales trend with markers
sns.lineplot(data=trend_df, x='Date', y='Daily_Sales', color='teal', linewidth=2.5)
# Add title
plt.title("2024 Sales Trajectory (Confidence Interval included)")
plt.show()

# 4. FACET GRID ANALYSIS (Deep Dive)
print("Generating Deep Dive Report...")
# Create a side-by-side comparison of membership tiers
sns.relplot(data=df, x='Annual_Income', y='Spending_Score', 
            col='Membership', hue='Region', 
            kind='scatter', size='Age', sizes=(20, 200),
            palette='viridis', height=5)
plt.show()

```