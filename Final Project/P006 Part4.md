## Lab 4: The Blueprint (Matplotlib Visualization)

In the previous lab, you structured your data into a clean Pandas DataFrame. Now, you will assume the role of a **Data Analyst** presenting technical findings to an engineering team. You will use **Matplotlib**, the foundation of Python visualization.

While other libraries (like Seaborn) are prettier, Matplotlib gives you granular control over every pixel—crucial for "Hard Science" and technical reporting.

### Detailed Requirements for Lab 4

1. **Data Aggregation for Plotting:** Group the data by "Hour" to calculate the average ridership trends throughout the day.
2. **The Canvas Setup:** Create a multi-panel figure (Subplots) containing two distinct charts side-by-side.
3. **Technical Line Chart:** Plot the "Ridership vs. Hour" trend using a line plot with markers.
4. **Comparative Bar Chart:** Plot the "Total Revenue by Transit Type" using a bar chart.
5. **Annotations & Formatting:** Add professional touches—gridlines, axis labels, specific titles, and an annotation pointing specifically to the "Peak Hour."

---

### Step 0: Setup & Data State

Since we are starting a new lab, run this block to recreate the clean `df_final` DataFrame from the end of Lab 3.

```python
import pandas as pd
import numpy as np

# Recreating the DataFrame from Lab 3 results
data = {
    'timestamp': pd.to_datetime(['2025-01-01 08:00:00', '2025-01-01 08:15:00', '2025-01-01 08:30:00', 
                                 '2025-01-01 09:00:00', '2025-01-01 09:15:00', '2025-01-01 09:30:00', 
                                 '2025-01-01 10:00:00', '2025-01-01 10:15:00', '2025-01-01 10:30:00', 
                                 '2025-01-01 11:00:00']),
    'transit_type': ['Bus', 'Metro', 'Bus', 'Metro', 'Metro', 'Bus', 'LightRail', 'Metro', 'Bus', 'Metro'],
    'passenger_count': [45, 120, 38, 310, 120, 55, 22, 150, 45, 280], # Imputed values included
    'revenue': [112.50, 360.00, 115.00, 930.00, 450.00, 137.50, 66.00, 450.00, 100.00, 840.00]
}
df_final = pd.DataFrame(data)
df_final['Hour'] = df_final['timestamp'].dt.hour
print("Setup Complete: 'df_final' is ready for plotting.")

```

---

### Step 1: Preparing Aggregated Data

Matplotlib needs simple lists or arrays to plot X vs Y. We cannot easily toss the whole raw DataFrame at it. We must prepare summary data first.

**Step Description:**
Create two specific datasets for our charts:

1. `hourly_trend`: The average `passenger_count` grouped by `Hour`.
2. `revenue_by_type`: The total `revenue` grouped by `transit_type`.

**Logic & Planning:**

```python
# Import the matplotlib pyplot module.
# Group the dataframe by 'Hour', calculate the mean of 'passenger_count', and reset the index.
# Group the dataframe by 'transit_type', sum the 'revenue', and reset the index.
# Sort the hourly trend data by 'Hour' to ensure the line plot connects correctly.
# Print the columns of the new dataframes to verify.

```

**Solution:**

```python
# Import the plotting module from matplotlib and give it the alias 'plt'
import matplotlib.pyplot as plt

# Group by 'Hour', take the mean of counts, and use reset_index to keep 'Hour' as a column
hourly_trend = df_final.groupby('Hour')['passenger_count'].mean().reset_index()

# Group by 'transit_type', sum the revenue, and reset index
revenue_by_type = df_final.groupby('transit_type')['revenue'].sum().reset_index()

# Sort the values by 'Hour' to ensure the time flows correctly from left to right
hourly_trend = hourly_trend.sort_values('Hour')

# Print the first few rows to confirm the data is ready for plotting
print(hourly_trend.head())

```

---

### Step 2: The Canvas (Subplots)

In technical reporting, we often need multiple charts in one image. We will create a "Figure" (the paper) and "Axes" (the individual plots).

**Step Description:**
Initialize a figure with 1 row and 2 columns. This gives us two empty plots side-by-side.

**Logic & Planning:**

```python
# Create a figure object and an array of axes objects (subplots) with 1 row and 2 columns.
# Set the overall figure size to be 12 inches wide by 5 inches tall.
# Add a main title to the entire figure (Super Title).
# Display the empty canvas.

```

**Solution:**

```python
# Use plt.subplots to create a figure with 1 row and 2 columns, setting size to 12x5
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

# Use suptitle to add a centered title above all subplots
fig.suptitle('Urban Transit Daily Analysis', fontsize=16)

# Show the plot to see the empty layout
plt.show()

```

---

### Step 3: Plotting the Data

Now we map our data to the axes `ax1` and `ax2`.

**Step Description:**

1. On the left plot (`ax1`), draw a **Line Chart** of Hour vs. Average Ridership.
2. On the right plot (`ax2`), draw a **Bar Chart** of Transit Type vs. Total Revenue.

