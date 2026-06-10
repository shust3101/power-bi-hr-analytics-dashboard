# DAX Measures

This file documents the main DAX measures and calculated columns used in the Power BI HR Analytics Dashboard.

## Main Measures

### Total Employees

```DAX
Total Employees =
DISTINCTCOUNT('HR Data'[Employee ID])
```

Calculates the total number of unique employees.

### Active Employees

```DAX
Active Employees =
CALCULATE(
    [Total Employees],
    'HR Data'[Attrition] = "No"
)
```

Calculates the number of employees who stayed with the company.

### Employees Left

```DAX
Employees Left =
CALCULATE(
    [Total Employees],
    'HR Data'[Attrition] = "Yes"
)
```

Calculates the number of employees who left the company.

### Attrition Rate

```DAX
Attrition Rate =
DIVIDE(
    [Employees Left],
    [Total Employees]
)
```

Calculates the percentage of employees who left the company.

### Average Age

```DAX
Average Age =
AVERAGE('HR Data'[Age])
```

Calculates the average employee age.

### Average Monthly Income

```DAX
Average Monthly Income =
AVERAGE('HR Data'[Monthly Income])
```

Calculates the average monthly income of employees.

### Average Years at Company

```DAX
Average Years at Company =
AVERAGE('HR Data'[Years at Company])
```

Calculates the average number of years employees have worked at the company.

### Average Job Satisfaction

```DAX
Average Job Satisfaction =
AVERAGE('HR Data'[Job Satisfaction])
```

Calculates the average job satisfaction score.

### Average Performance Rating

```DAX
Average Performance Rating =
AVERAGE('HR Data'[Performance Rating])
```

Calculates the average employee performance rating.

### Average Work Life Balance

```DAX
Average Work Life Balance =
AVERAGE('HR Data'[Work Life Balance])
```

Calculates the average work-life balance score.

---

## Display Measures

Display measures were created for KPI cards to show clean formatting and avoid automatic abbreviation in Power BI cards.

These measures were used only in KPI cards. Numeric measures were used in charts to preserve correct sorting, filtering, and aggregation.

### Total Employees Display

```DAX
Total Employees Display =
FORMAT([Total Employees], "#,0")
```

### Active Employees Display

```DAX
Active Employees Display =
FORMAT([Active Employees], "#,0")
```

### Employees Left Display

```DAX
Employees Left Display =
FORMAT([Employees Left], "#,0")
```

### Attrition Rate Display

```DAX
Attrition Rate Display =
FORMAT([Attrition Rate], "0.0%")
```

### Average Age Display

```DAX
Average Age Display =
FORMAT([Average Age], "0.0")
```

### Average Monthly Income Display

```DAX
Average Monthly Income Display =
FORMAT([Average Monthly Income], "$#,0")
```

### Average Years at Company Display

```DAX
Average Years at Company Display =
FORMAT([Average Years at Company], "0.0")
```

### Average Job Satisfaction Display

```DAX
Average Job Satisfaction Display =
FORMAT([Average Job Satisfaction], "0.0")
```

### Average Performance Rating Display

```DAX
Average Performance Rating Display =
FORMAT([Average Performance Rating], "0.0")
```

---

## Calculated Columns

Calculated columns were created to group employees into readable business categories and to control the sorting order in Power BI visuals.

### Age Group

```DAX
Age Group =
SWITCH(
    TRUE(),
    'HR Data'[Age] < 25, "Under 25",
    'HR Data'[Age] >= 25 && 'HR Data'[Age] < 35, "25-34",
    'HR Data'[Age] >= 35 && 'HR Data'[Age] < 45, "35-44",
    'HR Data'[Age] >= 45 && 'HR Data'[Age] < 55, "45-54",
    "55+"
)
```

Groups employees into age ranges.

### Age Group Sort

```DAX
Age Group Sort =
SWITCH(
    TRUE(),
    'HR Data'[Age] < 25, 1,
    'HR Data'[Age] >= 25 && 'HR Data'[Age] < 35, 2,
    'HR Data'[Age] >= 35 && 'HR Data'[Age] < 45, 3,
    'HR Data'[Age] >= 45 && 'HR Data'[Age] < 55, 4,
    5
)
```

Sorts age groups in the correct logical order.

### Tenure Group

```DAX
Tenure Group =
SWITCH(
    TRUE(),
    'HR Data'[Years at Company] < 1, "Less than 1 year",
    'HR Data'[Years at Company] >= 1 && 'HR Data'[Years at Company] < 3, "1-2 years",
    'HR Data'[Years at Company] >= 3 && 'HR Data'[Years at Company] < 6, "3-5 years",
    'HR Data'[Years at Company] >= 6 && 'HR Data'[Years at Company] < 10, "6-9 years",
    "10+ years"
)
```

Groups employees by tenure at the company.

### Income Group

```DAX
Income Group =
SWITCH(
    TRUE(),
    'HR Data'[Monthly Income] < 3000, "Under 3K",
    'HR Data'[Monthly Income] >= 3000 && 'HR Data'[Monthly Income] < 6000, "3K-6K",
    'HR Data'[Monthly Income] >= 6000 && 'HR Data'[Monthly Income] < 10000, "6K-10K",
    'HR Data'[Monthly Income] >= 10000 && 'HR Data'[Monthly Income] < 15000, "10K-15K",
    "15K+"
)
```

Groups employees by monthly income range.

### Income Group Sort

```DAX
Income Group Sort =
SWITCH(
    TRUE(),
    'HR Data'[Monthly Income] < 3000, 1,
    'HR Data'[Monthly Income] >= 3000 && 'HR Data'[Monthly Income] < 6000, 2,
    'HR Data'[Monthly Income] >= 6000 && 'HR Data'[Monthly Income] < 10000, 3,
    'HR Data'[Monthly Income] >= 10000 && 'HR Data'[Monthly Income] < 15000, 4,
    5
)
```

Sorts income groups in the correct logical order.

### Job Satisfaction Group

```DAX
Job Satisfaction Group =
SWITCH(
    'HR Data'[Job Satisfaction],
    1, "1 - Low",
    2, "2 - Medium",
    3, "3 - High",
    4, "4 - Very High"
)
```

Creates readable labels for job satisfaction levels.

### Job Satisfaction Sort

```DAX
Job Satisfaction Sort =
'HR Data'[Job Satisfaction]
```

Sorts job satisfaction groups in the correct order.

### Work Life Balance Group

```DAX
Work Life Balance Group =
SWITCH(
    'HR Data'[Work Life Balance],
    1, "1 - Low",
    2, "2 - Medium",
    3, "3 - High",
    4, "4 - Very High"
)
```

Creates readable labels for work-life balance levels.

### Work Life Balance Sort

```DAX
Work Life Balance Sort =
'HR Data'[Work Life Balance]
```

Sorts work-life balance groups in the correct order.

---

## Notes

The dashboard uses numeric measures for charts and formatted display measures for KPI cards.

This approach keeps charts accurate while making KPI cards easier to read.
