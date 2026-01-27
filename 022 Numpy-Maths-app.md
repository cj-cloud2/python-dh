# **Project: The Industrial Sensor Health Monitor**

**Time:** ~1 Hour
**Objective:** Build a complete data pipeline that simulates a vibrating machine, analyzes its signal frequencies, and calculates a safety score using matrix operations.

**Scenario:**
You are a Data Scientist at a manufacturing plant. You have a vibration sensor on a critical motor.

1. The motor vibrates at a specific "Safe Frequency" (50Hz).
2. The factory floor is noisy (random interference).
3. **Your Goal:**
* Simulate the sensor data (Signal + Noise).
* Use **FFT** to extract the dominant frequencies.
* Use **Linear Algebra** to calculate a weighted "Health Score" to decide if the machine needs maintenance.



---

## **Step 1: Setup & Data Simulation**

**Logical Step:**
First, we need to generate our data. We will use `numpy.math` to create a perfect "Sine Wave" representing the motor's vibration. Then, we will use `numpy.random` to generate "White Noise" (random static) and add it to our clean signal.

**Student Task:**

```python
import numpy as np
import matplotlib.pyplot as plt # Optional, just for visualizing if you know how

# 1. Define a time array 't' from 0 to 1 second with 1000 steps (use np.linspace or math logic)


# 2. Define the motor's frequency as 50 (Hz)


# 3. Create the 'clean_signal' using np.sin(), 2 * pi, frequency, and time 't'


# 4. Set a random seed (e.g., 42) for reproducibility


# 5. Create 'noise' array of same shape as 't' using np.random.normal() (mean=0, std_dev=2)


# 6. Create 'sensor_data' by adding 'clean_signal' + 'noise'


# 7. Print the first 5 values of 'sensor_data'


```

**Solution:**

```python
import numpy as np

# 1. Define a time array 't' from 0 to 1 second with 1000 steps
t = np.linspace(0, 1, 1000)

# 2. Define the motor's frequency as 50 (Hz)
freq = 50

# 3. Create the 'clean_signal' using np.sin(), 2 * pi, frequency, and time 't'
clean_signal = np.sin(2 * np.pi * freq * t)

# 4. Set a random seed
np.random.seed(42)

# 5. Create 'noise' array using np.random.normal()
noise = np.random.normal(0, 2, 1000)

# 6. Create 'sensor_data' by adding 'clean_signal' + 'noise'
sensor_data = clean_signal + noise

# 7. Print the first 5 values
print("First 5 sensor readings:", sensor_data[:5])

```

---

## **Step 2: Frequency Analysis (FFT)**

**Logical Step:**
The `sensor_data` looks messy because of the noise. We need to find out what the *dominant* frequency is (it should be 50Hz). We will use `numpy.fft` (Fast Fourier Transform) to convert our Time data into Frequency data.

**Student Task:**

```python
# 1. Compute the FFT of the 'sensor_data' using np.fft.fft()


# 2. Calculate the magnitudes (absolute values) of the complex FFT result using np.abs()


# 3. Find the index of the maximum value in the magnitudes array using np.argmax()
#    (This tells us which frequency is the strongest)


# 4. Print the index of the dominant frequency


```

**Solution:**

```python
# 1. Compute the FFT of the 'sensor_data'
fft_spectrum = np.fft.fft(sensor_data)

# 2. Calculate the magnitudes (absolute values)
magnitudes = np.abs(fft_spectrum)

# 3. Find the index of the maximum value
# Note: For real data, the first half of the array contains the positive frequencies
dominant_freq_index = np.argmax(magnitudes[:500]) 

# 4. Print the index
print(f"Dominant Frequency Detected: {dominant_freq_index} Hz")

```

---

## **Step 3: Risk Calculation (Linear Algebra)**

**Logical Step:**
Now we need to calculate a "Health Score". Imagine we have a safety model that weighs different statistical properties of the signal.
We will create a **Feature Vector** (Mean, Std Dev, Max) and a **Weight Vector** (how important each feature is). We will use the **Dot Product** (`numpy.linalg`) to calculate the final risk score.

**Student Task:**

```python
# 1. Extract features: Calculate mean, std deviation, and max of 'sensor_data'


# 2. Create a numpy array 'features' containing these 3 values


# 3. Create a numpy array 'weights' with values [0.2, 0.5, 0.3]
#    (Logic: Std Dev is most important, hence higher weight 0.5)


# 4. Calculate the Dot Product of 'features' and 'weights' using np.dot()


# 5. Print the final "Risk Score"


```

**Solution:**

```python
# 1. Extract features
data_mean = np.mean(sensor_data)
data_std = np.std(sensor_data)
data_max = np.max(sensor_data)

# 2. Create 'features' vector
features = np.array([data_mean, data_std, data_max])

# 3. Create 'weights' vector
weights = np.array([0.2, 0.5, 0.3])

# 4. Calculate Dot Product (Weighted Sum)
risk_score = np.dot(features, weights)

# 5. Print Risk Score
print(f"Features [Mean, Std, Max]: {features}")
print(f"Calculated Risk Score: {risk_score:.4f}")

```

---

## **Step 4: The Final Application**

**Logical Step:**
Put it all together into a single reusable function. This function simulates the machine and tells us if it is SAFE or DANGEROUS based on a threshold.

**Student Task:**

```python
def analyze_machine_health(freq_hz, noise_level):
    # 1. Setup Time (0 to 1 sec)
    
    # 2. Generate Clean Signal (Sin wave at freq_hz)
    
    # 3. Generate Noise (Normal dist, scale=noise_level)
    
    # 4. Create Sensor Data (Signal + Noise)
    
    # 5. Calculate Features (Mean, Std, Max)
    
    # 6. Calculate Risk Score (Dot product with weights [0.2, 0.5, 0.3])
    
    # 7. Logic: If Risk Score > 3.0 return "DANGER", else "SAFE"
    pass # Remove this pass and write your code

# Test the app
# print(analyze_machine_health(50, 1.0)) # Should be SAFE
# print(analyze_machine_health(50, 5.0)) # Should be DANGER (High noise)

```

**Solution:**

```python
def analyze_machine_health(freq_hz, noise_level):
    # 1. Setup
    t = np.linspace(0, 1, 1000)
    
    # 2. Generate
    clean = np.sin(2 * np.pi * freq_hz * t)
    noise = np.random.normal(0, noise_level, 1000)
    data = clean + noise
    
    # 3. Features & Linalg
    features = np.array([np.mean(data), np.std(data), np.max(data)])
    weights = np.array([0.2, 0.5, 0.3])
    score = np.dot(features, weights)
    
    # 4. Result
    status = "DANGER" if score > 3.0 else "SAFE"
    return f"Score: {score:.2f} | Status: {status}"

# Run the Application
print("Test 1 (Low Noise):", analyze_machine_health(50, 1.0))
print("Test 2 (High Noise):", analyze_machine_health(50, 5.0))

```