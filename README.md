# 🚦 Traffic Analysis Dashboard

## 📊 Dashboard Link
[University Traffic Dashboard](https://app.powerbi.com/groups/me/reports/c97c52fe-05c9-465d-9dbd-7cc8f0890a47/9634358e52330208548b?experience=power-bi)

## 📌 Problem Statement
The university is committed to promoting sustainable transportation but faces challenges due to the dominance of private vehicles, low public transport utilization, and minimal bicycle adoption.

### **Key Questions Addressed:**
- What is the ratio of public vs. private vehicle usage?
- What percentage of cars have single occupants?
- How can the university encourage sustainable transportation choices?

The dashboard provides **data-driven insights** into traffic patterns, enabling policymakers to optimize transport strategies for a more eco-friendly and efficient campus commute.

---
## 🛠 Steps Followed to Build the Dashboard

### **Step 1: Data Loading & Preprocessing**
- The dataset (CSV files) was imported into **Power BI Desktop**.
- Power Query Editor was used for data transformation, including:
  - Standardizing date & time formats.
  - Filtering vehicle types and occupancy values to remove inconsistencies.
  - Consolidating multiple CSV files into a single dataset.
  - Handling encoding and file structure issues.

### **Step 2: Creating New Columns & DAX Measures**

#### 🚗 **Categorizing Vehicles as Public or Private**
```DAX
Vehicle Category =  
SWITCH(
    TRUE(),
    merged_data[Type] = "bus", "Public",
    merged_data[Type] IN {"car", "bicycle", "taxi", "motorbike", "van", "lorry", "scooter"}, "Private",
    "Unknown"
)
```
This classification helped compare public and private transport adoption rates.

#### 🚶 **Categorizing Occupancy Levels for Cars**
```DAX
Occupancy Category = 
IF('merged_data'[Type] = "car",
   SWITCH(TRUE(),
       'merged_data'[Occupancy] = 1, "Lone Occupant",
       'merged_data'[Occupancy] = 2, "2 People",
       'merged_data'[Occupancy] > 2, "> 2 People",
       BLANK()
   ),
   BLANK()
)
```
Allowed for a detailed analysis of single vs. multi-occupant car usage.

#### 📊 **Vehicle Percentage Calculation**
```DAX
Vehicle Percentage = 
DIVIDE(
    COUNTROWS('merged_data'), 
    CALCULATE(COUNTROWS('merged_data'), ALL('merged_data'[Type]))
) * 100
```
Showed the proportion of each vehicle type in the dataset.

#### 🚴 **Bicycle Adoption Rate (%)**
```DAX
Bicycle Adoption Rate (%) = 
DIVIDE(
    COUNTROWS(FILTER(merged_data, merged_data[Type] = "bicycle")),
    COUNTROWS(merged_data)
) * 100
```
Highlighted the low usage of bicycles, supporting policy recommendations for better cycling infrastructure.

#### 👥 **Average Vehicle Occupancy Calculation**
```DAX
Avg Occupancy = 
AVERAGEX(
    SUMMARIZE(
        merged_data, 
        merged_data[Type], 
        "AvgOccupancy", AVERAGE(merged_data[Occupancy])
    ), 
    [AvgOccupancy]
)
```
Helped understand how effectively vehicles were being utilized.

---
## 📊 Step 3: Dashboard Visuals & Insights

### **📌 Key Visuals Created**
1️⃣ **Stacked Column Chart**: Public vs. Private Vehicle Distribution  
   - Analyzed the prevalence of private vs. public transport usage.
2️⃣ **Bar Chart**: Vehicle Type Breakdown  
   - Showed the dominance of private cars over other transport modes.
3️⃣ **Card Visuals**: Key Metrics  
   - 🚗 Total Vehicles
   - 🚴 Bicycle Adoption Rate (%)
   - 🚌 Public vs. Private Transport Ratio
   - 👥 Average Vehicle Occupancy
4️⃣ **Line Chart**: Traffic Trends Over Time  
   - Identified peak travel hours and days of the week with higher congestion.
5️⃣ **Donut Chart**: Occupancy Distribution (Lone Driver vs. Carpooling)  
   - Helped understand carpooling behavior and inefficiencies in vehicle occupancy.

---
## 📊 Step 4: Insights & Findings

### 🚗 **Dominance of Single-Occupancy Cars**
- **64% of cars** had only one occupant, leading to congestion & higher emissions.

### 🚴 **Low Bicycle Adoption**
- **Only 3%** of people use bicycles, highlighting the need for infrastructure improvements.

### 🚌 **Public Transport Underutilization**
- Buses and taxis accounted for a **low percentage of total transport**, indicating low adoption rates.

### 📉 **Slight Increase in Sustainable Practices (2023 vs. 2022)**
- A **4% rise** in carpooling and public transport use was observed, though **insufficient** to offset private car reliance.

---
## 📢 Step 5: Recommendations & Policy Actions

### 🔹 **Incentivize Carpooling & Public Transport Usage**
- Offer **priority parking & discounts** for shared rides.
- Implement a **ride-sharing system** for students & staff.

### 🔹 **Improve Bicycle Infrastructure**
- Create **dedicated cycling lanes** and **bike-sharing programs**.
- Provide **secure bicycle parking** near key campus locations.

### 🔹 **Enhance Public Transport Accessibility**
- Improve **bus frequency & route optimization**.
- Offer **subsidized travel passes** for students & faculty.

---
## 🚀 Step 6: Publishing & Future Work

### ✅ **Publishing the Dashboard**
- The dashboard was published to **Power BI Desktop** for real-time 
![Image](https://github.com/user-attachments/assets/3aac58bb-2ff5-4dde-9136-b5e997e8360e)

### 📊 **Future Enhancements**
- 🔍 **Machine Learning for Traffic Prediction**
  - Use ML models to forecast peak congestion times.
- 📈 **Live Traffic Feeds**
  - Integrate real-time traffic data from GPS or sensors.
- 🚨 **Anomaly Detection**
  - Identify unexpected spikes in single-occupancy cars or drops in public transport usage.

---
## 🎯 Conclusion
The **University Traffic Analysis Dashboard** provides **actionable insights** into campus commuting patterns. The findings highlight major sustainability challenges, including:
- **Over-reliance on private vehicles**
- **Low bicycle adoption**
- **Underutilized public transport**

By implementing **data-driven policies**, the university can:
✅ Reduce congestion
✅ Improve sustainability
✅ Encourage alternative transport modes 🚴🚗🚌

---
### 🚀 Developed with Power BI 📊