**Logic & Planning:**

```python
# Re-create the figure and axes (needed because the previous cell closed the plot).
# On the first axis (ax1), plot 'Hour' on x and 'passenger_count' on y using a line plot.
# Set the title, x-label, and y-label for the first axis.
# Enable gridlines on the first axis for readability.
# On the second axis (ax2), plot 'transit_type' on x and 'revenue' on y using a bar chart.
# Set the title, x-label, and y-label for the second axis.
# Set the color of the bars to 'green'.

```

**Solution:**

```python
# Re-initialize the subplots since the previous 'plt.show()' closed the figure context
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))
fig.suptitle('Urban Transit Daily Analysis', fontsize=16)

# Plot x=Hour, y=Count on ax1 with markers 'o' and a dashed line style '--'
ax1.plot(hourly_trend['Hour'], hourly_trend['passenger_count'], marker='o', linestyle='--')
# Set the specific title for the left subplot
ax1.set_title('Average Ridership by Hour')
# Label the X-axis
ax1.set_xlabel('Hour of Day (24h)')
# Label the Y-axis
ax1.set_ylabel('Avg. Passengers')
# Add a grid to the background for easier reading of values
ax1.grid(True)

# Plot a bar chart on ax2 with x=Type, y=Revenue, setting color to green
ax2.bar(revenue_by_type['transit_type'], revenue_by_type['revenue'], color='green')
# Set the title for the right subplot
ax2.set_title('Total Revenue by Transit Mode')
# Label the X-axis
ax2.set_xlabel('Transit Type')
# Label the Y-axis
ax2.set_ylabel('Revenue ($)')

```

---

### Step 4: Adding Annotations (The "Insight")

A chart without insight is just a drawing. We will programmatically find the peak hour and point an arrow at it.

**Step Description:**
Find the hour with the maximum ridership in our data, and place an annotation on the chart pointing to that specific coordinate.

**Logic & Planning:**

```python
# Identify the row with the maximum passenger count.
# Extract the 'Hour' (x) and 'passenger_count' (y) values from that row.
# Use the annotate method on ax1 to draw an arrow pointing to that (x, y) coordinate.
# Set the text of the annotation to "Peak Traffic".
# Define the arrow properties (facecolor black, shrink factor).

```

**Solution:**

```python
# Find the row with the highest passenger count using iloc and argmax
peak_data = hourly_trend.loc[hourly_trend['passenger_count'].idxmax()]

# Extract the x (hour) and y (count) coordinates for the annotation
peak_x = peak_data['Hour']
peak_y = peak_data['passenger_count']

# Add an annotation to ax1 pointing to the peak_x, peak_y coordinates
ax1.annotate('Peak Traffic', xy=(peak_x, peak_y), xytext=(peak_x+0.5, peak_y+50),
             arrowprops=dict(facecolor='black', shrink=0.05))

# Use tight_layout to automatically adjust subplot params so titles don't overlap
plt.tight_layout()

# Display the final composed figure
plt.show()

```

---

### Final Instructions: Run the Application

Copy the code below to generate the complete technical report.

```python
import matplotlib.pyplot as plt

# 1. Prepare Data
hourly_trend = df_final.groupby('Hour')['passenger_count'].mean().reset_index().sort_values('Hour')
revenue_by_type = df_final.groupby('transit_type')['revenue'].sum().reset_index()

# 2. Setup Figure
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 6))
fig.suptitle('Urban Transit Technical Report', fontsize=16, fontweight='bold')

# 3. Left Plot: Hourly Trend (Line)
ax1.plot(hourly_trend['Hour'], hourly_trend['passenger_count'], color='blue', marker='o', linestyle='-')
ax1.set_title('Hourly Passenger Load')
ax1.set_xlabel('Hour (24h)')
ax1.set_ylabel('Avg Passengers')
ax1.grid(True, linestyle='--', alpha=0.7)

# Annotation Logic
peak_row = hourly_trend.loc[hourly_trend['passenger_count'].idxmax()]
ax1.annotate(f'Peak: {int(peak_row["passenger_count"])}', 
             xy=(peak_row['Hour'], peak_row['passenger_count']), 
             xytext=(peak_row['Hour']+0.5, peak_row['passenger_count']+20),
             arrowprops=dict(facecolor='red', shrink=0.05))

# 4. Right Plot: Revenue (Bar)
ax2.bar(revenue_by_type['transit_type'], revenue_by_type['revenue'], color=['#2ca02c', '#1f77b4', '#ff7f0e'])
ax2.set_title('Revenue Distribution')
ax2.set_xlabel('Transit Mode')
ax2.set_ylabel('Total Revenue ($)')
ax2.grid(axis='y', alpha=0.5)

# 5. Finalize
plt.tight_layout()
plt.show() # In a real job, you might use plt.savefig('report.png')

```
