# **Project: Satellite Image Reconstruction System**

**Time:** ~1 Hour
**Objective:** Build a data pipeline that takes raw streams of numbers from a satellite, reshapes them into image "tiles," stitches them together into a complete map, and splits them for regional analysis.

**Scenario:**
You are working for a space agency. A satellite sends data down in long, 1-dimensional streams. Your job is to:

1. **Receive** raw data streams (Create Arrays).
2. **Format** them into 2D square tiles (Reshape).
3. **Assemble** a full map from these tiles (Concatenate/Stack).
4. **Slice** the map into specific regions for different teams to analyze (Split).

---

## **Step 1: Ingesting & Formatting Sensor Data**

**Logical Step:**
The satellite sends data as a simple list of numbers. We need to convert this list into a NumPy array and then `reshape` it into a 4x4 grid (a "Tile"). We will simulate two separate sensors: "Sensor A" (numbers 0-15) and "Sensor B" (numbers 16-31).

**Student Task:**

```python
import numpy as np

# 1. Create a list 'stream_a' containing numbers 0 to 15 (use standard python range or just list logic)


# 2. Convert 'stream_a' into a numpy array called 'arr_a'


# 3. Create a numpy array 'arr_b' containing numbers 16 to 31 (Try using np.arange(16, 32) for a shortcut)


# 4. Reshape 'arr_a' into a 4x4 matrix called 'tile_1'


# 5. Reshape 'arr_b' into a 4x4 matrix called 'tile_2'


# 6. Print both tiles to see the grids


```

**Solution:**

```python
import numpy as np

# 1. Create list (Using range is easiest)
stream_a = list(range(16))

# 2. Convert to array
arr_a = np.array(stream_a)

# 3. Create second array directly
arr_b = np.arange(16, 32)

# 4. Reshape into 4x4
tile_1 = arr_a.reshape(4, 4)

# 5. Reshape into 4x4
tile_2 = arr_b.reshape(4, 4)

# 6. Print
print("Tile 1:\n", tile_1)
print("\nTile 2:\n", tile_2)

```

---

## **Step 2: Assembling the Map (Stitching)**

**Logical Step:**
Now we have two 4x4 tiles. We want to combine them to create a wider view.
First, we will join `tile_1` and `tile_2` side-by-side (Horizontally) to create an 8-column strip.
Then, to simulate a full map, we will take this strip and stack it on top of itself (Vertically) to create a large square map.

**Student Task:**

```python
# 1. Stack 'tile_1' and 'tile_2' horizontally (side-by-side) using np.hstack() or np.concatenate with axis=1.
#    Call this 'top_strip'.


# 2. Print the shape of 'top_strip'. It should be (4, 8).


# 3. Create a 'bottom_strip' that is identical to 'top_strip' (Just assign top_strip to it, or copy it).


# 4. Stack 'top_strip' and 'bottom_strip' vertically (one on top of other) using np.vstack().
#    Call this 'full_map'.


# 5. Print the 'full_map' and its shape. It should be (8, 8).


```

**Solution:**

```python
# 1. Horizontal Stack
top_strip = np.hstack((tile_1, tile_2))

# 2. Check Shape
print(f"Top Strip Shape: {top_strip.shape}")

# 3. Create bottom strip (For simulation, we use the same data)
bottom_strip = top_strip.copy()

# 4. Vertical Stack
full_map = np.vstack((top_strip, bottom_strip))

# 5. Print Result
print("\nFull Map Shape:", full_map.shape)
print(full_map)

```

---

## **Step 3: Distributing Data (Splitting)**

**Logical Step:**
The assembled map is too big for one analyst to check. We need to split the `full_map` (which is 8 rows high) into 2 separate regions: "North Region" (Top 4 rows) and "South Region" (Bottom 4 rows).
We will use `np.split` (or `np.vsplit`) to cut the array horizontally.

**Student Task:**

```python
# 1. Split 'full_map' into 2 equal subarrays along the vertical axis (rows) using np.vsplit() or np.split().
#    Store the result in a variable called 'regions'.


# 2. Assign the first item in 'regions' to 'north_region' and the second to 'south_region'.


# 3. Print the shape of 'north_region' to verify it is (4, 8).


# 4. Print the first row of 'north_region' to verify the data.


```

**Solution:**

```python
# 1. Split into 2 parts
regions = np.vsplit(full_map, 2)

# 2. Assign variables
north_region = regions[0]
south_region = regions[1]

# 3. Verify Shape
print(f"North Region Shape: {north_region.shape}")

# 4. Verify Data
print("First row of North Region:", north_region[0])

```

---

## **Step 4: The Final Application**

**Logical Step:**
We will encapsulate this entire logic into a single function called `process_satellite_data()`. This simulates a real-world pipeline: Data comes in -> Process -> Data goes out.

**Student Task:**

```python
def process_satellite_data(raw_list_a, raw_list_b):
    # 1. Convert both input lists to numpy arrays
    
    # 2. Reshape both into 4x4 tiles (Assuming inputs are always length 16)
    
    # 3. Horizontal Stack the two tiles to make a strip
    
    # 4. Vertical Stack the strip with itself to make a full map
    
    # 5. Split the map vertically into 2 regions
    
    # 6. Return the "North" region (the top half)
    pass # Remove this pass

# Test the App
# Create dummy data
data_1 = list(range(16))       # 0..15
data_2 = list(range(16, 32))   # 16..31

# Run the pipeline
# result_map = process_satellite_data(data_1, data_2)
# print("Processed Region Shape:", result_map.shape)
# print(result_map)

```

**Solution:**

```python
def process_satellite_data(raw_list_a, raw_list_b):
    # 1. Convert
    arr_a = np.array(raw_list_a)
    arr_b = np.array(raw_list_b)
    
    # 2. Reshape
    tile_a = arr_a.reshape(4, 4)
    tile_b = arr_b.reshape(4, 4)
    
    # 3. Stitch Horizontally
    strip = np.hstack((tile_a, tile_b))
    
    # 4. Stitch Vertically (Full Map)
    full_map = np.vstack((strip, strip))
    
    # 5. Split
    regions = np.vsplit(full_map, 2)
    
    # 6. Return North
    return regions[0]

# Test Data
data_1 = list(range(16))
data_2 = list(range(16, 32))

# Run
result_map = process_satellite_data(data_1, data_2)
print("Processed Region Shape:", result_map.shape)
print("Map Data:\n", result_map)

```