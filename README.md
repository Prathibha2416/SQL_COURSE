# SQL_COURSE
All SQL basics and intermediate level



# COUNT, DISTINCT, LIMIT


# Exploring the Database

**Let us first explore the SanFranciscoFilmLocations database using the Datasette tool:**

**SELECT * FROM FilmLocations;**

These are the column attribute descriptions from the FilmLocations table:

FilmLocations(
Title:              titles of the films, 
ReleaseYear:        time of public release of the films, 
Locations:          locations of San Francisco where the films were shot, 
FunFacts:           funny facts about the filming locations, 
ProductionCompany:  companies who produced the films, 
Distributor:        companies who distributed the films, 
Director:           people who directed the films, 
Writer:             people who wrote the films, 
Actor1:             person 1 who acted in the films, 
Actor2:             person 2 who acted in the films,
Actor3:             person 3 who acted in the films
)



# Using COUNT statement

1) Suppose we want to count the number of records or rows of the "FilmLocations" table. The query for this would be:

   **SELECT COUNT(*) FROM FilmLocations;**

2) We want to count the number of locations of the films. But we also want to restrict the output result set so that we only retrieve the number
of locations of the films written by a certain writer. The query for this can be written as:

  **SELECT COUNT(Locations) FROM FilmLocations WHERE Writer="James Cameron";**

# Using DISTINCT statement

1) Assume that we want to retrieve the titles of all films in the table so that duplicates will be discarded in the output result set.

  **SELECT DISTINCT Title FROM FilmLocations;**

2) We want to retrieve the count of release years of the films produced by a specific company so that duplicate release years of those films will be discarded in the count.

   **SELECT COUNT(DISTINCT ReleaseYear) FROM FilmLocations WHERE ProductionCompany="Warner Bros. Pictures";**


# Using LIMIT statement

1) Retrieve only the first 25 rows from the table so that rows other than those are not in the output result set.

   **SELECT * FROM FilmLocations LIMIT 25;**

2) Now, we want to retrieve 15 rows from the table starting from row 11.

   **SELECT * FROM FilmLocations LIMIT 15 OFFSET 10;**

# Practice exercises

**COUNT**
1) Retrieve the number of locations of the films which are directed by Woody Allen.

   Query Solution

   **SELECT COUNT(Locations) FROM FilmLocations WHERE Director="Woody Allen";**

3) Retrieve the number of films shot at Russian Hill.

   Query Solution

   **SELECT Count(Title) FROM FilmLocations WHERE Locations="Russian Hill";**

5) Retrieve the number of rows having a release year older than 1950 from the "FilmLocations" table.

   Query Solution

   **SELECT Count(*) FROM FilmLocations WHERE ReleaseYear<1950;**


**DISTINCT**

1) Retrieve the names of all unique films released in the 21st century and onwards, along with their release years.

   Query Solution

   **SELECT DISTINCT Title, ReleaseYear FROM FilmLocations WHERE ReleaseYear>=2001;**

2) Retrieve the directors' names and their distinct films shot at City Hall.

   Query Solution

   **SELECT DISTINCT Title, Director FROM FilmLocations WHERE Locations="City Hall";**

3) Retrieve the number of distributors who distributed films with the 1st actor, Clint Eastwood.

   Query Solution
   
   **SELECT COUNT(DISTINCT Distributor) FROM FilmLocations WHERE Actor1="Clint Eastwood";**

**LIMIT**

1) Retrieve the names of the first 50 films.

   Query Solution
   
   **SELECT DISTINCT Title FROM FilmLocations LIMIT 50;**

2) Retrieve the first 10 film names released in 2015.

   Query Solution
   
   **SELECT DISTINCT Title FROM FilmLocations WHERE ReleaseYear=2015 LIMIT 10;** 

3) Retrieve the next 3 film names that follow after the first 5 films released in 2015.

   Query Solution

   **SELECT DISTINCT Title FROM FilmLocations WHERE ReleaseYear=2015 LIMIT 3 OFFSET 5;**

# String Patterns, Sorting and Grouping in MySQL

# String Patterns


You can use the LIKE operator to retrieve strings that contain the said text


