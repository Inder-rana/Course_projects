# Gender Gap insights: Project overview
### [SQL | Tableau]

* Created a Tableau dashboard showing the breakdown of male and females employees based on their average annual salary, number of employees working, number of managers   per department and average employee salary since 1990.
* The insights based on this tableau dashboard can help organization improve their gender gap policies and encourage equal opportunity for everyone.

### Resources and references used

**SQL+Tableau:** https://365datascience.com/courses/sql-tableau/

### Steps I have taken to complete this project:
**GitHub file name:** `Employees_mod` and `Gender_gap_Dashboard`

1. I write a SQL query in the MySQL database name `Employees_mod` to get the breakdown between the male and female employees working in the company each year, starting from 1990. Then I exported the SQL output into the CSV file name `Task 1_csv`, and then later on I imported this CSV file into Tableau as a Text file, then create a chart 1 showing the cumulative breakdown between male and female employees starting from 1990 to 2002.

   SQL query used: 
	```sql 
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
			
			
			
			
			
			
			
	
2. I write another SQL query to compare the number of male managers to the number of female managers from different departments for each year, starting from 1990. Exported the SQL result to the CSV file name `Task 2_csv`, and then created a Tableau chart 2 to give the breakdown of male and females managers in the different departments.

  Sql query used:
  
  `select
	  d.dept_name,
	  ee.gender,
	  dm.emp_no,
	  dm.from_date,
	  dm.to_date,
	  e.calendar_year,
	  case when year(dm.from_date) <= e.calendar_year and year(dm.to_date) >= e.calendar_year then 1 else 0 end as Active
  from 
	  (select 
		  year(hire_date) as calendar_year
       from
		  t_employees
        group by calendar_year) e
		  cross join
		  t_dept_manager dm
        join
      t_departments d on d.dept_no = dm.dept_no
        join
      t_employees ee on dm.emp_no = ee.emp_no
  order by dm.emp_no, e.calendar_year;`  


3. I write another SQL query in the same database to compare the average salary of female versus male employees in the entire company until year 2002, and add a filter allowing us to see that per each department. then I Exported the SQL results to the CSV file name `Task 3_csv`, and then created chart 3 in Tableau which gives the breakdown of average annual employee salary and can be filtered by gender and department name.

Sql query used:
select 
	e.gender, d.dept_name, round(avg(s.salary),2) as salary, year(s.from_date) as calendar_year
from
	t_salaries s
		join
     t_employees e on e.emp_no = s.emp_no
		join
     t_dept_emp de on e.emp_no= de.emp_no
		join
     t_departments d on d.dept_no = de.dept_no
group by d.dept_no, e.gender, calendar_year
having calendar_year <= 2002
order by d.dept_no;

4. This time I created a stored procedure in SQL that allow us to obtain the average male and female salary per department within a certain salary range. This range be defined by two values the user can insert when calling the procedure. I have select (50000, 90000) to call this procedure, and exported the SQL output into the CSV file name `Task 4_csv`, later on I created the chart 4 in Tableau representing the average employee salary since 1990 with the additional breakdown of gender and department name.

SQL query used:
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


5. Lastly, I have created a complete Tableau dashboard combined with all the 4 charts I have created. 



