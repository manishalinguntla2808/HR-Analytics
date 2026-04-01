# 📊 HR Analytics Dashboard – Power BI  

![Power BI](https://img.shields.io/badge/Tool-PowerBI-yellow)  
![Project Type](https://img.shields.io/badge/Project-HR%20Analytics-blue)  
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)  

---

## 📌 Project Overview  
This project focuses on analyzing employee attendance data to generate meaningful HR insights using **Power BI**.  

The dashboard helps HR teams and managers track:
- Employee attendance patterns  
- Work-from-home trends  
- Sick leave behavior  
- Overall workforce productivity  

---

## 🎯 Key Insights  

✔️ Working preferences (WFH vs Office)  
✔️ Attendance % (Weekly & Monthly)  
✔️ Sick Leave (SL %)  
✔️ Work From Home (WFH %)  
✔️ Employee-level attendance trends  

---

## 📂 Dataset  

- Source: Excel Workbook  
- Sheets:
  - `Apr 2022`  
  - `May 2022`  
  - `June 2022`  

---

## ⚙️ ETL Process (Power Query)  

### 🔄 Data Transformation  

1. Load Excel → Click **Transform Data**  
2. Duplicate query  
3. Select Employee Code & Name  
4. Click **Unpivot Other Columns**  

---

### 🧹 Data Cleaning  

- Convert Date → Date datatype  
- Remove errors  
- Rename columns  

---

### 🔁 Parameter Usage  

- Create Parameter: `GetData`  
- Use for dynamic filtering  

---

### 🔧 Function Creation  

- Convert query to function  
- Apply to all sheets  

---

### 🔗 Combine Data  

- Append all sheets  
- Final dataset:
  - Employee Code  
  - Name  
  - Date  
  - Attendance  

---

## 📐 Data Modeling  

### Measures vs Columns  

| Feature | Measure | Column |
|--------|--------|--------|
| Calc Time | Interaction | Refresh |
| Storage | No | Yes |
| Use | Aggregations | Row logic |

---

## 🧮 DAX  

### WFH Column  
```DAX
WFH Value = IF('Table'[Attendance]="WFH",1,IF('Table'[Attendance]="HWFH",0.5,0))
```

### Total Present Days  
```DAX
Total Present Days = COUNT('Table'[Attendance]) + SUM('Table'[WFH Value])
```

### Presence %  
```DAX
Presence % = DIVIDE([Total Present Days],[Total Working Days])
```

---

## 📊 Dashboard  

- KPI Cards  
- Employee Table  
- Attendance Matrix  
- Trend Charts  
- Month Slicer  
- Day-wise Analysis  

---

## 🔐 Row-Level Security  

- Employees → Limited access  
- Managers → Full access  

---

## 🚀 Tools  

- Power BI  
- DAX  
- Power Query  
- Excel  

---

## 🔗 Connect  

GitHub: https://github.com/manishalinguntla2808  
LinkedIn: https://www.linkedin.com/in/manisha-linguntla/  

---

⭐ Star this repo if you like it!
