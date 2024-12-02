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
