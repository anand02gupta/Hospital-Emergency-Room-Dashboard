# 🏥 Hospital Emergency Room (ER) Dashboard 📊

This project presents an interactive Power BI dashboard to analyze Emergency Room (ER) data, providing hospital administrators and healthcare professionals with actionable insights on patient flow, admission rates, and performance metrics.

## 📌 Objective

- Monitor ER admissions and discharge patterns
- Track patient inflow trends by date, time, and day of the week
- Identify key metrics such as admission rate, average wait time, and patient demographics
- Support hospital staff in decision-making and resource management

## 🧰 Tools & Technologies

- **Power BI** – for dashboard creation and visual analytics
- **DAX** – for calculated columns and measures
- **Excel/CSV** – as data source
- **Data Modeling** – for relationships and filters

## 📁 Dataset Overview

Key fields include:
- Patient ID
- Date & Time of Visit
- Gender
- Age Group
- Admission Flag
- Reason for Visit
- Department
- Discharge Status

> *Note: The dataset is a simulated sample for educational purposes.*

## 📊 Dashboard Features

- Total ER Visits and Admissions
- Admission Rate (calculated using DAX)
- Patient Trends by Weekday and Hour
- Age and Gender Distribution
- Filter by Date Range, Department, and Reason
- Clean layout with slicers and drill-downs

## 📌 DAX Highlight

Example formula used:
```DAX
1. Admission Status = IF('ER_Data'[Patient Admission Flag] = TRUE(), "Admitted", "Not Admitted")
2. month & Year = FORMAT('Date Table'[Date], "MMM") & " " & YEAR('Date Table'[Date])
3. Age Group = SWITCH(
    True(),
    'Hospital ER_Data'[Patient Age] >= 100, "100+",
    'Hospital ER_Data'[Patient Age] >= 90, "90-99",
    'Hospital ER_Data'[Patient Age] >= 80, "80-89",
    'Hospital ER_Data'[Patient Age] >= 70, "70-79",
    'Hospital ER_Data'[Patient Age] >= 60, "60-69",
    'Hospital ER_Data'[Patient Age] >= 50, "50-59",
    'Hospital ER_Data'[Patient Age] >= 40, "40-49",
    'Hospital ER_Data'[Patient Age] >= 30, "30-39",
    'Hospital ER_Data'[Patient Age] >= 20, "20-29",
    'Hospital ER_Data'[Patient Age] >= 10, "10-19",
    "0-9"
)
4. Avg Wait Time = FORMAT(AVERAGE('Hospital ER_Data'[Patient Waittime]),"0.0") & "Min"
5. Waittime Interval = 
SWITCH(
    TRUE(),
    'Hospital ER_Data'[Admission Hour] < 2, "00-02",
    'Hospital ER_Data'[Admission Hour] < 4, "03-04",
    'Hospital ER_Data'[Admission Hour] < 6, "05-06",
    'Hospital ER_Data'[Admission Hour] < 8, "07-08",
    'Hospital ER_Data'[Admission Hour] < 10, "09-10",
    'Hospital ER_Data'[Admission Hour] < 12, "11-12",
    'Hospital ER_Data'[Admission Hour] < 14, "13-14",
    'Hospital ER_Data'[Admission Hour] < 16, "15-16",
    'Hospital ER_Data'[Admission Hour] < 18, "17-18",
    'Hospital ER_Data'[Admission Hour] < 20, "19-20",
    'Hospital ER_Data'[Admission Hour] < 22, "21-22",
    'Hospital ER_Data'[Admission Hour] < 24, "23-24",
    "Above 24"
)
6. Waittime Status = if ('Hospital ER_Data'[Patient Waittime]<=30, "Within Target", "Target Missed")

