# P&L from scratch: Project Overview
### [Excel | Charts]
*	Created a Profit & Loss statement in Excel to help business stakeholders understand their organization’s financial health, based on the data insights they can make informed financial decisions.
*	This project could help organization decrease their unnecessary expenses by 10%
*	I have utilized the P&L Extractions from FY2016, 2017, and 2018, Extractions have around 335 data records, did some data cleaning and got rid of some null values, and created a mapping column for easier analysis by categorizing common P&L items.

### Resources and References used
**Intro to Excel:** https://365datascience.com/courses/introduction-to-microsoft-excel/

### Steps I have taken to complete this project:
**Github file name:** `Before_P&L` is an incomplete file and `After_P&L` is a complete file, open these files and follow along with the described steps below.

1. First, I went through the raw financial extractions of FY2016, FY2017, and FY2018. Then, I Tried to get a feel for the data and its components, it consists of various columns, like type of P&L account, partner company code, amounts, and account number.

2. Then I cleaned some data in the Partner company column as there were some alphabetic values named `total` that were not aligned with the rest of the data, I used a filter to bring them up and then deleted all the rows.

3. Then I added an extra column named `code` it has a unique code for each line of the row.

4. Then I created a new sheet named `Database` with column names: Code, P&L account, partner company, name of the partner company, FY16, and FY18. I filled these columns using Vlookup and Sumif functions.

5. Then I created a Mapping column in the Database sheet, it is a high-level categorization of the common items of the P&L account, this mapping column is the key to creating our P&L statement.

6. Then I created the P&L statement based on mapping column categories and filled the FY16, FY17, and FY18 data using sumif function. Also created the year-on-year % variation of FY16-17 and FY17-18. 

7. Then I created the KPIs and Net income check table, this net income check table helps us to find out if there is any error in the numerical data, it is a great preventive measure against any inaccurate information, any inaccurate changes, or typing errors to other sheet's numerical data will be reflected here.

8. To find out any error in numerical data or to check whether a specific row is accounted for in the final calculation or not, to do that I have created an extra column named `Count_check` in the database sheet, it uses a count if function to check, if a particular row is included in the calculation or not, by representing 1 means it is included, and by representing 0 means not included.

9. Lastly I have created a stacked column chart to give a revenue breakdown between FY16-FY18, and a Bridge chart to give a breakdown between EBITDA FY17-FY18.
  
![](https://github.com/Inder-rana/course_projects/blob/main/Excel_P%26L/image_P%26L.PNG)