**SELECT F_NAME, L_NAME
FROM EMPLOYEES
WHERE ADDRESS LIKE '%Elgin,IL%';**




Let us retrieve all employee records in department 5 where salary is between 60000 and 70000. The query that will be used is

**SELECT *
FROM EMPLOYEES
WHERE (SALARY BETWEEN 60000 AND 70000) AND DEP_ID = 5;**


# Sorting

**Sorting is done using the ORDER BY clause in your SQL query. By default, the ORDER BY clause sorts the records in ascending order.**


**SELECT F_NAME, L_NAME, DEP_ID 
FROM EMPLOYEES
ORDER BY DEP_ID;**


**get the output of the same query in descending order of department ID, and within each deaprtment, the records should be ordered in descending alphabetical order by last name. For descending order, you can make use of the DESC clause.**


**SELECT F_NAME, L_NAME, DEP_ID 
FROM EMPLOYEES
ORDER BY DEP_ID DESC, L_NAME DESC;**

# Grouping

A good example of grouping would be if For each department ID, we wish to retrieve the number of employees in the department.

**SELECT DEP_ID, COUNT(*)
FROM EMPLOYEES
GROUP BY DEP_ID;**


Now, for each department, retrieve the number of employees in the department and the average employee salary in the department. For this, you can use COUNT(*) to retrieve the total count of a column, and AVG() function to compute average salaries, and then GROUP BY.

**SELECT DEP_ID, COUNT(*), AVG(SALARY)
FROM EMPLOYEES
GROUP BY DEP_ID;**


You can refine your outut by using appropriate labels for the columns of data retrieved. Label the computed columns in the result set of the last problem as NUM_EMPLOYEES and AVG_SALARY.

**SELECT DEP_ID, COUNT(*) AS "NUM_EMPLOYEES", AVG(SALARY) AS "AVG_SALARY"
FROM EMPLOYEES
GROUP BY DEP_ID;**


You can also combine the usage of GROUP BY and ORDER BY statements to sort the output of each group in accordance with a specific parameter. It is important to note that in such a case, ORDER BY clause muct be used after the GROUP BY clause. For example, we can sort the result of the previous query by average salary. The SQL query would thus become


**SELECT DEP_ID, COUNT(*) AS "NUM_EMPLOYEES", AVG(SALARY) AS "AVG_SALARY"
FROM EMPLOYEES
GROUP BY DEP_ID
ORDER BY AVG_SALARY;**


In case you need to filter a grouped response, you have to use the HAVING clause. In the previous example, if we wish to limit the result to departments with fewer than 4 employees, We will have to use HAVING after the GROUP BY, and use the count() function in the HAVING clause instead of the column label.


**SELECT DEP_ID, COUNT(*) AS "NUM_EMPLOYEES", AVG(SALARY) AS "AVG_SALARY"
FROM EMPLOYEES
GROUP BY DEP_ID
HAVING count(*) < 4
ORDER BY AVG_SALARY;**


# Practice Questions

Retrieve the list of all employees, first and last names, whose first names start with ‘S’.

**SELECT F_NAME, L_NAME
FROM EMPLOYEES
WHERE F_NAME LIKE 'S%';**

Arrange all the records of the EMPLOYEES table in ascending order of the date of birth.

**SELECT *
FROM EMPLOYEES
ORDER BY B_DATE;**

Group the records in terms of the department IDs and filter them of ones that have average salary more than or equal to 60000. Display the department ID and the average salary.

**SELECT DEP_ID, AVG(SALARY)
FROM EMPLOYEES
GROUP BY DEP_ID
HAVING AVG(SALARY) >= 60000;**

For the problem above, sort the results for each group in descending order of average salary.

**SELECT DEP_ID, AVG(SALARY)
FROM EMPLOYEES
GROUP BY DEP_ID
HAVING AVG(SALARY) >= 60000
ORDER BY AVG(SALARY) DESC;**


# Built-in Functions

# Objectives

After completing this lab, you will be able to compose queries in phpMyAdmin with MySQL using:

**Aggregation Functions**

**Scalar Functions**

**String Functions**

**Date Functions**



# Aggregation Functions

Write a query that calculates the total cost of all animal rescues in the PETRESCUE table.

