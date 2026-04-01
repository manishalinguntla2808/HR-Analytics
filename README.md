# 📊 HR Analytics Dashboard – Power BI  

## 📌 Project Overview  
This project focuses on analyzing employee attendance data to generate meaningful HR insights using **Power BI**.

The dashboard helps HR teams and managers track:
- Employee attendance patterns  
- Work-from-home trends  
- Sick leave behavior  
- Overall workforce productivity  

---

## 🎯 Key Insights  

The dashboard is designed to identify:

- **Working Preferences** (Office vs Work From Home)
- **Attendance Percentage**
  - Weekly and Monthly presence trends
- **Sick Leave (SL) Percentage**
- **WFH (Work From Home) Trends**
- **Employee-level attendance patterns**

---

## ⚙️ ETL Process (Power Query Transformation)
## 📂 Dataset  

- Source: Excel Workbook  
- Sheets:
  - `Apr 2022`  
  - `May 2022`  
  - `June 2022`
  - `Attendence`  

---

## ⚙️ ETL Process (Power Query)  

### 🔄 Data Transformation  

1. Load Data into **Power BI**
  - Open Power BI → Get Data → Excel
  - Click Transform Data (Do not directly load)
2. Handle Multiple Sheets
  - Since each sheet contains separate monthly data, transformation is required before merging.
3. Unpivot Date Columns
  - Problem: Dates are stored as columns
  - Solution:
    - Select Employee Code and Employee Name
    - Click Unpivot Other Columns
  - Resulting structure:
  * Employee Code | Name | Date | Attendance Value
4. Data Cleaning
  - Convert Date column → Date datatype
  - Remove errors (Right click → Remove Errors)
  - Rename columns appropriately

---

### 🔁 Dynamic Data Handling using Parameters  

- Create a Parameter:
  - Name: GetData
  - Value: e.g., Apr 2022
- Use this parameter to filter sheet data dynamically instead of hardcoding sheet names. 

---

### 🔧 Apply Transformations to All Sheets

1. Duplicate query (April sheet)
2. Apply all transformations
3. Convert query into a Function
4. Apply function to all sheets using:
  - Add Column → Invoke Function 

---

### 🔗 Combine Data  

- Append all transformed sheets into a single dataset
- Final dataset contains:
  - Employee Code  
  - Name  
  - Date  
  - Attendance Status As Value

---

### 📤 Load Data

- Click Close & Apply
- Clean, structured dataset is now ready for analysis

---

## 📐 Data Modeling & Calculations

### Measures vs Calculated Columns  

| Feature | Measure | Column |
|--------|--------|--------|
| Calculation Timing | During visualization interaction | During data refresh |
| Storage | No physical storage | Stored in table |
| File Size | No impact | Increases file size |
| Use Case | Aggregations (%, totals) | Row-level logic |

---

## 🧮 DAX Key Calculations

### Day of Week
```DAX
Day of Week = FORMAT('Final Data'[Date], "ddd")
```

### Month
```DAX
Month = STARTOFMONTH('Final Data'[Date])
```

### Total SL
```DAX
Total SL = SWITCH(TRUE(),
    'Final Data'[Value] = "SL", 1,
    'Final Data'[Value] = "HSL", 0.5,
    0)
```

### Total WFH
```DAX
Total WFH = SWITCH(TRUE(),
    'Final Data'[Value] = "WFH", 1,
    'Final Data'[Value] = "HWFH", 0.5,
    0)
```

### Presence %
```DAX
Presence % = DIVIDE([TotalPresentDays], [TotalWorkingDays],0)
```

### SL %
```DAX
SL % = DIVIDE([TotalSL], [TotalWorkingDays], 0)
```

### TotalPresentDays
```DAX
TotalPresentDays = 

var PresentDays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] = "P")
RETURN PresentDays + [TotalWFH]
```

### TotalSL
```DAX
TotalSL = SUM('Final Data'[Total SL])
```

### TotalWFH
```DAX
TotalWFH = SUM('Final Data'[Total WFH])
```

### TotalWorkingDays
```DAX
TotalWorkingDays = 

var TotalDays = COUNT('Final Data'[Value])
var TotalNonWorkingDays = CALCULATE(COUNT('Final Data'[Value]), 'Final Data'[Value] in {"WO","NO"})

RETURN TotalDays - TotalNonWorkingDays
```

### WFH %
```DAX
WFH % = DIVIDE([TotalWFH], [TotalPresentDays], 0)
```

---

## 📅 Date Enhancements
- Create Month Column for filtering
- Avoid using FORMAT() (returns text)
- Use:
  - STARTOFMONTH
  - ENDOFMONTH
  - EOMONTH
    👉 Ensures proper date sorting

---

## 📊 Dashboard Design

### 🧾 Summary Cards
- Presence %
- WFH %
- Sick Leave %

---

### 📋 Employee Table

Displays:
` Employee Name
- Presence %
- WFH %
- SL %

---

### 🔍 Attendance Matrix
- Rows: Employee Name
- Columns: Date
- Values: Attendance Status

👉 Helps verify daily attendance

---

### 📈 Trend Analysis (Line Charts)
- Presence % over time
- WFH % trend
- SL % trend

---

### 📅 Slicer
- Month-based filtering
- Enables trend comparison across months

---

### 📆 Day-wise Analysis
- Create Day of Week column
- Table showing:
- Day
- Presence %
- WFH %
- SL %

---
## 🔐 Data Security (Row-Level Security)

To restrict access:
` Implement **Row-Level Security (RLS)**
**Use Case:**
- Employees see only their own data
- Managers see full dataset

👉 Can create:

- Manager Dashboard (Full Access)
- Employee Dashboard (Restricted Access)

---

## 📌 Conclusion

This HR Analytics dashboard provides:

- Clear visibility into employee attendance behavior
- Insights into work preferences (WFH vs Office)
- Data-driven decision-making for HR teams

---

## 🚀 Tools Used

- Power BI
- Power Query (ETL)
- DAX (Data Analysis Expressions)
- Excel (Data Source)

---

## 🔗 Connect  

GitHub: https://github.com/manishalinguntla2808  
LinkedIn: https://www.linkedin.com/in/manisha-linguntla/  

---
