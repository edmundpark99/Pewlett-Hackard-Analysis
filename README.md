# Pewlett-Hackard-Analysis

**_Pewlett Hackard Analysis Challenge_**

**Overview**

This analysis aimed to assess Pewlett Hackard and look at how many employees are slated to retire soon. Via the use of SQL, an analysis was performed to see how many employees will retire soon, categorize them based on their title and position in Pewlett Hackard and to identify those who are eligible to partake in a mentorship program. 

**Results**

*Employee Database*

![EmployeeDB](https://user-images.githubusercontent.com/6594718/163733286-532ce558-6ee6-4ba3-95ed-5da5fe13a978.png)

Above is the image of all the original tables used to create the data and the connections made between shared variables.

*Retirement Titles*


![retirement titles](https://user-images.githubusercontent.com/6594718/163738941-caea2fdb-1134-4399-b59a-2d9962c8af2a.png)

///
SELECT e.emp_no,
       e.first_name,
       e.last_name,
       t.title,
       t.from_date,
       t.to_date
INTO retirement_titles
FROM employees as e
INNER JOIN titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
order by e.emp_no;
///
