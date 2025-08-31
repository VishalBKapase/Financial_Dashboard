# 📊 Financial Dashboard in Power BI
## 🔹 Problem Statement
The finance team of a company is facing challenges in tracking and analyzing financial performance across multiple components and time periods. Currently, reports are generated manually using Excel, leading to:
- ⏳ Delayed decision-making due to slow reporting cycles.  
- 📉 Difficulty in comparing actual vs. target performance for Income, Expenses, and Savings.  
- 🔍 Lack of visibility into trends such as Monthly, Quarterly, and Yearly growth.  
- 📊 Inefficient tracking of KPIs like **Gross Margin %, Operating Income, and Savings**.  
To overcome these challenges, the company required a **centralized, interactive financial dashboard built in Power BI**.

## 🔹 Dataset Description
The dataset was sourced from **Excel spreadsheets** containing financial transactions and targets.  

**Dataset Fields:**  
- **Type**: Expense, Saving, Income, Target  
- **Components**: Emergency Fund, EMI, Fixed Deposit, Freelancing, Groceries & Food, Health, House Rent, Leisure, Liquid Cash, Mutual Fund, Salary, Savings, Shopping, Travel, Other  
- **Date**  
- **Value**  
- **Year**  
- **Month-Year**
- 
## 🔹 Data Modeling Steps
### 1. Data Collection & Preparation
- Imported financial data (Expense, Saving, Income, Target) from Excel.  
- Cleaned and transformed data using **Power Query**.  

### 2. Data Modeling
- Created relationships to enable time intelligence analysis.  

### 3. DAX Calculations
- Developed calculated measures including:  
  - **Total Value**  
  - **Income, Expense, Savings, Savings %**  
  - **Monthly Growth for Income, Expense, Savings**  
  - **Income Change MoM %**  
  - **Time Intelligence (e.g., PREVIOUSMONTH)**  

## 🔹 DAX Measures Used
Examples of DAX measures implemented:  

```DAX
Total Value = SUM('Dataset'[Value])

Income = CALCULATE([Total Value], 'Dataset'[Type] = "Income")

Expense = CALCULATE([Total Value], 'Dataset'[Type] = "Expense")

Savings = CALCULATE([Total Value], 'Dataset'[Type] = "Savings")

Saving % = DIVIDE([Savings], [Income])

Income LM = CALCULATE([Income], DATEADD('Dataset'[Date].[Date],-1, Month))

Income Change MoM % = DIVIDE([Income], [Income LM])

Income_Monthly_Growth = VAR Val = (CALCULATE([Monthly_Growth],'Dataset'[Type] = "Income" )) RETURN IF(Val=BLANK(), 0, Val)

Monthly Sale = Var CY_Selected_Month = SELECTEDVALUE('Selected Date'[Month_Year]) Return CALCULATE ([Total Value],'Dataset'[Month_Year] = CY_Selected_Month)

PY_Month_Sale = Var PY_Month =  PREVIOUSMONTH('Selected Date'[Date]) RETURN CALCULATE([Total Value], 'Dataset'[Date] = PY_Month)

Monthly_Growth = DIVIDE([Monthly Sale] - [PY_Month_Sale], [PY_Month_Sale])

##🔹** Dashboard Explanation**

The dashboard was designed with multiple interactive visuals to improve decision-making:

### KPI Cards 

Total Income, Total Expense, Total Savings, Savings %.

Monthly Growth metrics for Income, Expense, and Savings.

### Line/Area Chart

Displays Income, Expense, Savings, and Target trends over Month-Year.

Linked with a Dynamic Slicer for time-based filtering.

### Donut Charts

Breakdown of Expenses by Component.

Breakdown of Savings by Component.

Tooltip added to show Year-wise Expense and Savings.

### Matrix Table

Income and Expense by individual components.

### Bookmarks

Show/Hide Slicer functionality for improved user experience.

### Slicers

Year and Month-Year filter for flexible analysis.

Other functions used: SUM, CALCULATE, DIVIDE, VAR, PREVIOUSMONTH, SELECTEDVALUE, IF

## 🔹 ****Conclusion / Key Insights****

The Financial Dashboard enabled the finance team to move from static Excel reports to dynamic, interactive insights. Key takeaways include:

✅ Clear visibility of KPIs (Income, Expense, Savings, and Savings %) with growth trends.

✅ Identification of top-performing months for savings and income.

✅ Highlighted underperforming years vs. targets, enabling better planning.

✅ Expense analysis by components showed major cost drivers like Rent, EMI, and Groceries.

✅ Year-wise insights through tooltips provided deeper trend comparisons.

✅ Improved decision-making speed with interactive filters, drilldowns, and bookmarks.

This dashboard empowers stakeholders to track financial performance efficiently, analyze trends, and make data-driven financial decisions.

