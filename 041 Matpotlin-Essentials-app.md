# Lab: Matplotlib Essentials for Data Science

### Topics Covered:

1. **`matplotlib.pyplot`**: Quick plotting (Lines, Bars, Histograms, Scatters).
2. **`matplotlib.figure` & `axes**`: Structured layouts and the Object-Oriented interface.
3. **`matplotlib.colors` & `cm**`: Mapping data to colors and colormaps.
4. **`matplotlib.ticker` & `text**`: Customizing axis ticks and adding informative annotations.

---

### 0. Setup and Data Generation

*Run this cell first to create the data we will use for the exercises.*

```python
# Import the main plotting library
import matplotlib.pyplot as plt
# Import the color management module
import matplotlib.colors as mcolors
# Import the colormap reference
import matplotlib.cm as cm
# Import the tick configuration module
import matplotlib.ticker as ticker
# Import numpy for data generation
import numpy as np

# Create 50 points between 0 and 10 for lines
x = np.linspace(0, 10, 50)
# Calculate sine values for the y-axis
y = np.sin(x)
# Create categories for bar charts
categories = ['A', 'B', 'C', 'D']
# Create heights for bar charts
heights = [25, 40, 15, 30]
# Create 100 random points for scatter plots
rand_x = np.random.rand(100)
# Create 100 random points for the y-axis
rand_y = np.random.rand(100)
# Create 100 random values for color mapping
val_colors = np.random.rand(100)

print("Setup complete. Data is ready for plotting.")

```

---

### 1. `matplotlib.pyplot` (The Quick Interface)

**Concept:** This is the most common way to interact with Matplotlib. It provides simple functions to generate plots instantly. It is "state-based," meaning it keeps track of the current plot and applies changes to it.
**Use:** Perfect for quick data exploration and simple visualizations.

#### Sample Code

```python
# Create a new figure for the plot
plt.figure()
# Generate a line plot using x and y data
plt.plot(x, y)
# Add a title to the current plot
plt.title("Simple Line Plot")
# Display the final plot
plt.show()

```

#### Practice Cell

```python
# 1. Generate a bar chart using 'categories' and 'heights' plt.bar()


# 2. Add the title "Category Comparison"


# 3. Generate a scatter plot using 'rand_x' and 'rand_y' (plt.scatter(rand_x,rand_y)


# 4. Use plt.show() to see your results


```

---

### 2. `matplotlib.figure` and `matplotlib.axes` (Structured Layouts)

**Concept:** This is the "Object-Oriented" approach. Instead of letting Matplotlib handle the "current" plot, you explicitly create a **Figure** (the canvas) and **Axes** (the actual plot area).
**Use:** Essential for creating "Subplots" (multiple charts in one image) and for fine-grained control over layout.

#### Sample Code

```python
# Create a figure object (the container)
fig = plt.figure(figsize=(8, 4))
# Add an axes object at position 1 (1 row, 2 columns, index 1)
ax1 = fig.add_subplot(1, 2, 1)
# Add an axes object at position 2 (1 row, 2 columns, index 2)
ax2 = fig.add_subplot(1, 2, 2)
# Draw a line on the first axes
ax1.plot(x, y)
# Draw a histogram on the second axes
ax2.hist(rand_x, bins=10)
# Display the figure containing both plots
plt.show()

```

#### Practice Cell

```python
# 1. Create a figure named 'my_fig' with a specific size


# 2. Add one subplot named 'ax' to the figure


# 3. Use ax.bar(categories, heights) to create a bar chart


# 4. Use plt.show() to render the figure


```

---

### 3. `matplotlib.colors` and `matplotlib.cm` (Color Mapping)

**Concept:** Colors aren't just for decoration; they can represent a third dimension of data. `colors` allows you to define colors, and `cm` (Colormaps) provides preset gradients (like 'viridis' or 'magma').
**Use:** Used in scatter plots or heatmaps to show the intensity of a variable.

#### Sample Code

```python
# Create a new figure and axes
fig, ax = plt.subplots()
# Create a scatter plot where color 'c' is determined by 'val_colors' using the 'viridis' map
scatter = ax.scatter(rand_x, rand_y, c=val_colors, cmap=cm.viridis)
# Add a color bar to show what the colors represent
fig.colorbar(scatter)
# Display the plot
plt.show()

```

#### Practice Cell

```python
# 1. Create a scatter plot using rand_x and rand_y


# 2. Assign 'val_colors' to the 'c' parameter to color the dots


# 3. Set 'cmap' to 'plasma' or 'inferno'


# 4. Use plt.show() to see the color gradient


```

---

### 4. `matplotlib.ticker` and `matplotlib.text` (Customization)

**Concept:** `ticker` controls the markers on the X and Y axes (the numbers and dashes). `text` and `annotations` allow you to write notes directly on the chart to explain data points.
**Use:** Making charts readable for presentations by highlighting specific insights and fixing axis labels.

#### Sample Code

```python
# Create subplots and unpack them into fig and ax
fig, ax = plt.subplots()
# Plot the basic sine wave
ax.plot(x, y)
# Set the y-axis to show ticks every 0.5 units
ax.yaxis.set_major_locator(ticker.MultipleLocator(0.5))
# Place a text label at specific coordinates (x=5, y=0)
ax.text(5, 0, "Middle Point", fontsize=12, color='indigo')
# Create an arrow pointing to a specific data feature
ax.annotate('Peak', xy=(1.5, 1), xytext=(3, 1.2), arrowprops=dict(facecolor='black'))
# Display the customized plot
plt.show()

```

#### Practice Cell

```python
# 1. Plot the x and y data


# 2. Use ax.set_xlabel() and ax.set_ylabel() to name your axes


# 3. Add a text note at (2, 0.5) saying "Observation A"


# 4. Use plt.show()


```

---
