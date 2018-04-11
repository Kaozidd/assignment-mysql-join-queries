#MySql Join Queries

##1 Write a query to get the department name and number of employees in the department.

```sql
SELECT 
  E.DEPARTMENT_ID , 
  D.DEPARTMENT_NAME , 
  COUNT(*)
FROM Employees E
INNER JOIN Departments D
ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
GROUP BY E.DEPARTMENT_ID;
```

#2 Write a query to find the employee ID, job title, number of days between ending date and starting date for all jobs in department 90 from job history.

#3 Write a query to display the department ID and name and first name of manager.

#4 Write a query to display the department name, manager name, and city.

#5 Write a query to display the job title and average salary of employees.

#6 Write a query to display job title, employee name, and the difference between salary of the employee and minimum salary for the job.

#7 Write a query to display the job history that were done by any employee who is currently drawing more than 10000 of salary.

#8 Write a query to display department name, name (first_name, last_name), hire date, salary of the manager for all managers whose experience is more than 15 years.