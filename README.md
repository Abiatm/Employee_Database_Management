
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







 
