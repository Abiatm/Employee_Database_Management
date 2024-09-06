
### INTRODUCTION
In order to organize employee data for easy analysis,evaluation of their works and for promotion,the management demand that a single database system is made.
### PROBLEM STATEMENT

- Ques.1. Write a SQL query to fetch the list of employees with same salary.

- Ques.2. Write a SQL query to fetch Find the second highest salary and the department and name of the earner.

- Ques.3. Write a query to get the maximum salary from each department, the name of the department and the name of the earner. 

- Ques.4. Write a SQL query to fetch count of project managers that are in each department

- Ques.5. Write a query to fetch only the first name from the EmpName column of Employee table and after that add the salary for example- empname is “Amit singh”  and salary is 10000 then output should be Amit_10000

- Ques.6. Write a SQL query to fetch only odd salaries from from the employee table

- Ques.7. Create a view  to fetch EmpID,Empname, Departmantname, ProjectMangerName where salary is greater than 30000.

### DATA ANALYSIS
- To obtain the employee with same salary i created double table from employee table and with the use of join and where clause the employees with same salary was obtained.
- To obtain the second highest salary a temporary table called 'EmployeeRanking' ,also with use of dense rank ,the required salary was obtained.
- Here employee table,department table and with  use of dense-rank  the required result was obtained.
- Here count,group by,order by and join command was used.
- To obtain the reqired output such as 'Monika_10000' key commands like 'parsename,replace,cast' was used.
- For old salary modulus division was used which takes the old part of the division done.
- The function 'CREATE VIEW' was used to ahieve the needed result.
### QUERY
```
--(1)--
  SELECT E1.EmpName Employee1,E2.EmpName Sharing_same_Salary_With_Emp,E1.Salary
  FROM [EmployeDbForHrDept].[dbo].[Employee] E1
  LEFT JOIN [EmployeDbForHrDept].[dbo].[Employee] E2
  ON E1.Salary=E2.Salary AND E1.EmpID<E2.EmpID  --By position arrangement A01<B01 so E1.EmpName Employee1 comes first before E2.EmpName 
  WHERE E2.Salary IS NOT NULL AND E1.Salary IS NOT NULL

  -----(2)---
--WITH creates a temporary table(EmployeeRanking) that doesn't show on database Table
WITH EmployeeRanking AS (SELECT EM.Salary,EM.EmpID,EM.EmpName,DP.DepartmentName,EM.DepartmentID,DENSE_RANK() OVER (ORDER BY EM.Salary DESC) AS Ranking --Generate reapeted values for reapeted salary
FROM [EmployeDbForHrDept].[dbo].[Employee] EM
LEFT JOIN [EmployeDbForHrDept].[dbo].[Department] AS DP
ON DP.DepartmentID=EM.DepartmentID
)
SELECT EmpName Employee_Name,Salary,DepartmentName Department_Name FROM EmployeeRanking
WHERE Ranking=2

--(3)
WITH Employees_Rank AS (
    SELECT *,
           DENSE_RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Ranking --partition brings the deptID together,while dense rankscores them by their salaries in sequential_order
    FROM [EmployeDbForHrDept].[dbo].[Employee]
)
SELECT E.EmpName,E.Salary,D.DepartmentName
FROM Employees_Rank E
LEFT JOIN [EmployeDbForHrDept].[dbo].[Department] D
ON D.DepartmentID = E.DepartmentID
WHERE E.Ranking = 1 --since at all the no_1 position the values is the highest;

--(4)--
--count of project managers that are in each department
With PRoject_manag_count AS (
SELECT * FROM [EmployeDbForHrDept].[dbo].[Projectmanager]  )
SELECT DepartmentName,COUNT(ProjectManagerID) ProjectManager_count  FROM PRoject_manag_count PMC
LEFT JOIN [EmployeDbForHrDept].[dbo].[Department] DE
ON DE.DepartmentID=PMC.DepartmentID
GROUP BY DepartmentName
ORDER BY  ProjectManager_count  DESC

-------(5) SOLUTION------
SELECT PARSENAME(REPLACE(EmpName, ' ', '.'), 2) + '_' + CAST(Salary AS VARCHAR) AS FIRSTNAME_SALARY
FROM [EmployeDbForHrDept].[dbo].[Employee];

---------------------OR---------------------------------
SELECT SUBSTRING(EmpName, 1, CHARINDEX(' ', EmpName)) + '_' + CAST(Salary AS VARCHAR) AS FIRSTNAME_SALARY
FROM [EmployeDbForHrDept].[dbo].[Employee];

--(6)SOLUTION----------------------
  SELECT * FROM [EmployeDbForHrDept].[dbo].[Employee] 
  WHERE Salary%2 !=0 --(The result is an empty cell since the whole salaries value are divisible by 2
  --(here modulus division method was used)
---(7)SOLUTION-----------
  CREATE VIEW vw_SALARY_Joins AS
  SELECT EMP.EmpID,EMP.EmpName,DEP.DepartmentName,PRO.ProjectManagerName FROM [EmployeDbForHrDept].[dbo].[Employee] EMP
  LEFT JOIN [EmployeDbForHrDept].[dbo].[Department] DEP
  ON DEP.DepartmentID=EMP.DepartmentID
  LEFT JOIN [EmployeDbForHrDept].[dbo].[Projectmanager] PRO
  ON DEP.DepartmentID=PRO.DepartmentID
  WHERE EMP.Salary>30000

--(8)-----
  CREATE VIEW vw_TOP_EARNERS AS
  
WITH Employees_Rank AS (
    SELECT *,
           DENSE_RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Ranking --partition brings the deptID together,while dense rankscores them by their salaries in sequential_order
    FROM [EmployeDbForHrDept].[dbo].[Employee]
)
SELECT E.EmpName,D.DepartmentName
FROM Employees_Rank E
LEFT JOIN [EmployeDbForHrDept].[dbo].[Department] D
ON D.DepartmentID = E.DepartmentID
WHERE E.Ranking = 1 


```
### IMAGE
![Employee_PICX](https://github.com/user-attachments/assets/6928726a-e0f1-4020-a528-d9334516a6c4)

### OBSERVATIONS
- Employee names like 'Monika singh,Sunil Rana' shares same salary of 10000,also employee names like 'Vipul Gupta,Satish Sharama' shares the same salary of 45000, but other employees has no pair in share of same salary.
- Two employees shares same salary of 45000.
- None of the employee is earning an odd number salary.
- For easy payment structure the append of name and salary can help for easy payment structure and promotion.
### RECOMMENDATIONS
- Employees satisfaction programs should be encourage to avoid sudden attrition or resignation.
- More project managers as needed as some department has more employee more than others.
- Use of more states should be encouraged.







 
