# Gender Gap insights: Project overview
### [Excel | SQL | Tableau]
* Created a Tableau Dashboard to show the breakdown of male and female employees in various departments, to promote equal opportunities for everyone.
* This project could help improve gender gap policies in the organization and increase women’s employment in the local area by 7%.
* This project has various tables, totaling around 1.3 million data records, and did some SQL querying in the employee database to identify the relevant records to the analysis. 

### Resources and references used

**SQL+Tableau:** https://365datascience.com/courses/sql-tableau/

### Steps I have taken to complete this project:
**GitHub file name:** `Employees_mod` and `Gender_gap_Dashboard`

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/image_database.PNG "Relational Schema")

**1.** I wrote a SQL query in the MySQL database name `Employees_mod` to get the breakdown between the male and female employees working in the company each year, starting from 1990. Then I exported the SQL output into the CSV file name `Task 1_csv`, and then later on I imported this CSV file into Tableau as a Text file, then created chart 1 showing the cumulative breakdown between male and female employees starting from 1990 to 2002.


	SQL query used: 

```
SELECT
YEAR(d.from_date) AS Calender_year,
e.gender,
COUNT(e.emp_no) AS Num_of_employees
FROM
t_dept_emp d
JOIN
t_employees e ON d.emp_no = e.emp_no
GROUP BY Calender_year , e.gender
HAVING Calender_year >= 1990;
```
**SQL Output 1**

![SQL Output](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_SQL_output_task1.PNG "SQL Output 1")

**Tableau Chart 1**

![Tableau Chart 1](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_chart1.PNG "Tableau chart 1")



**2.** I wrote another SQL query to compare the number of male managers to the number of female managers from different departments for each year, starting from 1990. Exported the SQL result to the CSV file name `Task 2_csv`, and then created a Tableau chart 2 to give the breakdown of male and female managers in the different departments.


	SQL query used:

```
SELECT 
    d.dept_name,
    ee.gender,
    dm.emp_no,
    dm.from_date,
    dm.to_date,
    e.calendar_year,
    CASE
        WHEN
            YEAR(dm.from_date) <= e.calendar_year
                AND YEAR(dm.to_date) >= e.calendar_year
        THEN
            1
        ELSE 0
    END AS Active
FROM
    (SELECT 
        YEAR(hire_date) AS calendar_year
    FROM
        t_employees
    GROUP BY calendar_year) e
        CROSS JOIN
    t_dept_manager dm
        JOIN
    t_departments d ON d.dept_no = dm.dept_no
        JOIN
    t_employees ee ON dm.emp_no = ee.emp_no
ORDER BY dm.emp_no , e.calendar_year;
```
**SQL Output 2**

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_SQL_output_task2.PNG "SQL Output 2")

**Tableau Chart 2**

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_chart2.PNG "Tableau chart 2")



**3.** I wrote another SQL query in the same database to compare the average salary of female versus male employees in the entire company until the year 2002 and added a filter allowing us to see that per department. then I Exported the SQL results to the CSV file name `Task 3_csv`, and then created chart 3 in Tableau which gives the breakdown of average annual employee salary and can be filtered by gender and department name.

	SQL query used:

```
SELECT 
    e.gender,
    d.dept_name,
    ROUND(AVG(s.salary), 2) AS salary,
    YEAR(s.from_date) AS calendar_year
FROM
    t_salaries s
        JOIN
    t_employees e ON e.emp_no = s.emp_no
        JOIN
    t_dept_emp de ON e.emp_no = de.emp_no
        JOIN
    t_departments d ON d.dept_no = de.dept_no
GROUP BY d.dept_no , e.gender , calendar_year
HAVING calendar_year <= 2002
ORDER BY d.dept_no;
```
**SQL Output 3**

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_SQL_output_task3.PNG "SQL Output 3")

**Tableau Chart 3**

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_chart3.PNG "Tableau chart 3")


**4.** This time I created a stored procedure in SQL that allows us to obtain the average male and female salary per department within a certain salary range. This range is defined by two values the user can insert when calling the procedure. I selected (50000, 90000) to call this procedure, and exported the SQL output into the CSV file name `Task 4_csv`, later on, I created chart 4 in Tableau representing the average employee salary since 1990 with the additional breakdown of gender and department name.

	SQL query used:

```

drop procedure if exists filter_salary;

delimiter $$

create procedure filter_salary (in p_min_salary float, in p_max_salary float)
begin
select
	e.gender, d.dept_name, avg(s.salary) as avg_salary
from
	t_salaries s
		join
    t_employees e on s.emp_no = e.emp_no
		join
    t_dept_emp de on de.emp_no = e.emp_no
		join
    t_departments d on d.dept_no = de.dept_no
where salary between p_min_salary and p_max_salary
group by de.dept_no, e.gender
order by de.dept_no;
end $$

delimiter ;

call filter_salary(50000,90000);
```
**SQL Output 4**

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_SQL_output_task4.PNG "SQL Output 4")

**Tableau Chart 4**

![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_chart4.PNG "Tableau chart 4")

**5.** Lastly, I have created a complete Tableau dashboard combined with all 4 charts I have created. 

[Tableau Dashboard Public link](https://public.tableau.com/app/profile/inderjeet.singh4420/viz/GenderGap_16817125020040/Dashboard1)
![](https://github.com/Inder-rana/course_projects/blob/main/Gender_gap_SQL_Tableau/images/image_gender_gap_dashboard.PNG "Tableau complete Dashboard")







