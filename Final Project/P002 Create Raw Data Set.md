### The "UrbanPulse_Raw_Transit_Data.csv"

Copy this content into a file named `transit_data.csv` or use the Python snippet below to generate it automatically in your environment.

```csv
timestamp,station_id,transit_type,passenger_count,revenue,weather_temp
2025-01-01 08:00:00,STN_001,Bus,45,112.50,2.5
2025-01-01 08:15:00,STN_002,Metro,120,360.00,2.4
01/01/2025 08:30,STN_001,bus,38,,2.1
2025-01-01 09:00:00,STN_003,Metro,310,930.00,
2025-01-01 09:15:00,STN_002,Metro,,450.00,3.0
01-01-2025 09:30,STN_001,Bus,55,137.50,3.5
2025-01-01 10:00:00,STN_004,LightRail,22,66.00,4.2
2025-01-01 10:15:00,STN_002,METRO,150,450.00,4.5
2025-01-01 10:30:00,STN_001,Bus,NaN,100.00,4.8
2025-01-01 11:00:00,STN_003,Metro,280,840.00,5.0

```

---

### Data Engineering Challenges Built-in:

* **Case Sensitivity:** Look at `transit_type`. We have "Bus", "bus", "Metro", and "METRO".
* **Missing Values:** Note the empty revenue for row 3 and `NaN` for passenger count in row 9.
* **Inconsistent Datetime:** We have `YYYY-MM-DD`, `MM/DD/YYYY`, and `DD-MM-YYYY`.
* **Missing Metadata:** `weather_temp` is missing for STN_003 at 09:00.

---

### Automated Setup Script

Run this code in your Python environment (Jupyter/Colab) to create the file and prepare for **Lab 1**.

```python
import pandas as pd
import io

csv_data = """timestamp,station_id,transit_type,passenger_count,revenue,weather_temp
2025-01-01 08:00:00,STN_001,Bus,45,112.50,2.5
2025-01-01 08:15:00,STN_002,Metro,120,360.00,2.4
01/01/2025 08:30,STN_001,bus,38,,2.1
2025-01-01 09:00:00,STN_003,Metro,310,930.00,
2025-01-01 09:15:00,STN_002,Metro,,450.00,3.0
01-01-2025 09:30,STN_001,Bus,55,137.50,3.5
2025-01-01 10:00:00,STN_004,LightRail,22,66.00,4.2
2025-01-01 10:15:00,STN_002,METRO,150,450.00,4.5
2025-01-01 10:30:00,STN_001,Bus,NaN,100.00,4.8
2025-01-01 11:00:00,STN_003,Metro,280,840.00,5.0"""

with open('transit_data.csv', 'w') as f:
    f.write(csv_data)

print("File 'transit_data.csv' has been created successfully!")

```

---
