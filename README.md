# MySql Join Queries

## 1 Write a query to get the department name and number of employees in the department.

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

# 2 Write a query to find the employee ID, job title, number of days between ending date and starting date for all jobs in department 90 from job history.

```sql
SELECT
  E.EMPLOYEE_ID,
  J.JOB_TITLE,
DATEDIFF(H.END_DATE, H.START_DATE) AS DAYS_IN_LABOR
FROM
  Employees E
  INNER JOIN Jobs J
  ON E.JOB_ID = J.JOB_ID
  INNER JOIN JobHistory H
  ON E.EMPLOYEE_ID = H.EMPLOYEE_ID
WHERE
  H.DEPARTMENT_ID = 90
```

# 3 Write a query to display the department ID and name and first name of manager.

```sql
SELECT
  E.FIRST_NAME,
  E.LAST_NAME,
  D.DEPARTMENT_ID
FROM
  Employees E
INNER JOIN Departments D
  ON E.EMPLOYEE_ID = D.MANAGER_ID
```

# 4 Write a query to display the department name, manager name, and city.

```sql
SELECT
  D.DEPARTMENT_NAME,
  CONCAT(E.FIRST_NAME, ' ', E.LAST_NAME) AS MANAGER,
  L.CITY
FROM
  Departments D
INNER JOIN Employees E
  ON E.EMPLOYEE_ID = D.MANAGER_ID
INNER JOIN Locations L
  ON D.LOCATION_ID = L.LOCATION_ID
```

# 5 Write a query to display the job title and average salary of employees.

```sql
SELECT
  J.JOB_TITLE,
  AVG(DISTINCT E.SALARY) AS AVERAGE_SALARY
FROM
  Jobs J
INNER JOIN Employees E
  ON J.JOB_ID = E.JOB_ID
GROUP BY J.JOB_ID
```

# 6 Write a query to display job title, employee name, and the difference between salary of the employee and minimum salary for the job.

```sql
SELECT
  J.JOB_TITLE,
  CONCAT(E.FIRST_NAME, ' ', E.LASTNAME) AS EMPLOYEE_NAME,
  (E.SALARY - J.MIN_SALARY) AS OVER_MIN_WAGE
FROM
  Jobs J
INNER JOIN Employees E
  ON J.JOB_ID = E.JOB_ID
```

# 7 Write a query to display the job history that were done by any employee who is currently drawing more than 10000 of salary.

```sql
SELECT
  CONCAT(E.FIRST_NAME, ' ', E.LAST_NAME) AS EMPLOYEE,
  CONCAT('From ', H.START_DATE, ' to ', H.END_DATE) AS WORKSPAN,
  J.JOB_TITLE,
  D.DEPARTMENT_NAME
FROM
  Employees E
INNER JOIN JobHistory H
  ON E.EMPLOYEE_ID = H.EMPLOYEE_ID
INNER JOIN Jobs J
  ON E.JOB_ID = J.JOB_ID
INNER JOIN Departments D
  ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
WHERE
  E.SALARY > 10000
```

# 8 Write a query to display department name, name (first_name, last_name), hire date, salary of the manager for all managers whose experience is more than 15 years.

```sql
SELECT
  D.DEPARTMENT_NAME,
  CONCAT(E.FIRST_NAME, ' ', E.LAST_NAME) AS NAME,
  E.HIRE_DATE,
  E.SALARY,
  DATEDIFF(CURDATE(), E.HIRE_DATE) / 365 AS EXPERIENCE
FROM
  Departments D
INNER JOIN Employees E
  ON E.EMPLOYEE_ID = D.MANAGER_ID
WHERE
  DATEDIFF(CURDATE(), E.HIRE_DATE) > (15*365)
```