For this query, we will use the function SUM(COLUMN_NAME). The output of this query will be the total value of all elements in the column. The query for this question can be written as:


**SELECT SUM(COST) FROM PETRESCUE;**

You can further assign a label to the query SUM_OF_COST.


**SELECT SUM(COST) AS SUM_OF_COST FROM PETRESCUE;**

Write a query that displays the maximum quantity of animals rescued (of any kind).

For this query, we will use the function MAX(COLUMN_NAME). The output of this query will be the maximum value of all elements in the column. The query for this question can be written as:


**SELECT MAX(QUANTITY) FROM PETRESCUE;**

The query can easily be changed to display the minimum quantity using the MIN function instead.

**SELECT MIN(QUANTITY) FROM PETRESCUE;**

Write a query that displays the average cost of animals rescued.

For this query, we will use AVG(COLUMN_NAME). The output of this query will be the average of all elements in the column. The query for this question can be written as


**SELECT AVG(COST) FROM PETRESCUE;**


# Scalar Functions and String Functions

Write a query that displays the rounded integral cost of each rescue.
For this query, we will use the function ROUND(COLUMN_NAME, NUMBER_OF_DECIMALS). The output of this query will be the value of each element in the column rounded to the specified number of decimal places. Note that the second argument is optional and, if omitted, results in rounding to an integer value. The query for this question can be written as:

1
**SELECT ROUND(COST) FROM PETRESCUE;**

The query could also be written as:

1
**SELECT ROUND(COST, 0) FROM PETRESCUE;**

In case the question was to round the value to 2 decimal places, the query would change to:

1
**SELECT ROUND(COST, 2) FROM PETRESCUE;**

Write a query that displays the length of each animal name.
For this query, we will use the function LENGTH(COLUMN_NAME). The output of this query will be the length of each element in the column. The query for this question can be written as:

1
**SELECT LENGTH(ANIMAL) FROM PETRESCUE;**

Write a query that displays the animal name in each rescue in uppercase.
For this query, we will use the function UCASE(COLUMN_NAME). The output of this query will be each element in the column in upper case letters. The query for this question can be written as:

1
**SELECT UCASE(ANIMAL) FROM PETRESCUE;**

Just as easily, the user could ask for a lower case representation, and the query would be changed to:

1
**SELECT LCASE(ANIMAL) FROM PETRESCUE;**

# Date Functions
Write a query that displays the rescue date.
For this query, we will use the function DAY(COLUMN_NAME). The output of this query will be only the DAY part of the date in the column. The query for this question can be written as:

1
**SELECT DAY(RESCUEDATE) FROM PETRESCUE;**

In case the query was asking for MONTH of rescue, the query would change to:

1
**SELECT MONTH(RESCUEDATE) FROM PETRESCUE;**

In case the query was asking for YEAR of rescue, the query would change to:

1
**SELECT YEAR(RESCUEDATE) FROM PETRESCUE;**

Animals rescued should see the vet within three days of arrival. Write a query that displays the third day of each rescue.
For this query, we will use the function DATE_ADD(COLUMN_NAME, INTERVAL Number Date_element). Here, the quantity in Number and in Date_element will combine to form the interval to be added to the date in the column. For the given question, the query would be:

1
**SELECT DATE_ADD(RESCUEDATE, INTERVAL 3 DAY) FROM PETRESCUE**

If the question was to add 2 months to the date, the query would change to:

1
**SELECT DATE_ADD(RESCUEDATE, INTERVAL 2 MONTH) FROM PETRESCUE**

Similarly, we can retrieve a date before the one given in the column by a given number using the function DATE_SUB. By modifying the same example, the following query would provide the date 3 days before the rescue.

1
**SELECT DATE_SUB(RESCUEDATE, INTERVAL 3 DAY) FROM PETRESCUE**

Write a query that displays the length of time the animals have been rescued, for example, the difference between the current date and the rescue date.
For this query, we will use the function DATEDIFF(Date_1, Date_2). This function calculates the difference between the two given dates and gives the output in number of days. For the given question, the query would be:

1
**SELECT DATEDIFF(CURRENT_DATE, RESCUEDATE) FROM PETRESCUE**

CURRENT_DATE is also an inbuilt function that returns the present date as known to the server.

