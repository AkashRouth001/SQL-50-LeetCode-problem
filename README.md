![App Screenshot](https://github.com/AkashRouth001/SQL-50-LeetCode-problem/blob/ee5262e049a5e836cc9344b8645d8f338ff6267d/Screenshot%202024-11-27%20210901.png)
# SQL 50 LeetCode problem
Solutions for [SQL 50 Study Plan](https://leetcode.com/studyplan/top-sql-50/) on LeetCode
# Select
## [1757 - Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)

## Table: Products


| Column Name | Type    |
--------------|-----------
| product_id|int|
| low_fats    | enum    |
| recyclable  | enum    |

|  Field | Type |
|-------|-----|
| ID  | NUMBER |
| NAME | VARCHAR2(17)   |
| COUNTRY CODE  | VARCHAR2(3)  |
| DISTRICT |  VARCHAR2(20) |
| POPULATION | NUMBER |

product_id is the primary key (column with unique values) for this table.
low_fats is an ENUM (category) of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM (category) of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.

## Problem Statement

Write a solution to find the ids of products that are both low fat and recyclable.

Return the result table in any order.

The result format is in the following example:

### Example 1:

**Input:**  
Products table:  


| product_id  | low_fats | recyclable |  
-------------|----------|------------
| 0           | Y        | N          |  
| 1           | Y        | Y          |  
| 2           | N        | Y          |  
| 3           | Y        | Y          |  
| 4           | N        | N          |  


**Output:**  

 
| product_id  |  
--------------|
| 1           |  
| 3           |  


**Explanation:**  
Only products 1 and 3 are both low fat and recyclable.

## ANSWER
```sql
SELECT product_id  FROM Products
WHERE (low_fats = 'Y') AND (recyclable = 'Y');
```

---------------------------------------
  
## [584 - Find Customer Referee](https://leetcode.com/problems/find-customer-referee)

## Table: Customer

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| referee_id  | int     |

id is the primary key column for this table.  
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.

## Problem Statement

Write a solution to find the names of the customers that are **not referred** by the customer with `id = 2`.

Return the result table in any order.

The result format is in the following example:

### Example 1:

**Input:**  
Customer table:  

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |

**Output:**  

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |

**Explanation:**  
Only `Alex` and `Mark` are referred by the customer with `id = 2`.  
Thus, all other customers (`Will`, `Jane`, `Bill`, `Zack`) are included in the output.

## ANSWER
```sql
SELECT name from Customer
WHERE (not referee_id = 2)
OR (referee_id is null) ;
```

-------------------------------------------------------------------------

## [595 - Big Countries](https://leetcode.com/problems/big-countries/)
## Table: World

| Column Name | Type    |
|-------------|---------|
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | bigint  |

- **name** is the primary key (column with unique values) for this table.
- Each row provides information about a country's name, its continent, area (in km²), population, and GDP.

### Definition of "Big Country":
A country is classified as **big** if:
- Its area is at least 3,000,000 (3000000 km²), or
- Its population is at least 25,000,000 (25000000).

## Problem Statement

Write a solution to find the `name`, `population`, and `area` of the **big countries**.  
Return the result table in any order.

### Example 1:

**Input:**  
World table:

| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

**Output:**  

| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |

**Explanation:**  
- Afghanistan is classified as a big country because its population exceeds 25,000,000.  
- Algeria is classified as a big country because its population exceeds 25,000,000.  

## Answer
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
```
------------------------------------
## [1148 - Article Views I](https://leetcode.com/problems/article-views-i)
## Table: Views

| Column Name   | Type    |
|---------------|---------|
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |

- The table has no primary key and may contain duplicate rows.
- Each row indicates that a `viewer_id` viewed an `article_id` authored by `author_id` on a specific `view_date`.
- Note: `author_id` and `viewer_id` being equal implies that an author viewed their own article.

## Problem Statement

Write a solution to find all the authors (`author_id`) who have viewed at least one of their own articles.  
Return the result table sorted by `id` (author_id) in ascending order.

### Example 1:

**Input:**  
Views table:

| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |

**Output:**  

| id   |
|------|
| 4    |
| 7    |

**Explanation:**  
- Author `7` viewed their own article (`viewer_id = author_id = 7`).  
- Author `4` viewed their own article (`viewer_id = author_id = 4`).  

## Answer
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE  author_id = viewer_id
ORDER BY id ASC;
```
------------------------------------------------
## [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50)
## Table: Tweets

| Column Name | Type    |
|-------------|---------|
| tweet_id    | int     |
| content     | varchar |

- **tweet_id** is the primary key for this table.
- Each row contains the `tweet_id` and its `content` (the text of the tweet).

## Problem Statement

Write a solution to find the IDs of the **invalid tweets**.  
A tweet is invalid if the number of characters in its `content` exceeds 15.

Return the result table in any order.

### Example 1:

**Input:**  
Tweets table:

| tweet_id | content                           |
|----------|-----------------------------------|
| 1        | Let us Code                       |
| 2        | More than fifteen chars are here! |

**Output:**  

| tweet_id |
|----------|
| 2        |

**Explanation:**  
- Tweet with `tweet_id = 1` has content length = 11. It is valid.  
- Tweet with `tweet_id = 2` has content length = 33. It is invalid.  

## Answer
```sql
SELECT tweet_id FROM Tweets
WHERE LENGTH(content)>15;
```

# Basic Joins

## [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/)  
## Tables: Employees, EmployeeUNI  

### Employees Table  

| Column Name | Type    |  
|-------------|---------|  
| id          | int     |  
| name        | varchar |  

- **id** is the primary key for this table.  
- Each row contains the `id` and the `name` of an employee in the company.  

### EmployeeUNI Table  

| Column Name | Type    |  
|-------------|---------|  
| id          | int     |  
| unique_id   | int     |  

- **(id, unique_id)** is the primary key for this table.  
- Each row contains the `id` of an employee and the corresponding `unique_id` in the company.  

## Problem Statement  

Write a solution to show the **unique ID** of each user. If a user does not have a unique ID, show `null` instead.  

Return the result table in any order.  

### Example 1:  

**Input:**  
Employees table:  

| id | name     |  
|----|----------|  
| 1  | Alice    |  
| 7  | Bob      |  
| 11 | Meir     |  
| 90 | Winston  |  
| 3  | Jonathan |  

EmployeeUNI table:  

| id | unique_id |  
|----|-----------|  
| 3  | 1         |  
| 11 | 2         |  
| 90 | 3         |  

**Output:**  

| unique_id | name     |  
|-----------|----------|  
| null      | Alice    |  
| null      | Bob      |  
| 2         | Meir     |  
| 3         | Winston  |  
| 1         | Jonathan |  

**Explanation:**  
- Alice and Bob do not have a unique ID, so we show `null` for them.  
- Meir's unique ID is 2.  
- Winston's unique ID is 3.  
- Jonathan's unique ID is 1.  

## Answer  
```sql
SELECT unique_id , name
FROM Employees AS E
LEFT JOIN EmployeeUNI AS EU
ON E.id = EU.id;
```
-------------------------------
## [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/)  
## Tables: Sales, Product  

### Sales Table  

| Column Name | Type  |  
|-------------|-------|  
| sale_id     | int   |  
| product_id  | int   |  
| year        | int   |  
| quantity    | int   |  
| price       | int   |  

- **(sale_id, year)** is the primary key for this table.  
- **product_id** is a foreign key referencing the `product_id` in the **Product** table.  
- Each row represents a sale of the product with `product_id` in a specific year.  
- The `price` is the unit price of the product.  

### Product Table  

| Column Name  | Type    |  
|--------------|---------|  
| product_id   | int     |  
| product_name | varchar |  

- **product_id** is the primary key for this table.  
- Each row indicates the `product_name` corresponding to a `product_id`.  

## Problem Statement  

Write a solution to report the **product_name**, **year**, and **price** for each sale in the **Sales** table.  

Return the resulting table in any order.  

### Example 1:  

**Input:**  
Sales table:  

| sale_id | product_id | year | quantity | price |  
|---------|------------|------|----------|-------|  
| 1       | 100        | 2008 | 10       | 5000  |  
| 2       | 100        | 2009 | 12       | 5000  |  
| 7       | 200        | 2011 | 15       | 9000  |  

Product table:  

| product_id | product_name |  
|------------|--------------|  
| 100        | Nokia        |  
| 200        | Apple        |  
| 300        | Samsung      |  

**Output:**  

| product_name | year  | price |  
|--------------|-------|-------|  
| Nokia        | 2008  | 5000  |  
| Nokia        | 2009  | 5000  |  
| Apple        | 2011  | 9000  |  

**Explanation:**  
- From `sale_id = 1`, Nokia was sold for 5000 in the year 2008.  
- From `sale_id = 2`, Nokia was sold for 5000 in the year 2009.  
- From `sale_id = 7`, Apple was sold for 9000 in the year 2011.  

## Answer  
```sql
SELECT product_name,year, price
FROM Sales AS S
LEFT JOIN Product AS P
ON S.product_id = P.product_id;
```
-----------------------------
## [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/)  
## Tables: Visits, Transactions  

### Visits Table  

| Column Name | Type    |  
|-------------|---------|  
| visit_id    | int     |  
| customer_id | int     |  

- **visit_id** is the unique identifier for each visit.  
- This table contains information about customers who visited the mall.  

### Transactions Table  

| Column Name    | Type    |  
|----------------|---------|  
| transaction_id | int     |  
| visit_id       | int     |  
| amount         | int     |  

- **transaction_id** is the unique identifier for each transaction.  
- This table contains details of transactions made during a specific `visit_id`.  

## Problem Statement  

Write a solution to find the **IDs of customers who visited the mall without making any transactions** and the number of such visits (`count_no_trans`) for each customer.  

Return the result table sorted in any order.  

### Example 1:  

**Input:**  
Visits table:  

| visit_id | customer_id |  
|----------|-------------|  
| 1        | 23          |  
| 2        | 9           |  
| 4        | 30          |  
| 5        | 54          |  
| 6        | 96          |  
| 7        | 54          |  
| 8        | 54          |  

Transactions table:  

| transaction_id | visit_id | amount |  
|----------------|----------|--------|  
| 2              | 5        | 310    |  
| 3              | 5        | 300    |  
| 9              | 5        | 200    |  
| 12             | 1        | 910    |  
| 13             | 2        | 970    |  

**Output:**  

| customer_id | count_no_trans |  
|-------------|----------------|  
| 54          | 2              |  
| 30          | 1              |  
| 96          | 1              |  

**Explanation:**  
- Customer `23` visited once and made one transaction during the visit (`visit_id = 1`).  
- Customer `9` visited once and made one transaction during the visit (`visit_id = 2`).  
- Customer `30` visited once (`visit_id = 4`) without making any transactions.  
- Customer `54` visited three times. They made transactions during one visit (`visit_id = 5`) and no transactions during two visits (`visit_ids = 7, 8`).  
- Customer `96` visited once (`visit_id = 6`) without making any transactions.  

## Answer  
```sql
SELECT V.customer_id , COUNT(*) AS count_no_trans
FROM Visits AS V 
LEFT JOIN 
Transactions AS T
ON V. visit_id = T. visit_id 
WHERE 
transaction_id IS NULL
GROUP BY customer_id;
```

----------------------------------------
## [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/description/)  
## Table: Weather  

| Column Name   | Type    |  
|---------------|---------|  
| id            | int     |  
| recordDate    | date    |  
| temperature   | int     |  

- **id** is the unique identifier for each record.  
- **recordDate** is the date of the temperature recording.  
- **temperature** is the recorded temperature for that date.  

## Problem Statement  

Write a solution to find all dates' **id** with higher temperatures compared to the previous day's temperature.  

Return the result table in any order.  

### Example 1:  

**Input:**  
Weather table:  

| id  | recordDate  | temperature |  
|-----|-------------|-------------|  
| 1   | 2015-01-01  | 10          |  
| 2   | 2015-01-02  | 25          |  
| 3   | 2015-01-03  | 20          |  
| 4   | 2015-01-04  | 30          |  

**Output:**  

| id  |  
|-----|  
| 2   |  
| 4   |  

**Explanation:**  
- On **2015-01-02**, the temperature was higher than on the previous day (10 -> 25).  
- On **2015-01-04**, the temperature was higher than on the previous day (20 -> 30).  

## Answer  
```sql
SELECT W1.id 
FROM Weather AS W1
JOIN Weather AS W2
ON DATE(W1.recordDate) = DATE(W2.recordDate) + INTERVAL 1 DAY
WHERE W1.temperature > W2.temperature;

```
----------------------------------
## [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/description/)  
## Table: Activity  

| Column Name    | Type    |  
|----------------|---------|  
| machine_id     | int     |  
| process_id     | int     |  
| activity_type  | enum    |  
| timestamp      | float   |  

- **machine_id** is the ID of a machine.  
- **process_id** is the ID of a process running on the machine with ID `machine_id`.  
- **activity_type** is an enum of type ('start', 'end'), where 'start' indicates the process starts and 'end' indicates it ends.  
- **timestamp** is a float representing the time in seconds.  
  - 'start' timestamp will always be before the 'end' timestamp for every `(machine_id, process_id)` pair.  

## Problem Statement  

Write a solution to find the **average time** each machine takes to complete a process.  

The time to complete a process is calculated as the 'end' timestamp minus the 'start' timestamp. The **average time** is the total time to complete every process on the machine divided by the number of processes run on that machine.

The result should include `machine_id` along with the **average time** as `processing_time`, which should be rounded to 3 decimal places.

Return the result table in any order.  

### Example 1:  

**Input:**  
Activity table:  

| machine_id | process_id | activity_type | timestamp |  
|------------|------------|---------------|-----------|  
| 0          | 0          | start         | 0.712     |  
| 0          | 0          | end           | 1.520     |  
| 0          | 1          | start         | 3.140     |  
| 0          | 1          | end           | 4.120     |  
| 1          | 0          | start         | 0.550     |  
| 1          | 0          | end           | 1.550     |  
| 1          | 1          | start         | 0.430     |  
| 1          | 1          | end           | 1.420     |  
| 2          | 0          | start         | 4.100     |  
| 2          | 0          | end           | 4.512     |  
| 2          | 1          | start         | 2.500     |  
| 2          | 1          | end           | 5.000     |  

**Output:**  

| machine_id | processing_time |  
|------------|-----------------|  
| 0          | 0.894           |  
| 1          | 0.995           |  
| 2          | 1.456           |  

**Explanation:**  
- Machine 0's average time is ((1.520 - 0.712) + (4.120 - 3.140)) / 2 = 0.894  
- Machine 1's average time is ((1.550 - 0.550) + (1.420 - 0.430)) / 2 = 0.995  
- Machine 2's average time is ((4.512 - 4.100) + (5.000 - 2.500)) / 2 = 1.456  

## Answer  
```sql
SELECT machine_id, ROUND(AVG(end - start), 3) AS processing_time
FROM 
(SELECT machine_id, process_id, 
    MAX(CASE WHEN activity_type = 'start' THEN timestamp END) AS start,
    MAX(CASE WHEN activity_type = 'end' THEN timestamp END) AS end
 FROM Activity 
  GROUP BY machine_id, process_id) AS subq
GROUP BY machine_id
```
---------------------------------------

## [577. Employee Bonus](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50)
## Table: Employee

| Column Name | Type    |
|-------------|---------|
| empId       | int     |
| name        | varchar |
| supervisor  | int     |
| salary      | int     |

- **empId** is the column with unique values for this table.
- Each row of this table indicates the name and the ID of an employee in addition to their salary and the id of their manager.

## Table: Bonus

| Column Name | Type |
|-------------|------|
| empId       | int  |
| bonus       | int  |

- **empId** is the column of unique values for this table.
- **empId** is a foreign key (reference column) to **empId** from the Employee table.
- Each row of this table contains the id of an employee and their respective bonus.

## Problem Statement

Write a solution to report the name and bonus amount of each employee with a bonus less than 1000.

Return the result table in any order.

### Example 1:

**Input:**  
Employee table:

| empId | name   | supervisor | salary |
|-------|--------|------------|--------|
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |

Bonus table:

| empId | bonus |
|-------|-------|
| 2     | 500   |
| 4     | 2000  |

**Output:**  

| name | bonus |
|------|-------|
| Brad | null  |
| John | null  |
| Dan  | 500   |

**Explanation:**  
- Employee with `empId = 3` (Brad) does not have a bonus listed, so it's `null`.  
- Employee with `empId = 1` (John) does not have a bonus listed, so it's `null`.  
- Employee with `empId = 2` (Dan) has a bonus of 500, which is less than 1000.  

## Answer  
```sql
SELECT E.name ,  B.bonus 
FROM Employee AS E
LEFT JOIN Bonus AS B
ON E.empId = B.empId
WHERE bonus < 1000 OR bonus IS NULL
```
----------------------
## [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50)
## Table: Students

| Column Name   | Type    |
|---------------|---------|
| student_id    | int     |
| student_name  | varchar |

- **student_id** is the primary key (column with unique values) for this table.
- Each row of this table contains the ID and the name of one student in the school.

## Table: Subjects

| Column Name  | Type    |
|--------------|---------|
| subject_name | varchar |

- **subject_name** is the primary key (column with unique values) for this table.
- Each row of this table contains the name of one subject in the school.

## Table: Examinations

| Column Name  | Type    |
|--------------|---------|
| student_id   | int     |
| subject_name | varchar |

- There is no primary key (column with unique values) for this table. It may contain duplicates.
- Each student from the Students table takes every course from the Subjects table.
- Each row of this table indicates that a student with ID **student_id** attended the exam of **subject_name**.

## Problem Statement

Write a solution to find the number of times each student attended each exam.

Return the result table ordered by **student_id** and **subject_name**.

### Example 1:

**Input:**  
Students table:

| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |

Subjects table:

| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

Examinations table:

| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |

**Output:**  

| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

**Explanation:**  
- The result table should contain all students and all subjects.
- Alice attended the Math exam 3 times, the Physics exam 2 times, and the Programming exam 1 time.
- Bob attended the Math exam 1 time, the Programming exam 1 time, and did not attend the Physics exam.
- Alex did not attend any exams.
- John attended the Math exam 1 time, the Physics exam 1 time, and the Programming exam 1 time.

## Answer  
```sql
WITH student_subject_combinations AS (
    SELECT 
        s.student_id, 
        s.student_name, 
        subj.subject_name
    FROM 
        Students s
    CROSS JOIN 
        Subjects subj
)
SELECT 
    ss.student_id, 
    ss.student_name, 
    ss.subject_name, 
    COALESCE(COUNT(e.subject_name), 0) AS attended_exams
FROM 
    student_subject_combinations ss
LEFT JOIN 
    Examinations e
ON 
    ss.student_id = e.student_id AND 
    ss.subject_name = e.subject_name
GROUP BY 
    ss.student_id, ss.student_name, ss.subject_name
ORDER BY 
    ss.student_id, ss.subject_name;

```
------------------------------
## [570. Managers with At Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50)
## Table: Employee

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |

- **id** is the primary key (column with unique values) for this table.
- Each row of this table indicates the name of an employee, their department, and the id of their manager.
- If **managerId** is null, then the employee does not have a manager.
- No employee will be the manager of themself.

## Problem Statement

Write a solution to find managers with at least five direct reports.

Return the result table in any order.

### Example 1:

**Input:**  
Employee table:

| id  | name  | department | managerId |
|-----|-------|------------|-----------|
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |

**Output:**  

| name |
|------|
| John |

**Explanation:**  
- John is the manager of 5 employees: Dan, James, Amy, Anne, and Ron.
- Since he has at least 5 direct reports, he is included in the result.

## Answer  
```sql
SELECT a.name
FROM Employee a
JOIN Employee b
WHERE a.id = b.managerId
GROUP BY b.managerId
HAVING COUNT(*) >= 5
```
----------------------------------------------
## [1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50)
## Table: Signups

| Column Name    | Type     |
|----------------|----------|
| user_id        | int      |
| time_stamp     | datetime |
 
- **user_id** is the column of unique values for this table.
- Each row contains information about the signup time for the user with ID **user_id**.

## Table: Confirmations

| Column Name    | Type     |
|----------------|----------|
| user_id        | int      |
| time_stamp     | datetime |
| action         | ENUM     |

- (**user_id**, **time_stamp**) is the primary key (combination of columns with unique values) for this table.
- **user_id** is a foreign key (reference column) to **user_id** from the Signups table.
- **action** is an ENUM (category) of the type ('confirmed', 'timeout').
- Each row of this table indicates that the user with ID **user_id** requested a confirmation message at **time_stamp**, and that confirmation message was either confirmed ('confirmed') or expired without confirming ('timeout').

## Problem Statement

The confirmation rate of a user is the number of 'confirmed' messages divided by the total number of requested confirmation messages. The confirmation rate of a user who did not request any confirmation messages is 0. Round the confirmation rate to two decimal places.

Write a solution to find the confirmation rate of each user.

Return the result table in any order.

### Example 1:

**Input:**  
Signups table:

| user_id | time_stamp          |
|---------|---------------------|
| 3       | 2020-03-21 10:16:13 |
| 7       | 2020-01-04 13:57:59 |
| 2       | 2020-07-29 23:09:44 |
| 6       | 2020-12-09 10:39:37 |

Confirmations table:

| user_id | time_stamp          | action    |
|---------|---------------------|-----------|
| 3       | 2021-01-06 03:30:46 | timeout   |
| 3       | 2021-07-14 14:00:00 | timeout   |
| 7       | 2021-06-12 11:57:29 | confirmed |
| 7       | 2021-06-13 12:58:28 | confirmed |
| 7       | 2021-06-14 13:59:27 | confirmed |
| 2       | 2021-01-22 00:00:00 | confirmed |
| 2       | 2021-02-28 23:59:59 | timeout   |

**Output:**  

| user_id | confirmation_rate |
|---------|-------------------|
| 6       | 0.00              |
| 3       | 0.00              |
| 7       | 1.00              |
| 2       | 0.50              |

**Explanation:**  
- User 6 did not request any confirmation messages. The confirmation rate is 0.  
- User 3 made 2 requests and both timed out. The confirmation rate is 0.  
- User 7 made 3 requests and all were confirmed. The confirmation rate is 1.  
- User 2 made 2 requests where one was confirmed and the other timed out. The confirmation rate is 1 / 2 = 0.5.

## Answer  
```sql
SELECT 
  s.user_id, 
  ROUND(
    COALESCE(
      SUM(
        CASE WHEN ACTION = 'confirmed' THEN 1 END
      ) / COUNT(*), 0),2) 
  AS confirmation_rate 
FROM Signups s 
LEFT JOIN Confirmations c 
ON s.user_id = c.user_id 
GROUP BY s.user_id;  
```
----------------------------
# Basic Aggregate Functions
## [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50)  
## Table: Cinema  

| Column Name | Type    |  
|-------------|---------|  
| id          | int     |  
| movie       | varchar |  
| description | varchar |  
| rating      | float   |  

- **id** is the primary key for this table.  
- Each row contains information about the name of a movie, its genre, and its rating.  
- **rating** is a 2 decimal places float in the range [0, 10].  

## Problem Statement  

Write a solution to report the movies with an odd-numbered **id** and a **description** that is not "boring".  

Return the result table ordered by **rating** in descending order.  

### Example 1:  

**Input:**  
Cinema table:  

| id | movie      | description | rating |  
|----|------------|-------------|--------|  
| 1  | War        | great 3D    | 8.9    |  
| 2  | Science    | fiction     | 8.5    |  
| 3  | irish      | boring      | 6.2    |  
| 4  | Ice song   | Fantacy     | 8.6    |  
| 5  | House card | Interesting | 9.1    |  

**Output:**  

| id | movie      | description | rating |  
|----|------------|-------------|--------|  
| 5  | House card | Interesting | 9.1    |  
| 1  | War        | great 3D    | 8.9    |  

**Explanation:**  
- We have three movies with odd-numbered IDs: 1, 3, and 5.  
- The movie with **id = 3** is "boring," so it is excluded.  
- The result is sorted by **rating** in descending order.  

## Answer  
```sql
 SELECT * FROM Cinema
WHERE (id %2) != 0 
AND
description != 'boring'
ORDER BY rating DESC
```
------------------------------------------
## [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50)  
## Table: Prices  

| Column Name  | Type |  
|--------------|------|  
| product_id   | int  |  
| start_date   | date |  
| end_date     | date |  
| price        | int  |  

- **(product_id, start_date, end_date)** is the primary key for this table.  
- Each row indicates the price of the product_id during the period from **start_date** to **end_date**.  
- There are no overlapping periods for the same product_id.  

## Table: UnitsSold  

| Column Name   | Type |  
|---------------|------|  
| product_id    | int  |  
| purchase_date | date |  
| units         | int  |  

- This table may contain duplicate rows.  
- Each row indicates the date, units, and product_id of each product sold.  

## Problem Statement  

Write a solution to find the **average selling price** for each product.  

- The **average_price** should be rounded to 2 decimal places.  
- If a product does not have any sold units, its average selling price is assumed to be **0**.  

Return the result table in any order.  

### Example 1:  

**Input:**  

**Prices table:**  

| product_id | start_date | end_date   | price |  
|------------|------------|------------|-------|  
| 1          | 2019-02-17 | 2019-02-28 | 5     |  
| 1          | 2019-03-01 | 2019-03-22 | 20    |  
| 2          | 2019-02-01 | 2019-02-20 | 15    |  
| 2          | 2019-02-21 | 2019-03-31 | 30    |  

**UnitsSold table:**  

| product_id | purchase_date | units |  
|------------|---------------|-------|  
| 1          | 2019-02-25    | 100   |  
| 1          | 2019-03-01    | 15    |  
| 2          | 2019-02-10    | 200   |  
| 2          | 2019-03-22    | 30    |  

**Output:**  

| product_id | average_price |  
|------------|---------------|  
| 1          | 6.96          |  
| 2          | 16.96         |  

**Explanation:**  

- Average selling price = Total Price of Product / Number of products sold.  
- For product 1: ((100 \* 5) + (15 \* 20)) / 115 = 6.96.  
- For product 2: ((200 \* 15) + (30 \* 30)) / 230 = 16.96.  

## Answer  
```sql
SELECT 
    P.product_id, 
    ROUND(COALESCE(SUM(P.price * U.units) / NULLIF(SUM(U.units), 0), 0), 2) AS average_price
FROM 
    Prices AS P
LEFT JOIN 
    UnitsSold AS U
ON 
    P.product_id = U.product_id
    AND U.purchase_date BETWEEN P.start_date AND P.end_date
GROUP BY 
    P.product_id;

```
----------------------------------------------
## [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50)  
## Table: Project  

| Column Name | Type |  
|-------------|------|  
| project_id  | int  |  
| employee_id | int  |  

- **(project_id, employee_id)** is the primary key of this table.  
- **employee_id** is a foreign key referencing the Employee table.  
- Each row indicates that the employee with **employee_id** is working on the project with **project_id**.  

## Table: Employee  

| Column Name      | Type    |  
|------------------|---------|  
| employee_id      | int     |  
| name             | varchar |  
| experience_years | int     |  

- **employee_id** is the primary key of this table.  
- **experience_years** is guaranteed not to be NULL.  
- Each row contains information about an employee.  

## Problem Statement  

Write an SQL query to report the **average experience years** of all the employees for each project, rounded to 2 decimal places.  

Return the result table in any order.  

### Example 1:  

**Input:**  

**Project table:**  

| project_id | employee_id |  
|------------|-------------|  
| 1          | 1           |  
| 1          | 2           |  
| 1          | 3           |  
| 2          | 1           |  
| 2          | 4           |  

**Employee table:**  

| employee_id | name   | experience_years |  
|-------------|--------|------------------|  
| 1           | Khaled | 3                |  
| 2           | Ali    | 2                |  
| 3           | John   | 1                |  
| 4           | Doe    | 2                |  

**Output:**  

| project_id | average_years |  
|------------|---------------|  
| 1          | 2.00          |  
| 2          | 2.50          |  

**Explanation:**  

- For **project 1**, the average experience years are \((3 + 2 + 1) / 3 = 2.00\).  
- For **project 2**, the average experience years are \((3 + 2) / 2 = 2.50\).  

## Answer  
```sql
SELECT P.project_id , 
ROUND(AVG(E.experience_years),2) AS average_years
FROM Project AS P
LEFT JOIN Employee AS E
ON P.employee_id = E.employee_id
GROUP BY P.project_id
```
------------------------------------
## [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50)  
## Table: Users  

| Column Name | Type    |  
|-------------|---------|  
| user_id     | int     |  
| user_name   | varchar |  

- **user_id** is the primary key for this table.  
- Each row contains the name and the ID of a user.  

## Table: Register  

| Column Name | Type |  
|-------------|------|  
| contest_id  | int  |  
| user_id     | int  |  

- **(contest_id, user_id)** is the primary key for this table.  
- Each row contains the ID of a user and the contest they registered for.  

## Problem Statement  

Write an SQL query to find the **percentage of users registered** in each contest, rounded to two decimal places.  

Return the result table:  
- Ordered by **percentage** in descending order.  
- In case of a tie, order by **contest_id** in ascending order.  

### Example 1:  

**Input:**  

**Users table:**  

| user_id | user_name |  
|---------|-----------|  
| 6       | Alice     |  
| 2       | Bob       |  
| 7       | Alex      |  

**Register table:**  

| contest_id | user_id |  
|------------|---------|  
| 215        | 6       |  
| 209        | 2       |  
| 208        | 2       |  
| 210        | 6       |  
| 208        | 6       |  
| 209        | 7       |  
| 209        | 6       |  
| 215        | 7       |  
| 208        | 7       |  
| 210        | 2       |  
| 207        | 2       |  
| 210        | 7       |  

**Output:**  

| contest_id | percentage |  
|------------|------------|  
| 208        | 100.0      |  
| 209        | 100.0      |  
| 210        | 100.0      |  
| 215        | 66.67      |  
| 207        | 33.33      |  

**Explanation:**  
- All users registered in contests **208**, **209**, and **210**, making their percentage **100%**.  
- Contests **208**, **209**, and **210** are sorted by **contest_id** in ascending order.  
- Contests **215** had **2 out of 3 users**, so the percentage is \((2/3) \times 100 = 66.67\).  
- Contest **207** had only **1 user** registered, so the percentage is \((1/3) \times 100 = 33.33\).  

## Answer  
```sql
SELECT R.contest_id,
ROUND((COUNT(R.user_id)/(SELECT COUNT(user_id) FROM Users ))*100,2) AS percentage
FROM Register AS R 
GROUP BY R.contest_id
ORDER BY percentage DESC, R.contest_id ASC;
```
-----------------------------------
## [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/)  
### Table: Queries  

| Column Name | Type    |  
|-------------|---------|  
| query_name  | varchar |  
| result      | varchar |  
| position    | int     |  
| rating      | int     |  

- Duplicate rows may exist in the table.  
- **position** values are integers from 1 to 500.  
- **rating** values are integers from 1 to 5.  
- A query is considered **poor** if its rating is less than 3.  

### Problem Statement  

Write an SQL query to calculate the following for each `query_name`:  
1. **Quality**: The average ratio of `rating / position`.  
2. **Poor Query Percentage**: The percentage of queries with a `rating < 3`.  

Both `quality` and `poor_query_percentage` should be **rounded to 2 decimal places**.  

Return the results table in any order.  

### Example  

#### Input:  
**Queries table:**  

| query_name | result            | position | rating |  
|------------|-------------------|----------|--------|  
| Dog        | Golden Retriever  | 1        | 5      |  
| Dog        | German Shepherd   | 2        | 5      |  
| Dog        | Mule              | 200      | 1      |  
| Cat        | Shirazi           | 5        | 2      |  
| Cat        | Siamese           | 3        | 3      |  
| Cat        | Sphynx            | 7        | 4      |  

#### Output:  
| query_name | quality | poor_query_percentage |  
|------------|---------|-----------------------|  
| Dog        | 2.50    | 33.33                 |  
| Cat        | 0.66    | 33.33                 |  

#### Explanation:  
- **Dog**:  
  - Quality: \(((5 / 1) + (5 / 2) + (1 / 200)) / 3 = 2.50\)  
  - Poor Query Percentage: \((1 / 3) \times 100 = 33.33\)%  
- **Cat**:  
  - Quality: \(((2 / 5) + (3 / 3) + (4 / 7)) / 3 = 0.66\)  
  - Poor Query Percentage: \((1 / 3) \times 100 = 33.33\)%  

## Answer  
```sql
SELECT query_name,
       ROUND(AVG(rating / position), 2) AS quality,
       ROUND((SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) / COUNT(rating))*100, 2) AS poor_query_percentage
FROM Queries
WHERE query_name IS NOT NULL
GROUP BY query_name;
```  
-----------------------------------------
## [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/description/)
## Table: Transactions

| Column Name   | Type    |
|---------------|---------|
| id            | int     |
| country       | varchar |
| state         | enum    |
| amount        | int     |
| trans_date    | date    |

- **id** is the primary key of this table.  
- The table contains information about incoming transactions.  
- The `state` column is an enum of type ["approved", "declined"].  

## Problem Statement

Write an SQL query to find for each month and country:  
1. The total number of transactions.  
2. The total number of approved transactions.  
3. The total amount of all transactions.  
4. The total amount of approved transactions.  

Return the result table in any order.  

### Example 1:

**Input:**  
Transactions table:

| id   | country | state    | amount | trans_date |
|------|---------|----------|--------|------------|
| 121  | US      | approved | 1000   | 2018-12-18 |
| 122  | US      | declined | 2000   | 2018-12-19 |
| 123  | US      | approved | 2000   | 2019-01-01 |
| 124  | DE      | approved | 2000   | 2019-01-07 |

**Output:**  

| month    | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
|----------|---------|-------------|----------------|--------------------|-----------------------|
| 2018-12  | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01  | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01  | DE      | 1           | 1              | 2000               | 2000                  |

**Explanation:**  
- In December 2018, the US had 2 transactions totaling 3000, of which 1 was approved, totaling 1000.  
- In January 2019, the US had 1 approved transaction totaling 2000.  
- In January 2019, Germany (DE) had 1 approved transaction totaling 2000.  

## Answer
```sql
SELECT 
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(*) AS trans_count,
    SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM 
    Transactions
GROUP BY 
    DATE_FORMAT(trans_date, '%Y-%m'), country;
```
-----------------------------------------
## [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/description/)
## Table: Delivery

| Column Name                 | Type    |
|-----------------------------|---------|
| delivery_id                 | int     |
| customer_id                 | int     |
| order_date                  | date    |
| customer_pref_delivery_date | date    |

- **delivery_id** is the column of unique values in this table.  
- The table contains information about food delivery orders.  
- An order is considered **immediate** if the `customer_pref_delivery_date` is the same as the `order_date`; otherwise, it is considered **scheduled**.  
- The **first order** of a customer is the one with the earliest `order_date`.  
- It is guaranteed that each customer has exactly one first order.

## Problem Statement

Write an SQL query to calculate the percentage of **immediate orders** among the first orders of all customers. The result should be rounded to 2 decimal places.

### Example 1:

**Input:**  
Delivery table:

| delivery_id | customer_id | order_date | customer_pref_delivery_date |
|-------------|-------------|------------|-----------------------------|
| 1           | 1           | 2019-08-01 | 2019-08-02                  |
| 2           | 2           | 2019-08-02 | 2019-08-02                  |
| 3           | 1           | 2019-08-11 | 2019-08-12                  |
| 4           | 3           | 2019-08-24 | 2019-08-24                  |
| 5           | 3           | 2019-08-21 | 2019-08-22                  |
| 6           | 2           | 2019-08-11 | 2019-08-13                  |
| 7           | 4           | 2019-08-09 | 2019-08-09                  |

**Output:**  

| immediate_percentage |
|-----------------------|
| 50.00                |

**Explanation:**  
- Customer **1**: First order (`delivery_id = 1`) is scheduled.  
- Customer **2**: First order (`delivery_id = 2`) is immediate.  
- Customer **3**: First order (`delivery_id = 5`) is scheduled.  
- Customer **4**: First order (`delivery_id = 7`) is immediate.  

Out of 4 customers, 2 have immediate first orders. The percentage is \( \frac{2}{4} \times 100 = 50.00 \).  

## Answer
```sql
 WITH FirstOrders AS (
    SELECT 
        customer_id,
        delivery_id,
        order_date,
        customer_pref_delivery_date,
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date) AS rn
    FROM Delivery
)
SELECT 
    ROUND(
        SUM(CASE WHEN order_date = customer_pref_delivery_date THEN 1 ELSE 0 END) 
        / COUNT(*) * 100, 2
    ) AS immediate_percentage
FROM FirstOrders
WHERE rn = 1;

```
---------------------------------------------
## [550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/description/)
## Table: Activity

| Column Name  | Type    |
|--------------|---------|
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |

- **(player_id, event_date)** is the primary key for this table.  
- Each row represents a player's activity on a specific date, including the device used and the number of games played.

## Problem Statement

Write an SQL query to calculate the fraction of players who logged in again on the day immediately following their first login date.  
- Count the number of players with at least two consecutive login days starting from their first login date.  
- Divide that count by the total number of players.  

Return the result rounded to **2 decimal places**.

### Example 1:

**Input:**  
Activity table:

| player_id | device_id | event_date | games_played |
|-----------|-----------|------------|--------------|
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |

**Output:**  

| fraction |
|----------|
| 0.33     |

**Explanation:**  
- Player **1**: First login on `2016-03-01`. Logged in again on `2016-03-02`.  
- Player **2**: First login on `2017-06-25`. No login on `2017-06-26`.  
- Player **3**: First login on `2016-03-02`. No login on `2016-03-03`.  

Only **1 out of 3 players** logged in consecutively after their first day. The fraction is \( \frac{1}{3} = 0.33 \).

## Answer
```sql
WITH FirstLogin AS (
    -- Find the first login date for each player
    SELECT player_id, MIN(event_date) AS first_login
    FROM Activity
    GROUP BY player_id
),
NextLogin AS (
    -- Find the players who logged in on the next day after their first login
    SELECT A.player_id
    FROM Activity A
    JOIN FirstLogin F ON A.player_id = F.player_id
    WHERE A.event_date = DATE_ADD(F.first_login, INTERVAL 1 DAY)
)
-- Calculate the fraction of players who logged in again the next day
SELECT ROUND(COUNT(DISTINCT N.player_id) / COUNT(DISTINCT A.player_id), 2) AS fraction
FROM Activity A
LEFT JOIN NextLogin N ON A.player_id = N.player_id;

```
---------------------------------------------
# Sorting and Grouping
## [2356 - Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher)

## Table: Teacher

| Column Name | Type    |
|-------------|---------|
| teacher_id  | int     |
| subject_id  | int     |
| dept_id     | int     |

- `(subject_id, dept_id)` is the primary key of this table.
- Each row in this table indicates that the teacher with `teacher_id` teaches the subject `subject_id` in the department `dept_id`.

## Problem Statement

Write a solution to calculate the number of **unique subjects** each teacher teaches in the university.

Return the result table in any order.

The result format is shown in the following example:

### Example 1:

**Input:**  
Teacher table:  

| teacher_id | subject_id | dept_id |
|------------|------------|---------|
| 1          | 2          | 3       |
| 1          | 2          | 4       |
| 1          | 3          | 3       |
| 2          | 1          | 1       |
| 2          | 2          | 1       |
| 2          | 3          | 1       |
| 2          | 4          | 1       |

**Output:**  

| teacher_id | cnt |
|------------|-----|
| 1          | 2   |
| 2          | 4   |

**Explanation:**  
- Teacher `1`:  
  - They teach subject `2` in departments `3` and `4` (unique subject: `2`).  
  - They teach subject `3` in department `3` (unique subject: `3`).  
  - Total unique subjects: `2`.  
- Teacher `2`:  
  - They teach subject `1`, `2`, `3`, and `4` in department `1`.  
  - Total unique subjects: `4`.

## ANSWER
```sql
# Write your MySQL query statement below
select teacher_id , 
count(distinct subject_id ) as cnt
from Teacher
group by teacher_id
```
-----------------------------------------------
## [1141 - User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i)

## Table: Activity

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| session_id    | int     |
| activity_date | date    |
| activity_type | enum    |

- The `activity_type` column is an ENUM of type `('open_session', 'end_session', 'scroll_down', 'send_message')`.
- The table may have duplicate rows.
- Each session belongs to exactly one user.
- The table shows user activities for a social media website.

## Problem Statement

Write a solution to find the **daily active user count** for a period of **30 days** ending on `2019-07-27` inclusively.  
A user was considered active on a specific day if they made **at least one activity** on that day.

Return the result table in any order.

The result format is shown in the following example:

### Example 1:

**Input:**  
Activity table:  

| user_id | session_id | activity_date | activity_type |
|---------|------------|---------------|---------------|
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          | 2019-07-20    | scroll_down   |
| 1       | 1          | 2019-07-20    | end_session   |
| 2       | 4          | 2019-07-20    | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          | 2019-07-21    | end_session   |
| 3       | 2          | 2019-07-21    | open_session  |
| 3       | 2          | 2019-07-21    | send_message  |
| 3       | 2          | 2019-07-21    | end_session   |
| 4       | 3          | 2019-06-25    | open_session  |
| 4       | 3          | 2019-06-25    | end_session   |

**Output:**  

| day        | active_users |
|------------|--------------|
| 2019-07-20 | 2            |
| 2019-07-21 | 2            |

**Explanation:**  
- On `2019-07-20`, users `1` and `2` were active.
- On `2019-07-21`, users `2` and `3` were active.
- Days outside the period of the last 30 days ending on `2019-07-27` are excluded.

## ANSWER
```sql
SELECT activity_date AS day ,COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date BETWEEN DATE_SUB('2019-07-27', INTERVAL 29 DAY) AND '2019-07-27'
GROUP BY activity_date
```
------------------------------------
## [1070 - Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii)

## Table: Sales

| Column Name | Type  |
|-------------|-------|
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |

- `(sale_id, year)` is the primary key of this table.
- `product_id` is a foreign key referencing the `Product` table.
- Each row in this table shows a sale of `product_id` in a specific `year`.
- `price` represents the price per unit.

## Table: Product

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

- `product_id` is the primary key of this table.
- Each row in this table indicates the product name for each product.

## Problem Statement

Write a solution to select the `product_id`, the first year of sale (`first_year`), `quantity`, and `price` for the **first year** of every product sold.

Return the result table in any order.

### Example 1:

**Input:**  

**Sales table:**  

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

**Product table:**  

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

**Output:**  

| product_id | first_year | quantity | price |
|------------|------------|----------|-------|
| 100        | 2008       | 10       | 5000  |
| 200        | 2011       | 15       | 9000  |

**Explanation:**  
- Product `100` was first sold in the year `2008` with a quantity of `10` and a price of `5000`.
- Product `200` was first sold in the year `2011` with a quantity of `15` and a price of `9000`.

## ANSWER
```sql
SELECT s.product_id, s.year AS first_year, s.quantity, s.price
FROM Sales s
JOIN (
  SELECT product_id, MIN(year) AS year 
  FROM sales 
  GROUP BY product_id
  ) p
ON s.product_id = p.product_id
AND s.year = p.year
```
---------------------------------
## [596 - Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students)

## Table: Courses

| Column Name | Type    |
|-------------|---------|
| student     | varchar |
| class       | varchar |

- `(student, class)` is the primary key of this table.
- Each row indicates the name of a student and the class they are enrolled in.

## Problem Statement

Write a solution to find all the classes that have **at least five students**.

Return the result table in any order.

### Example 1:

**Input:**  

**Courses table:**  

| student | class    |
|---------|----------|
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |

**Output:**  

| class   |
|---------|
| Math    |

**Explanation:**  
- `Math` has 6 students, so it is included in the output.
- `English`, `Biology`, and `Computer` each have only 1 student, so they are excluded.

## ANSWER
```sql
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(student) > 4;
```
--------------------------------------------------------
## [1729 - Find Followers Count](https://leetcode.com/problems/find-followers-count)

## Table: Followers

| Column Name | Type |
|-------------|------|
| user_id     | int  |
| follower_id | int  |

- `(user_id, follower_id)` is the primary key of this table.
- Each row in this table indicates that `follower_id` follows `user_id` on a social media platform.

## Problem Statement

Write a solution to calculate the number of followers for each user.

- Return the result table ordered by `user_id` in ascending order.

### Example 1:

**Input:**  

**Followers table:**  

| user_id | follower_id |
|---------|-------------|
| 0       | 1           |
| 1       | 0           |
| 2       | 0           |
| 2       | 1           |

**Output:**  

| user_id | followers_count |
|---------|-----------------|
| 0       | 1               |
| 1       | 1               |
| 2       | 2               |

**Explanation:**  
- User `0` has `1` follower (`1`).
- User `1` has `1` follower (`0`).
- User `2` has `2` followers (`0, 1`).

## ANSWER
```sql
# Write your MySQL query statement below
SELECT user_id, COUNT( follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id
```
-------------------------------
## [619 - Biggest Single Number](https://leetcode.com/problems/biggest-single-number)

## Table: MyNumbers

| Column Name | Type |
|-------------|------|
| num         | int  |

- This table may contain duplicates, meaning there is no primary key.
- Each row contains an integer.

## Problem Statement

A **single number** is defined as a number that appears **only once** in the `MyNumbers` table.

Write a solution to find the largest single number in the table. If there is no single number, return `null`.

### Example 1:

**Input:**  

**MyNumbers table:**  

| num |
|-----|
| 8   |
| 8   |
| 3   |
| 3   |
| 1   |
| 4   |
| 5   |
| 6   |

**Output:**  

| num |
|-----|
| 6   |

**Explanation:**  
The single numbers are `1`, `4`, `5`, and `6`.  
Since `6` is the largest single number, it is returned.

---

### Example 2:

**Input:**  

**MyNumbers table:**  

| num |
|-----|
| 8   |
| 8   |
| 7   |
| 7   |
| 3   |
| 3   |
| 3   |

**Output:**  

| num  |
|------|
| null |

**Explanation:**  
There are no single numbers in the input table, so `null` is returned.

## ANSWER
```sql
SELECT COALESCE(
  (SELECT num
  FROM MyNumbers
  GROUP BY num
  HAVING COUNT(num) = 1
  ORDER BY num DESC
  LIMIT 1), null) 
  AS num
```
------------------------------------------
## [1045 - Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products)

## Table: Customer

| Column Name | Type    |
|-------------|---------|
| customer_id | int     |
| product_key | int     |

This table may contain duplicate rows.  
`customer_id` is not NULL.  
`product_key` is a foreign key (reference column) to the `Product` table.

---

## Table: Product

| Column Name | Type    |
|-------------|---------|
| product_key | int     |

`product_key` is the primary key for this table.

---

## Problem Statement

Write a solution to report the `customer_id` values from the `Customer` table that bought **all** the products in the `Product` table.

Return the result table in any order.

---

### Example 1:

**Input:**  
**Customer Table:**

| customer_id | product_key |
|-------------|-------------|
| 1           | 5           |
| 2           | 6           |
| 3           | 5           |
| 3           | 6           |
| 1           | 6           |

**Product Table:**

| product_key |
|-------------|
| 5           |
| 6           |

---

**Output:**  

| customer_id |
|-------------|
| 1           |
| 3           |

---

**Explanation:**  
The customers who bought all the products (5 and 6) are customers with IDs 1 and 3.  

---

## ANSWER  
```sql
select customer_id 
from Customer  
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (
  SELECT COUNT(product_key)
  FROM Product
)
```
----------------------
