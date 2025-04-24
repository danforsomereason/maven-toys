# Maven Toys Sales Dashboard

This is an interactive Excel dashboard built around fictional data from a toy company's regional sales managers. It tracks performance across time, filters dynamically by region, and highlights key business trends.

![image](https://github.com/user-attachments/assets/0766c26b-aa16-4d7a-b7d8-ac5cd02bbfda)


## 📊 Project Overview

The goal of this project was to explore and visualize sales trends for Regional Sales Managers across various U.S. regions. It compares monthly and year-over-year revenue trends, calculates KPIs, and displays performance through clean and strategic Excel visualizations.

This dashboard was built as part of a Maven Analytics course to practice advanced Excel techniques and dashboard development.

## 🛠️ Tools Used

- Microsoft Excel
  - Named Ranges & Name Manager (similar to storing a function in a variable and then using the variable as a callback)
  - Conditional Formatting
  - Lookups and advanced formulas
  - Charts and Linked Pictures

## 💡 Key Features

- KPI calculations for revenue, growth, and comparisons
- Monthly performance tracking with MoM trends
- Year-over-year metrics using `MAXIFS` and `SUMIFS`
- Dynamically sorted tables
- Linked pictures to retain formatting in dashboard tiles
- Logic for hiding future (0-value) months in line charts using `NA()`

## ✏️ Formulas & Logic Highlights

Here are a few Excel techniques used in the project:

-Name Manager allows us to declare a name for our filters, making it easier to write formulas in plain English down the line.

When it came to calculating our month data, we used an IF statement to return the previous year so that January - 1 equals December. As in this scenario:
=SUMIFS(Data[Revenue],Data[Region],Region,Data[Month],PrevMonth,Data[Year],IF(CurMonth=1,PrevYear,CurYear))

As a shortcut, we created a new filter using just the condition at the end:
IF(CurMonth=1,PrevYear,CurYear)

Then, we used Name Manager again to give this year a title (PMYear).Therefore, any time we need to use the IF condition to work around the previous month being December, we can simply use "PMYear" in the formula like a variable that stores an if condition.

Pro tip: We used a linked picture of a cell to retain the formatting otherwise lost by inserting a text box and referencing the cell alone. 

There's an issue when trying to [absolute] fix data when using tables in excel. Using F4 won't work on the named range. Here's the solution:
Data[Revenue]:[Revenue]
This ensures that we don't advance over to next column when auto-populating elsewhere. 
As in this case:
=SUMIFS(Data[[Revenue]:[Revenue]],Data[[Region]:[Region]],Region,Data[[Month]:[Month]],DataPrep!$G3,Data[[Year]:[Year]],DataPrep!H$2)

Pro Tip - Hiding 0 Values in a Line Chart:
Preface the formula with an IF condition that checks whether month in column G is GREATER THAN the CurMonth. If TRUE, return NA() (which excel recognizes as an Error value). ELSE, return the result of the original formula (above).

In the case of using negative values (MoM data) with a bar chart, he used the trick of selecting blank cells (as opposed to using the custom format code ;;; as this doesn't work with strings, only number values).

