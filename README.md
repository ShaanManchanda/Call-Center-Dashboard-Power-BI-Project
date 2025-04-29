![GitHub Banners (4)](https://github.com/user-attachments/assets/f7f8b2ca-c1da-4e11-8b3a-b19898a1cbd0)

# Call Center Dashboard - Power BI Project

## Problem Statement

This project aims to create a **Power BI dashboard** for the Call Center Manager that reflects all relevant **Key Performance Indicators (KPIs)** and metrics derived from the call center trends dataset from January to March in 2021.

KPIs include:
- Overall customer satisfaction
- Calls answered and abandoned
- Calls by time of day
- Average speed of answer
- Agent performance (handle time vs calls answered)

---

## Datasource

- **Dataset Source**: Provided by PwC  
  [PwC Virtual Case Experience](https://www.pwc.ch/en/careers-with-pwc/students/virtual-case-experience.html)
- **Dataset**: 
 [Call Center Trends](https://github.com/SagnikKundu07/Call-Centre-Dashboard---Power-BI-Project/blob/main/Call-Center-Dataset.xlsx)
- **Structure**: 10 columns, 5000 rows

---

## Tools and Technologies

- Microsoft Power BI Desktop
- Power Query Editor
- DAX (Data Analysis Expressions)
- Power BI Visualizations
- Microsoft Excel

---

## Data Preparation

Performed in **Power Query**:
- Removed unnecessary columns and rows
- Corrected data types

The dataset was then loaded into **Power BI Desktop** for modeling.

---

## Data Modeling

The cleaned and transformed dataset was modeled to support KPI tracking and visualization.

---

## DAX Measures

- Total Calls Answered = `COUNTX(FILTER('call_log', 'call_log'[Answered (Y/N)] = "Answered"), 'call_log'[Answered (Y/N)])`

- Total Calls Not Answered = `COUNTX(FILTER('call_log', 'call_log'[Answered (Y/N)] = "Not Answered"), 'call_log'[Answered (Y/N)])`

- Total Calls Received = `[Total Calls Answered] + [Total Calls Not Answered]`

- Total Calls Resolved = `COUNTX(FILTER('call_log', 'call_log'[Resolved] = "Resolved"), 'call_log'[Resolved])`

- Average Satisfaction Rate = `AVERAGEX('call_log', [Satisfaction rating])`

- Average Speed of Answer = `AVERAGEX('call_log', [Speed of answer in seconds])`

- Average Call Duration = `AVERAGEX('call_log', [Duration (Secs)])`

- Short Month Name = `FORMAT('call_log'[Date], "mmm")`

- Resolution Rate % = `DIVIDE([Total Calls Resolved], [Total Calls Answered], 0)`

- Overall Average Speed of Answer = `CALCULATE(AVERAGEX('call_log', [Speed of answer in seconds]), ALL('call_log'))`

- Overall Average Call Duration = `CALCULATE(AVERAGEX('call_log', [Duration (Secs)]), ALL('call_log'))`

- Overall Average Satisfaction Rate = `CALCULATE(AVERAGEX('call_log', [Satisfaction rating]), ALL('call_log'))`

- Overall Average Resolution Rate % = `CALCULATE(DIVIDE([Total Calls Resolved], [Total Calls Answered]), ALL('call_log'))`

- Speed of Answer Icon = `SWITCH(TRUE(), [AVG Speed of Answer] > [Overall Average Speed of Answer], UNICHAR(9650), [AVG Speed of Answer] < [Overall Average Speed of Answer], UNICHAR(9660), UNICHAR(9473))`

- Speed of Answer Icon Color = `SWITCH(TRUE(), [AVG Speed of Answer] > [Overall Average Speed of Answer], "Green", [AVG Speed of Answer] < [Overall Average Speed of Answer], "Red", "Grey")`

- Resolution Rate Icon = `SWITCH(TRUE(), [Resolution Rate %] > [Overall Average Resolution Rate %], UNICHAR(9650), [Resolution Rate %] < [Overall Average Resolution Rate %], UNICHAR(9660), UNICHAR(9473))`

- Resolution Rate Icon Color = `SWITCH(TRUE(), [Resolution Rate %] > [Overall Average Resolution Rate %], "Green", [Resolution Rate %] < [Overall Average Resolution Rate %], "Red", "Grey")`

- Call Duration Icon = `SWITCH(TRUE(), [AVG Call Duration] > [Overall Average Call Duration], UNICHAR(9650), [AVG Call Duration] < [Overall Average Call Duration], UNICHAR(9660), UNICHAR(9473))`

- Call Duration Icon Color = `SWITCH(TRUE(), [AVG Call Duration] > [Overall Average Call Duration], "Green", [AVG Call Duration] < [Overall Average Call Duration], "Red", "Grey")`

- Satisfaction Rating Color = `SWITCH(TRUE(), [AVG Satisfaction Rate] > [Overall Average Satisfaction Rate], "#19b47b", [AVG Satisfaction Rate] < [Overall Average Satisfaction Rate], "#D91656", "Grey")`

- Top Rated Agent = `VAR AgentAvgTable = ADDCOLUMNS(VALUES('call_log'[Agent]), "AvgSatisfaction", CALCULATE(AVERAGE('call_log'[Satisfaction rating]))) VAR TopAgentRow = TOPN(1, AgentAvgTable, [AvgSatisfaction], DESC) RETURN CONCATENATEX(TopAgentRow, [Agent], ", ")`

---

## Data Visualization (Dashboard)

![GitHub Banners (4)](https://github.com/user-attachments/assets/6da3d948-082c-4aff-a766-8a8ca9924391)

Dashboard created in **Microsoft Power BI Desktop**, featuring:
- Total calls overview
- Answered vs abandoned analysis
- Resolution rates
- Satisfaction trends
- Average call durations
- Agent performance insights
- Call patterns by time of day
- Green and Red Icon colors (based on whether the metric's average value is higher or lower)

![image](https://github.com/user-attachments/assets/4561cb11-f04f-4998-b88e-f4b7456f06d3)

![image](https://github.com/user-attachments/assets/c19adc4c-3f6b-4e32-894c-ba699faacbce)


---

## Key Insights

### Customer Satisfaction
- Most customer satisfaction ratings are between **3** and **4**.
- Agent satisfaction ratings peaked in **January** at **2.84**, then declined through **February** and **March**.

### Call Volume and Timing
- The highest volume of calls occurs between **11 AM** and **2 PM**.
- The issue resolution rate was highest in **January**, dipped in **February**, and improved again in **March**.

### Agent Performance
- **Diane** has the fastest average speed of answer at **52 seconds**, while **Martha** has the slowest response time.
- **Greg** achieved the highest resolution rate, resolving **91%** of customer queries with an average call duration of **182 seconds**.

### Expertise by Issue Type
- **Becky** primarily handled **payment** and **streaming** issues.
- **Dan** and **Martha** mainly provided **technical support**.
- **Diane** focused on **administrative support** issues.
- **Greg** specialized in resolving **streaming**-related problems.
- **Jim** and **Stewart** focused on **contract-related** issues.
- **Joe** offered balanced support across **streaming**, **payment**, **technical**, and **administrative** categories, but showed limited involvement with **contract-related** cases.