To present the output in a YYYY-MM-DD format, another function FROM_DAYS(number_of_days)can be used. This function takes a number of days and returns the required formatted output. The query above would thus be modified to

1
**SELECT FROM_DAYS(DATEDIFF(CURRENT_DATE, RESCUEDATE)) FROM PETRESCUE**



# Practice Problems
Write a query that displays the average cost of rescuing a single dog. Note that the cost per dog would not be the same in different instances.

**SELECT AVG(COST/QUANTITY) FROM PETRESCUE WHERE ANIMAL = 'Dog';**

Write a query that displays the animal name in each rescue in uppercase without duplications.

**SELECT DISTINCT UCASE(ANIMAL) FROM PETRESCUE;**

Write a query that displays all the columns from the PETRESCUE table where the animal(s) rescued are cats. Use cat in lowercase in the query.

**SELECT * FROM PETRESCUE WHERE LCASE(ANIMAL)="cat";**

Write a query that displays the number of rescues in the 5th month.

**SELECT SUM(QUANTITY) FROM PETRESCUE WHERE MONTH(RESCUEDATE)="05";**

The rescue shelter is supposed to find good homes for all animals within 1 year of their rescue. Write a query that displays the ID and the target date.

**SELECT ID, DATE_ADD(RESCUEDATE, INTERVAL 1 YEAR) FROM PETRESCUE;**



# Sub-queries and Nested Selects
Say you are asked to retrieve all employee records whose salary is lower than the average salary. You might use the following query to do this.


**SELECT * 
FROM EMPLOYEES 
WHERE salary < AVG(salary);**

However, this query will generate an error stating, "Illegal use of group function." Here, the group function is AVG and cannot be used directly in the condition since it has not been retrieved from the data. Therefore, the condition will use a sub-query to retrieve the average salary information to compare the existing salary. The modified query would become:


**SELECT *
FROM EMPLOYEES
WHERE SALARY < (SELECT AVG(SALARY) FROM EMPLOYEES);**

Now, consider executing a query that retrieves all employee records with EMP_ID, SALARY, and maximum salary as MAX_SALARY in every row. For this, the maximum salary must be queried and used as one of the columns. This can be done using the query below.


**SELECT EMP_ID, SALARY, (SELECT MAX(SALARY) FROM EMPLOYEES) AS MAX_SALARY 
FROM EMPLOYEES;**

Now, consider that you wish to extract the first and last names of the oldest employee. Since the oldest employee will be the one with the smallest date of birth, the query can be written as:


**SELECT F_NAME, L_NAME
FROM EMPLOYEES
WHERE B_DATE = (SELECT MIN(B_DATE) FROM EMPLOYEES);**

You may also use sub-queries to create derived tables, which can then be used to query specific information. Say you want to know the average salary of the top 5 earners in the company. You will first have to extract a table of the top five salaries as a table. From that table, you can query the average value of the salary. The query can be written as follows.


**SELECT AVG(SALARY) 
FROM (SELECT SALARY 
      FROM EMPLOYEES 
      ORDER BY SALARY DESC 
      LIMIT 5) AS SALARY_TABLE;**

# Practice Problems

Write a query to find the average salary of the five least-earning employees.

**SELECT AVG(SALARY) 
FROM (SELECT SALARY 
      FROM EMPLOYEES 
      ORDER BY SALARY 
      LIMIT 5) AS SALARY_TABLE;**

Write a query to find the records of employees older than the average age of all employees.


**SELECT * 
FROM EMPLOYEES 
WHERE YEAR(FROM_DAYS(DATEDIFF(CURRENT_DATE,B_DATE))) > 
    (SELECT AVG(YEAR(FROM_DAYS(DATEDIFF(CURRENT_DATE,B_DATE)))) 
    FROM EMPLOYEES);**

From the Job_History table, display the list of Employee IDs, years of service, and average years of service for all entries.

**SELECT EMPL_ID, YEAR(FROM_DAYS(DATEDIFF(CURRENT_DATE, START_DATE))), 
    (SELECT AVG(YEAR(FROM_DAYS(DATEDIFF(CURRENT_DATE, START_DATE)))) 
    FROM JOB_HISTORY)
FROM JOB_HISTORY;**

