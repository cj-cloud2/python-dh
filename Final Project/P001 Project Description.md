## 1. Data Integrity & Schema Validation

The project must implement a "Clean-as-you-go" architecture. Before any analysis occurs, the raw data (which will contain intentional errors) must pass through a validation gate.

* **Handling Nulls:** You must define a strategy for missing values—imputing the mean for passenger counts or flagging unknown stations as "Uncategorized."
* **Type Consistency:** Ensure timestamps are strictly ISO-8601 compliant and numerical values (like revenue) are cast to float types to prevent logic errors during the NumPy phase.

## 2. Computational Efficiency (Vectorization)

A core requirement is to move away from slow Python loops as the dataset scales.

* **The "No-Loop" Rule:** Once the project moves into the **NumPy** and **Pandas** labs, element-wise calculations (like calculating tax or fare increases) must be performed using **vectorized operations**.
* **Performance Benchmarking:** You will compare the execution time of a standard Python `for` loop against a NumPy array operation to demonstrate the engineering advantage of array-based computing.

## 3. Relational Data Integration

Data Engineering is rarely about a single file. This project requires the successful merging of disparate datasets.

* **The Join Requirement:** You must merge the **Ridership Dataset** with a **Weather Dataset** and a **Station Metadata** file.
* **Key Mapping:** You will use the "Station_ID" as the foreign key to join these sets, ensuring no data loss occurs (Inner vs. Left joins).

## 4. Analytical Transformation (Feature Engineering)

Raw data is seldom useful for executives; it must be transformed into "features."

* **Time-Series Decomposition:** You must extract the "Hour of Day," "Day of Week," and "Is Weekend" flags from the raw timestamps.
* **Aggregated Metrics:** The pipeline must generate a "Peak-Load Factor" for every transit route, calculated as:



## 5. Visual Hierarchy & Statistical Storytelling

The final requirement is to move from "plotting data" to "visualizing insights."

* **Exploratory vs. Explanatory:** Lab 4 (Matplotlib) must focus on technical accuracy (labeled axes, scales, legends), while Lab 5 (Seaborn) must focus on trends (correlation heatmaps and distribution density).
* **Consistency:** A unified color palette must be used across all five labs to represent specific transit lines (e.g., Red Line always appears in red).

---

### Project Success Metric

By the end of Lab 5, you should be able to answer one specific "Business Question":

> *"How does a 5-degree drop in temperature affect the revenue of the Metro system compared to the Bus system?"*
