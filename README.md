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

```
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
```

Above is the code and resulting table to produce data regarding retirement titles. 

Based on the results, it seems there are a large majority of potential retirees within this range of people born within the specified period of time.

*Unique Titles*

![Unique Titles](https://user-images.githubusercontent.com/6594718/163739574-89616035-67cb-43b6-8e10-26d947118454.png)

```
SELECT DISTINCT ON (emp_no) emp_no,
first_name,
last_name,
title
INTO unique_titles
FROM retirement_titles
ORDER BY emp_no, title DESC;
```

Above is the results and production of the Unique Titles data. Based on the results, the majority of potential retirees are senior staff, senior engineers, or engineers in general. A few technique leaders are present.

*Retiring Titles*

![Retiring Titles](https://user-images.githubusercontent.com/6594718/163739837-a47c5121-8fe4-4af8-97af-0710e1439aac.png)

```
SELECT COUNT(ut.emp_no),
ut.title
INTO retiring_titles
FROM unique_titles as ut
GROUP BY title 
ORDER BY COUNT(title) DESC;
```

Above is the code for the charts that denote retiring titles. A very large percentage of the retiring staff occupy senior titles, which implies that job openings for senior staff and senior engineers will have the biggest opportunities available in the near future.

*Mentorship Eligible Individuals*

![Mentorship Eligibility](https://user-images.githubusercontent.com/6594718/163740075-c9dff3a0-d477-410b-b1ca-4ea9b4ab8915.png)

```
SELECT DISTINCT ON(e.emp_no) e.emp_no, 
    e.first_name, 
    e.last_name, 
    e.birth_date,
    de.from_date,
    de.to_date,
    t.title
INTO mentorship_eligibility
FROM employees as e
Left outer Join dept_emp as de
ON (e.emp_no = de.emp_no)
Left outer Join titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY e.emp_no;
```

Above is the mentorship elibility data and the code used to create it.

*Summation of Results and Points*

- A large portion of potential retirees are senior staff or senior engineers, effectively senior positions. 37,462 individuals are from these positions, and out of a total of 90,398 retirees in total, that amounts to 41% in senior positions.
- 32,452 retirees are general staff, 29,415 are senior engineers, 14,221 are engineers, 8,047 are senior staff, 4,502 are technique leaders, and 1,761 are assistant engineers.
- The majority of the people in the potential retirees group started at their positions in the late 1980s or early 1990s.
- 1,940 individuals are eligible for mentorship among the group.

**Summary**

First, one of the main things that can be concluded from all this is that a large number of staff will need to be hired in the future, a sizable amount of senior positions will need to be filled, and especially engineer positions will be left vacant. 

With only 1,940 individuals eligible for mentorship, however, there aren't enough who can mentor potential new recruits, especially compared to the high number of expected retirees that will arise in the near future.
