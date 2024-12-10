![App Screenshot](https://github.com/AkashRouth001/SQL-50-LeetCode-problem/blob/4b444cdf7361033434c07faa1f9e45c8cc12883b/500.png)
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

## Table: Product

| Column Name | Type    |
|-------------|---------|
| product_key | int     |

`product_key` is the primary key for this table.

## Problem Statement

Write a solution to report the `customer_id` values from the `Customer` table that bought **all** the products in the `Product` table.

Return the result table in any order.

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

**Output:**  

| customer_id |
|-------------|
| 1           |
| 3           |


**Explanation:**  
The customers who bought all the products (5 and 6) are customers with IDs 1 and 3.  


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
# Advanced Select and Joins
## [1731 - The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee)

## Table: Employees

| Column Name  | Type    |
|--------------|---------|
| employee_id  | int     |
| name         | varchar |
| reports_to   | int     |
| age          | int     |

- `employee_id` is the column with unique values for this table.  
- This table contains information about the employees and the ID of the manager they report to.  
- Some employees do not report to anyone (`reports_to` is null).

## Problem Statement

We will consider a manager as an employee who has at least one other employee reporting to them.

Write a solution to report the:
- IDs (`employee_id`) and names of all managers,
- The number of employees who report directly to them (`reports_count`),
- The average age of their reports (`average_age`, rounded to the nearest integer).

Return the result table ordered by `employee_id`.

### Example 1:

**Input:**  
**Employees Table:**  

| employee_id | name    | reports_to | age |
|-------------|---------|------------|-----|
| 9           | Hercy   | null       | 43  |
| 6           | Alice   | 9          | 41  |
| 4           | Bob     | 9          | 36  |
| 2           | Winston | null       | 37  |

**Output:**  

| employee_id | name  | reports_count | average_age |
|-------------|-------|---------------|-------------|
| 9           | Hercy | 2             | 39          |

**Explanation:**  
- Hercy has 2 employees reporting to him: Alice and Bob.  
- Their average age is `(41 + 36) / 2 = 38.5`, which is rounded to `39`.

### Example 2:

**Input:**  
**Employees Table:**  

| employee_id | name    | reports_to | age |
|-------------|---------|------------|-----|
| 1           | Michael | null       | 45  |
| 2           | Alice   | 1          | 38  |
| 3           | Bob     | 1          | 42  |
| 4           | Charlie | 2          | 34  |
| 5           | David   | 2          | 40  |
| 6           | Eve     | 3          | 37  |
| 7           | Frank   | null       | 50  |
| 8           | Grace   | null       | 48  |

**Output:**  

| employee_id | name    | reports_count | average_age |
|-------------|---------|---------------|-------------|
| 1           | Michael | 2             | 40          |
| 2           | Alice   | 2             | 37          |
| 3           | Bob     | 1             | 37          |

**Explanation:**  
- Michael has 2 employees reporting to him: Alice and Bob. Average age: `(38 + 42) / 2 = 40`.  
- Alice has 2 employees reporting to her: Charlie and David. Average age: `(34 + 40) / 2 = 37`.  
- Bob has 1 employee reporting to him: Eve. Average age: `37`.


## ANSWER  

```sql
SELECT e1.employee_id, e1.name, COUNT(e2.employee_id) reports_count, ROUND(AVG(e2.age)) average_age 
FROM Employees e1, Employees e2
WHERE e1.employee_id = e2.reports_to
GROUP BY e1.employee_id
HAVING reports_count > 0
ORDER BY e1.employee_id
```
----------------------------
## [1789 - Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee)

## Table: Employee

| Column Name   | Type    |
|---------------|---------|
| employee_id   | int     |
| department_id | int     |
| primary_flag  | varchar |

- `(employee_id, department_id)` is the primary key (combination of columns with unique values).  
- `employee_id` is the ID of the employee.  
- `department_id` is the ID of the department the employee belongs to.  
- `primary_flag` is an ENUM of type ('Y', 'N'):  
  - `'Y'`: The department is the primary department for the employee.  
  - `'N'`: The department is not the primary.  

## Problem Statement

Employees can belong to multiple departments. When they join other departments, they decide on a primary department.  
- If an employee belongs to only one department, their `primary_flag` is `'N'`.

Write a solution to report all employees with their primary department.  
- For employees with only one department, report their only department.


### Example 1:

**Input:**  
**Employee Table:**  

| employee_id | department_id | primary_flag |
|-------------|---------------|--------------|
| 1           | 1             | N            |
| 2           | 1             | Y            |
| 2           | 2             | N            |
| 3           | 3             | N            |
| 4           | 2             | N            |
| 4           | 3             | Y            |
| 4           | 4             | N            |

**Output:**  

| employee_id | department_id |
|-------------|---------------|
| 1           | 1             |
| 2           | 1             |
| 3           | 3             |
| 4           | 3             |

**Explanation:**  
- Employee 1 belongs to one department (1), so it is their primary department.  
- Employee 2 has department 1 as their primary department.  
- Employee 3 belongs to only one department (3), so it is their primary department.  
- Employee 4 has department 3 as their primary department.


## ANSWER  

```sql
SELECT employee_id, department_id
FROM Employee 
WHERE primary_flag = 'Y'
UNION
SELECT employee_id, department_id
FROM Employee
GROUP BY employee_id
HAVING COUNT(employee_id)=1
```
-----------------------
## [610 - Triangle Judgement](https://leetcode.com/problems/triangle-judgement)

## Table: Triangle

| Column Name | Type |
|-------------|------|
| x           | int  |
| y           | int  |
| z           | int  |

- `(x, y, z)` is the primary key column for this table.  
- Each row represents the lengths of three line segments.

## Problem Statement

Determine if the three line segments `(x, y, z)` can form a triangle.  
For three segments to form a triangle, they must satisfy the triangle inequality conditions:  
1. \( x + y > z \)  
2. \( x + z > y \)  
3. \( y + z > x \)  

Write a query to return the result for each row with an additional column **triangle**, which should contain `'Yes'` if the segments can form a triangle and `'No'` otherwise.

### Example 1:

**Input:**  
**Triangle Table:**  

| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |

**Output:**  

| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |

**Explanation:**  
- For the first row, \( 13 + 15 \leq 30 \), so it cannot form a triangle.  
- For the second row, all the triangle inequality conditions are satisfied, so it can form a triangle.


## ANSWER  

```sql
SELECT x, y, z, 
CASE WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
ELSE 'No' END AS triangle
FROM Triangle
```
----------------------------
## [180 - Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers)

## Table: Logs

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| num         | varchar |

- `id` is the primary key column for this table.  
- The `id` column is an autoincrement column starting from 1.  


## Problem Statement

Find all numbers in the `Logs` table that appear at least **three times consecutively**.  
Return the result as a table with one column: **ConsecutiveNums**.


### Example 1:

**Input:**  
**Logs Table:**  

| id | num |
|----|-----|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |

**Output:**  

| ConsecutiveNums |
|-----------------|
| 1               |

**Explanation:**  
- The number `1` appears consecutively for at least 3 times (at `id = 1, 2, 3`).  
- No other numbers satisfy this condition.


## ANSWER  

```sql
WITH cte AS (
  SELECT id, num, 
    LEAD(num) OVER (ORDER BY id) AS next, 
    LAG(num) OVER (ORDER BY id) AS prev
  FROM Logs
) 
SELECT DISTINCT(num) AS ConsecutiveNums
FROM cte
WHERE num = next AND num = prev
```
------------------
## [1164 - Product Price at a Given Date](https://leetcode.com/problems/product-price-at-a-given-date)

## Table: Products

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| new_price     | int     |
| change_date   | date    |

- `(product_id, change_date)` is the **primary key** for this table.  
- Each row indicates that the price of a product was changed to a new value on a specific date.  


## Problem Statement

Find the prices of all products on **2019-08-16**.  
- Assume that the price of all products is **10** before any changes are recorded.


### Example 1:

**Input:**  
**Products Table:**  

| product_id | new_price | change_date |
|------------|-----------|-------------|
| 1          | 20        | 2019-08-14  |
| 2          | 50        | 2019-08-14  |
| 1          | 30        | 2019-08-15  |
| 1          | 35        | 2019-08-16  |
| 2          | 65        | 2019-08-17  |
| 3          | 20        | 2019-08-18  |

**Output:**  

| product_id | price |
|------------|-------|
| 2          | 50    |
| 1          | 35    |
| 3          | 10    |

**Explanation:**  
- For **product_id = 1**, the price on **2019-08-16** is 35.  
- For **product_id = 2**, the price on **2019-08-16** is 50.  
- For **product_id = 3**, there is no change recorded before **2019-08-16**, so the price is 10 (default value).


## ANSWER  

```sql
SELECT product_id, new_price AS price
FROM products
WHERE (product_id, change_date) IN
(   
    SELECT product_id, MAX(change_date)
    FROM products
    WHERE change_date <= '2019-08-16'
    GROUP BY product_id
)
UNION

SELECT product_id, 10 AS price
FROM products
WHERE product_id NOT IN
(
    SELECT product_id
    FROM products
    WHERE change_date <= '2019-08-16'
);

```
-----------------
## [1204 - Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus)

## Table: Queue

| Column Name | Type    |
|-------------|---------|
| person_id   | int     |
| person_name | varchar |
| weight      | int     |
| turn        | int     |

- `person_id` contains **unique values**.  
- `(person_id, turn)` contains all numbers from 1 to `n`, where `n` is the number of rows.  
- `turn` determines the order in which people board the bus.  


## Problem Statement

Given a **weight limit of 1000 kg**, find the **person_name** of the **last person** who can board the bus without exceeding the limit.  
- The test cases guarantee that the first person in line does not exceed the weight limit.  
- Only one person can board the bus at a time, and the boarding happens in the order of `turn`.


### Example 1:

**Input:**  
**Queue Table:**  

| person_id | person_name | weight | turn |
|-----------|-------------|--------|------|
| 5         | Alice       | 250    | 1    |
| 4         | Bob         | 175    | 5    |
| 3         | Alex        | 350    | 2    |
| 6         | John Cena   | 400    | 3    |
| 1         | Winston     | 500    | 6    |
| 2         | Marie       | 200    | 4    |

**Output:**  

| person_name |
|-------------|
| John Cena   |

**Explanation:**  

The table below tracks the cumulative weight:  

| Turn | ID | Name      | Weight | Total Weight | Notes               |
|------|----|-----------|--------|--------------|---------------------|
| 1    | 5  | Alice     | 250    | 250          | Alice boards.       |
| 2    | 3  | Alex      | 350    | 600          | Alex boards.        |
| 3    | 6  | John Cena | 400    | 1000         | John Cena boards.   |
| 4    | 2  | Marie     | 200    | 1200         | Marie **cannot** board. |
| 5    | 4  | Bob       | 175    | ___          | -                   |
| 6    | 1  | Winston   | 500    | ___          | -                   |

Thus, **John Cena** is the last person to board without exceeding the weight limit.

## ANSWER  

```sql
WITH CumulativeWeight AS (
    SELECT 
        person_name,
        weight,
        turn,
        SUM(weight) OVER (ORDER BY turn) AS total_weight
    FROM 
        Queue
)
SELECT 
    person_name
FROM 
    CumulativeWeight
WHERE 
    total_weight <= 1000
ORDER BY 
    turn DESC
LIMIT 1;
```
----------------------
## [1907 - Count Salary Categories](https://leetcode.com/problems/count-salary-categories)

## Table: Accounts

| Column Name | Type |
|-------------|------|
| account_id  | int  |
| income      | int  |

`account_id` is the primary key (column with unique values) for this table.  
Each row contains information about the monthly income for one bank account.

## Problem Statement

Write a solution to calculate the number of bank accounts for each salary category. The salary categories are:

- "Low Salary": All the salaries strictly less than $20,000.
- "Average Salary": All the salaries in the inclusive range [$20,000, $50,000].
- "High Salary": All the salaries strictly greater than $50,000.

The result table must contain all three categories. If there are no accounts in a category, return 0.

Return the result table in any order.

### Example 1:

**Input:**  
Accounts table:  

| account_id | income  |
|------------|---------|
| 3          | 108939  |
| 2          | 12747   |
| 8          | 87709   |
| 6          | 91796   |

**Output:**  

| category        | accounts_count |
|-----------------|----------------|
| Low Salary      | 1              |
| Average Salary  | 0              |
| High Salary     | 3              |

**Explanation:**  
- **Low Salary**: Account 2 with income 12747.  
- **Average Salary**: No accounts fall in this range.  
- **High Salary**: Accounts 3, 6, and 8 have incomes greater than 50000.  

## ANSWER  
```sql
WITH CategorizedAccounts AS (
    SELECT 
        CASE 
            WHEN income < 20000 THEN 'Low Salary'
            WHEN income BETWEEN 20000 AND 50000 THEN 'Average Salary'
            ELSE 'High Salary'
        END AS category
    FROM 
        Accounts
)
SELECT 
    AllCategories.category AS category,  -- Explicitly specify the source
    COUNT(CategorizedAccounts.category) AS accounts_count
FROM (
    SELECT 'Low Salary' AS category
    UNION ALL
    SELECT 'Average Salary'
    UNION ALL
    SELECT 'High Salary'
) AS AllCategories
LEFT JOIN CategorizedAccounts
ON AllCategories.category = CategorizedAccounts.category
GROUP BY AllCategories.category;

```
--------------------------
# Subqueries

## [1978 - Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company)

## Table: Employees

| Column Name | Type     |
|-------------|----------|
| employee_id | int      |
| name        | varchar  |
| manager_id  | int      |
| salary      | int      |

`employee_id` is the primary key for this table.  
This table contains information about the employees, their salary, and the ID of their manager. Some employees do not have a manager (`manager_id` is null). 

## Problem Statement

Find the IDs of the employees whose salary is strictly less than $30,000 and whose manager left the company. When a manager leaves the company, their information is deleted from the `Employees` table, but the reports still have their `manager_id` set to the manager that left.

Return the result table ordered by `employee_id`.

### Example 1:

**Input:**  
Employees table:

| employee_id | name      | manager_id | salary |
|-------------|-----------|------------|--------|
| 3           | Mila      | 9          | 60301  |
| 12          | Antonella | null       | 31000  |
| 13          | Emery     | null       | 67084  |
| 1           | Kalel     | 11         | 21241  |
| 9           | Mikaela   | null       | 50937  |
| 11          | Joziah    | 6          | 28485  |

**Output:**  

| employee_id |
|-------------|
| 11          |

**Explanation:**  
The employees with a salary less than $30,000 are 1 (Kalel) and 11 (Joziah).  
Kalel's manager is employee 11, who is still in the company (Joziah).  
Joziah's manager is employee 6, who left the company because there is no row for employee 6 (as it was deleted).

## ANSWER  
```sql
SELECT 
    e.employee_id
FROM 
    Employees e
WHERE 
    e.salary < 30000 
    AND e.manager_id IS NOT NULL
    AND e.manager_id NOT IN (
        SELECT employee_id
        FROM Employees
    )
ORDER BY 
    e.employee_id;

```

------------------------
## [626 - Exchange Seats](https://leetcode.com/problems/exchange-seats)

## Table: Seat

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| student     | varchar |

`id` is the primary key (unique value) column for this table.  
Each row of this table indicates the name and the ID of a student.  
The ID sequence always starts from 1 and increments continuously.

## Problem Statement

Write a solution to swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.

Return the result table ordered by `id` in ascending order.

### Example 1:

**Input:**  
Seat table:

| id | student |
|----|---------|
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |

**Output:**  

| id | student |
|----|---------|
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |

**Explanation:**  
Note that if the number of students is odd, there is no need to change the last one's seat.

## ANSWER  
```sql
SELECT 
    CASE 
        WHEN MOD(id, 2) = 1 AND id + 1 <= (SELECT MAX(id) FROM Seat) THEN id + 1
        WHEN MOD(id, 2) = 0 THEN id - 1
        ELSE id
    END AS id,
    student
FROM Seat
ORDER BY id;

```

---------------------------
## [1341 - Movie Rating](https://leetcode.com/problems/movie-rating)

## Table: Movies

| Column Name   | Type    |
|---------------|---------|
| movie_id      | int     |
| title         | varchar |

`movie_id` is the primary key (column with unique values) for this table.  
`title` is the name of the movie.

## Table: Users

| Column Name   | Type    |
|---------------|---------|
| user_id       | int     |
| name          | varchar |

`user_id` is the primary key (column with unique values) for this table.  
The column `name` has unique values.

## Table: MovieRating

| Column Name   | Type    |
|---------------|---------|
| movie_id      | int     |
| user_id       | int     |
| rating        | int     |
| created_at    | date    |

`(movie_id, user_id)` is the primary key (column with unique values) for this table.  
This table contains the rating of a movie by a user in their review.  
`created_at` is the user's review date.

## Problem Statement

Write a solution to:

1. Find the name of the user who has rated the greatest number of movies. In case of a tie, return the lexicographically smaller user name.
2. Find the movie name with the highest average rating in February 2020. In case of a tie, return the lexicographically smaller movie name.

### Example 1:

**Input:**  
Movies table:

| movie_id | title     |
|----------|-----------|
| 1        | Avengers  |
| 2        | Frozen 2  |
| 3        | Joker     |

Users table:

| user_id | name    |
|---------|---------|
| 1       | Daniel  |
| 2       | Monica  |
| 3       | Maria   |
| 4       | James   |

MovieRating table:

| movie_id | user_id | rating | created_at |
|----------|---------|--------|------------|
| 1        | 1       | 3      | 2020-01-12 |
| 1        | 2       | 4      | 2020-02-11 |
| 1        | 3       | 2      | 2020-02-12 |
| 1        | 4       | 1      | 2020-01-01 |
| 2        | 1       | 5      | 2020-02-17 |
| 2        | 2       | 2      | 2020-02-01 |
| 2        | 3       | 2      | 2020-03-01 |
| 3        | 1       | 3      | 2020-02-22 |
| 3        | 2       | 4      | 2020-02-25 |

**Output:**

| results   |
|-----------|
| Daniel    |
| Frozen 2  |

**Explanation:**  
- Daniel and Monica have rated 3 movies ("Avengers", "Frozen 2", and "Joker"), but Daniel is lexicographically smaller.
- Frozen 2 and Joker have an average rating of 3.5 in February, but Frozen 2 is lexicographically smaller.

## ANSWER  
```sql
WITH UserRatingCount AS (
    SELECT 
        u.name AS user_name,
        COUNT(mr.movie_id) AS rating_count
    FROM Users u
    JOIN MovieRating mr ON u.user_id = mr.user_id
    GROUP BY u.name
),
TopUser AS (
    SELECT 
        user_name
    FROM UserRatingCount
    ORDER BY rating_count DESC, user_name ASC
    LIMIT 1
),
MovieAverageRating AS (
    SELECT 
        m.title AS movie_title,
        AVG(mr.rating) AS avg_rating
    FROM Movies m
    JOIN MovieRating mr ON m.movie_id = mr.movie_id
    WHERE mr.created_at BETWEEN '2020-02-01' AND '2020-02-29'
    GROUP BY m.title
),
TopMovie AS (
    SELECT 
        movie_title
    FROM MovieAverageRating
    ORDER BY avg_rating DESC, movie_title ASC
    LIMIT 1
)
SELECT 
    user_name AS results
FROM TopUser
UNION ALL
SELECT 
    movie_title AS results
FROM TopMovie;

```

-----------------------------------

## [1321 - Restaurant Growth](https://leetcode.com/problems/restaurant-growth)

## Table: Customer

| Column Name   | Type    |
|---------------|---------|
| customer_id   | int     |
| name          | varchar |
| visited_on    | date    |
| amount        | int     |

`(customer_id, visited_on)` is the primary key for this table.  
This table contains data about customer transactions in a restaurant.  
`visited_on` is the date on which the customer with ID (`customer_id`) has visited the restaurant.  
`amount` is the total paid by a customer.

## Problem Statement

You are the restaurant owner and you want to analyze a possible expansion (there will be at least one customer every day).

Compute the moving average of how much the customer paid in a seven days window (i.e., current day + 6 days before).  
`average_amount` should be rounded to two decimal places.

Return the result table ordered by `visited_on` in ascending order.

### Example 1:

**Input:**  
Customer table:

| customer_id | name    | visited_on  | amount |
|-------------|---------|-------------|--------|
| 1           | Jhon    | 2019-01-01  | 100    |
| 2           | Daniel  | 2019-01-02  | 110    |
| 3           | Jade    | 2019-01-03  | 120    |
| 4           | Khaled  | 2019-01-04  | 130    |
| 5           | Winston | 2019-01-05  | 110    |
| 6           | Elvis   | 2019-01-06  | 140    |
| 7           | Anna    | 2019-01-07  | 150    |
| 8           | Maria   | 2019-01-08  | 80     |
| 9           | Jaze    | 2019-01-09  | 110    |
| 1           | Jhon    | 2019-01-10  | 130    |
| 3           | Jade    | 2019-01-10  | 150    |

**Output:**  

| visited_on | amount | average_amount |
|------------|--------|----------------|
| 2019-01-07 | 860    | 122.86         |
| 2019-01-08 | 840    | 120            |
| 2019-01-09 | 840    | 120            |
| 2019-01-10 | 1000   | 142.86         |

**Explanation:**  
1. 1st moving average from 2019-01-01 to 2019-01-07 has an `average_amount` of (100 + 110 + 120 + 130 + 110 + 140 + 150) / 7 = 122.86  
2. 2nd moving average from 2019-01-02 to 2019-01-08 has an `average_amount` of (110 + 120 + 130 + 110 + 140 + 150 + 80) / 7 = 120  
3. 3rd moving average from 2019-01-03 to 2019-01-09 has an `average_amount` of (120 + 130 + 110 + 140 + 150 + 80 + 110) / 7 = 120  
4. 4th moving average from 2019-01-04 to 2019-01-10 has an `average_amount` of (130 + 110 + 140 + 150 + 80 + 110 + 130 + 150) / 7 = 142.86

## ANSWER  
```sql
SELECT
    visited_on,
    (
        SELECT SUM(amount)
        FROM customer
        WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
    ) AS amount,
    ROUND(
        (
            SELECT SUM(amount) / 7
            FROM customer
            WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
        ),
        2
    ) AS average_amount
FROM customer c
WHERE visited_on >= (
        SELECT DATE_ADD(MIN(visited_on), INTERVAL 6 DAY)
        FROM customer
    )
GROUP BY visited_on;
```

-------------------------

## [602 - Friend Requests II: Who Has the Most Friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends)

## Table: RequestAccepted

| Column Name    | Type    |
|----------------|---------|
| requester_id   | int     |
| accepter_id    | int     |
| accept_date    | date    |

(requester_id, accepter_id) is the primary key (combination of columns with unique values) for this table.  
This table contains the ID of the user who sent the request, the ID of the user who received the request, and the date when the request was accepted.

## Problem Statement

Write a solution to find the people who have the most friends and the most friends number.

The test cases are generated so that only one person has the most friends.

Return the result in the following format:

### Example 1:

**Input:**  
RequestAccepted table:

| requester_id | accepter_id | accept_date |
|--------------|-------------|-------------|
| 1            | 2           | 2016/06/03  |
| 1            | 3           | 2016/06/08  |
| 2            | 3           | 2016/06/08  |
| 3            | 4           | 2016/06/09  |

**Output:**  

| id | num |
|----|-----|
| 3  | 3   |

**Explanation:**  
The person with id 3 is a friend of people 1, 2, and 4, so they have three friends in total, which is the most number compared to anyone else.

## Follow-up:  
In the real world, multiple people could have the same most number of friends. Could you find all these people in this case?

## ANSWER
```sql
WITH all_ids AS (
    SELECT ra.requester_id AS id, COUNT(*) AS cnt
    FROM RequestAccepted ra
    GROUP BY ra.requester_id

    UNION ALL -- don't remove duplicates

    SELECT ra.accepter_id AS id, COUNT(*) AS cnt 
    FROM RequestAccepted ra
    GROUP BY ra.accepter_id
)

SELECT id, SUM(cnt) AS num
FROM all_ids
GROUP BY id
ORDER BY num DESC
LIMIT 1
```

---------------------------------

## [585 - Investments in 2016](https://leetcode.com/problems/investments-in-2016)

## Table: Insurance

| Column Name | Type   |
|-------------|--------|
| pid         | int    |
| tiv_2015    | float  |
| tiv_2016    | float  |
| lat         | float  |
| lon         | float  |

pid is the primary key (column with unique values) for this table.  
Each row of this table contains information about one policy where:
- pid is the policyholder's policy ID.
- tiv_2015 is the total investment value in 2015, and tiv_2016 is the total investment value in 2016.
- lat is the latitude of the policyholder's city, and lon is the longitude. It's guaranteed that lat and lon are not NULL.

## Problem Statement

Write a solution to report the sum of all total investment values in 2016 (tiv_2016), for all policyholders who:
1. Have the same tiv_2015 value as one or more other policyholders.
2. Are not located in the same city as any other policyholder (i.e., the `(lat, lon)` attribute pairs must be unique).

Round tiv_2016 to two decimal places.

### Example 1:

**Input:**  
Insurance table:

| pid | tiv_2015 | tiv_2016 | lat | lon |
|-----|----------|----------|-----|-----|
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |

**Output:**  

| tiv_2016 |
|----------|
| 45.00    |

**Explanation:**  
The first record in the table, like the last record, meets both of the two criteria:
1. The tiv_2015 value of 10 is the same as the third and fourth records.
2. Its location is unique.

The second record does not meet either of the two criteria. Its tiv_2015 is not like any other policyholder, and its location is the same as the third record, which makes the third record fail as well.

Thus, the result is the sum of tiv_2016 of the first and last record, which is 45.

## ANSWER
```sql
WITH DuplicateTIV AS (
    -- Identify the tiv_2015 values that are duplicated
    SELECT tiv_2015
    FROM Insurance
    GROUP BY tiv_2015
    HAVING COUNT(*) > 1
),
UniqueLocation AS (
    -- Identify the (lat, lon) pairs that are unique
    SELECT lat, lon
    FROM Insurance
    GROUP BY lat, lon
    HAVING COUNT(*) = 1
)
SELECT ROUND(SUM(i.tiv_2016), 2) AS tiv_2016
FROM Insurance i
JOIN DuplicateTIV d ON i.tiv_2015 = d.tiv_2015
JOIN UniqueLocation u ON i.lat = u.lat AND i.lon = u.lon;

```

-------------------------------

## [185 - Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries)

## Table: Employee

| Column Name  | Type    |
|--------------|---------|
| id           | int     |
| name         | varchar |
| salary       | int     |
| departmentId | int     |

id is the primary key (column with unique values) for this table.  
departmentId is a foreign key (reference column) of the ID from the Department table.  
Each row of this table indicates the ID, name, and salary of an employee. It also contains the ID of their department.

## Table: Department

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
  
id is the primary key (column with unique values) for this table.  
Each row of this table indicates the ID of a department and its name.

## Problem Statement

A company's executives are interested in seeing who earns the most money in each of the company's departments. A high earner in a department is an employee who has a salary in the top three unique salaries for that department.

Write a solution to find the employees who are high earners in each of the departments.

Return the result table in any order.

### Example 1:

**Input:**  
Employee table:

| id  | name  | salary | departmentId |
|-----|-------|--------|--------------|
| 1   | Joe   | 85000  | 1            |
| 2   | Henry | 80000  | 2            |
| 3   | Sam   | 60000  | 2            |
| 4   | Max   | 90000  | 1            |
| 5   | Janet | 69000  | 1            |
| 6   | Randy | 85000  | 1            |
| 7   | Will  | 70000  | 1            |

Department table:

| id  | name  |
|-----|-------|
| 1   | IT    |
| 2   | Sales |

**Output:**  

| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Joe      | 85000  |
| IT         | Randy    | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |

**Explanation:**  
In the IT department:
- Max earns the highest unique salary
- Both Randy and Joe earn the second-highest unique salary
- Will earns the third-highest unique salary

In the Sales department:
- Henry earns the highest salary
- Sam earns the second-highest salary
- There is no third-highest salary as there are only two employees in this department.

## ANSWER
```sql
WITH EmpsWithDeps AS (
  SELECT 
    Employee.id AS empId,
    Department.id AS depId,
    Employee.name AS empName,
    Department.name AS depName,
    Employee.salary AS salary,
    dense_rank() OVER (
      PARTITION BY Department.id 
      ORDER BY Employee.salary DESC
    ) AS `rank`
  FROM Employee
  JOIN Department ON Employee.departmentId = Department.id
)

SELECT 
  depName AS Department,
  empName AS Employee,
  salary AS Salary
FROM EmpsWithDeps 
WHERE `rank` < 4;

```

------------------------------------
# Advanced String Functions / Regex / Clause


## [1667 - Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table)

## Table: Users

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| name        | varchar |

user_id is the primary key (column with unique values) for this table.  
This table contains the ID and the name of the user. The name consists of only lowercase and uppercase characters.

## Problem Statement

Write a solution to fix the names so that only the first character is uppercase and the rest are lowercase.

Return the result table ordered by user_id.

### Example 1:

**Input:**  
Users table:

| user_id | name  |
|---------|-------|
| 1       | aLice |
| 2       | bOB   |

**Output:**  

| user_id | name  |
|---------|-------|
| 1       | Alice |
| 2       | Bob   |

**Explanation:**  
- For user_id = 1, the name "aLice" is converted to "Alice" (first letter uppercase, rest lowercase).
- For user_id = 2, the name "bOB" is converted to "Bob" (first letter uppercase, rest lowercase).

## ANSWER
```sql
SELECT 
    user_id, 
    CONCAT(UPPER(SUBSTRING(name, 1, 1)), LOWER(SUBSTRING(name, 2))) AS name
FROM Users
ORDER BY user_id;

```

----------------------------------

## [1527 - Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition)

## Table: Patients

| Column Name   | Type    |
|---------------|---------|
| patient_id    | int     |
| patient_name  | varchar |
| conditions    | varchar |

patient_id is the primary key (column with unique values) for this table.  
'conditions' contains 0 or more codes separated by spaces.  
This table contains information of the patients in the hospital.

## Problem Statement

Write a solution to find the patient_id, patient_name, and conditions of the patients who have Type I Diabetes. Type I Diabetes always starts with the DIAB1 prefix.

Return the result table in any order.

### Example 1:

**Input:**  
Patients table:

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 1          | Daniel       | YFEV COUGH   |
| 2          | Alice        |              |
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
| 5          | Alain        | DIAB201      |

**Output:**  

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 | 

**Explanation:**  
Bob and George both have a condition that starts with DIAB1.

## ANSWER
```sql
select patient_id,patient_name,conditions from Patients
where conditions like 'DIAB1%'  or  conditions like '% DIAB1%' ;
```
--------------------------------------------------------------------------

## [196 - Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails)

## Table: Person

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| email       | varchar |

id is the primary key (column with unique values) for this table.  
Each row of this table contains an email. The emails will not contain uppercase letters.

## Problem Statement

Write a solution to delete all duplicate emails, keeping only one unique email with the smallest id.

For SQL users, please note that you are supposed to write a DELETE statement and not a SELECT one.

For Pandas users, please note that you are supposed to modify Person in place.

After running your script, the answer shown is the Person table. The driver will first compile and run your piece of code and then show the Person table. The final order of the Person table does not matter.

### Example 1:

**Input:**  
Person table:

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

**Output:**  

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |

**Explanation:**  
john@example.com is repeated two times. We keep the row with the smallest Id = 1.

## ANSWER
```sql
delete p1 from person p1,person p2 
where p1.email=p2.email and p1.id>p2.id;
```

----------------------------------------------------------------------

## [176 - Second Highest Salary](https://leetcode.com/problems/second-highest-salary)

## Table: Employee

| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

id is the primary key (column with unique values) for this table.  
Each row of this table contains information about the salary of an employee.

## Problem Statement

Write a solution to find the second highest distinct salary from the Employee table. If there is no second highest salary, return `null` (or `None` in Pandas).

### Example 1:

**Input:**  
Employee table:

| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

**Output:**  

| SecondHighestSalary |
|---------------------|
| 200                 |

### Example 2:

**Input:**  
Employee table:

| id | salary |
|----|--------|
| 1  | 100    |

**Output:**  

| SecondHighestSalary |
|---------------------|
| null                |

## Answer

```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

-------------------------------------------------------------------------------

## [1484 - Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date)

## Table: Activities

| Column Name | Type    |
|-------------|---------|
| sell_date   | date    |
| product     | varchar |

There is no primary key (column with unique values) for this table. It may contain duplicates.  
Each row of this table contains the product name and the date it was sold in a market.

## Problem Statement

Write a solution to find for each date the number of different products sold and their names.

The sold products' names for each date should be sorted lexicographically.

Return the result table ordered by `sell_date`.

### Example 1:

**Input:**  
Activities table:

| sell_date  | product     |
|------------|-------------|
| 2020-05-30 | Headphone   |
| 2020-06-01 | Pencil      |
| 2020-06-02 | Mask        |
| 2020-05-30 | Basketball  |
| 2020-06-01 | Bible       |
| 2020-06-02 | Mask        |
| 2020-05-30 | T-Shirt     |

**Output:**  

| sell_date  | num_sold | products                     |
|------------|----------|------------------------------|
| 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
| 2020-06-01 | 2        | Bible,Pencil                 |
| 2020-06-02 | 1        | Mask                         |

**Explanation:**  
- For `2020-05-30`, the sold items were (Headphone, Basketball, T-shirt), which are sorted lexicographically and separated by commas.
- For `2020-06-01`, the sold items were (Pencil, Bible), sorted and separated by commas.
- For `2020-06-02`, only the item `Mask` was sold.

## ANSWER
```sql
select sell_date, count( DISTINCT product ) as num_sold ,
    
    GROUP_CONCAT( DISTINCT product order by product ASC separator ',' ) as products
    
        FROM Activities GROUP BY sell_date order by sell_date ASC;
```

-------------------------------------------------------------------------------------------


## [1327 - List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period)

## Table: Products

| Column Name      | Type    |
|------------------|---------|
| product_id       | int     |
| product_name     | varchar |
| product_category | varchar |

`product_id` is the primary key (column with unique values) for this table.  
This table contains data about the company's products.

## Table: Orders

| Column Name   | Type    |
|---------------|---------|
| product_id    | int     |
| order_date    | date    |
| unit          | int     |

`product_id` is a foreign key (reference column) to the Products table.  
This table may have duplicate rows.

## Problem Statement

Write a solution to get the names of products that have at least 100 units ordered in February 2020 and their amount.

Return the result table in any order.

### Example 1:

**Input:**  
Products table:

| product_id | product_name          | product_category |
|------------|-----------------------|------------------|
| 1          | Leetcode Solutions    | Book             |
| 2          | Jewels of Stringology | Book             |
| 3          | HP                    | Laptop           |
| 4          | Lenovo                | Laptop           |
| 5          | Leetcode Kit          | T-shirt          |

Orders table:

| product_id | order_date | unit |
|------------|------------|------|
| 1          | 2020-02-05 | 60   |
| 1          | 2020-02-10 | 70   |
| 2          | 2020-01-18 | 30   |
| 2          | 2020-02-11 | 80   |
| 3          | 2020-02-17 | 2    |
| 3          | 2020-02-24 | 3    |
| 4          | 2020-03-01 | 20   |
| 4          | 2020-03-04 | 30   |
| 4          | 2020-03-04 | 60   |
| 5          | 2020-02-25 | 50   |
| 5          | 2020-02-27 | 50   |
| 5          | 2020-03-01 | 50   |

**Output:**  

| product_name       | unit |
|--------------------|------|
| Leetcode Solutions | 130  |
| Leetcode Kit       | 100  |

**Explanation:**  
- Product with `product_id = 1` was ordered in February a total of (60 + 70) = 130 units.
- Product with `product_id = 2` was ordered in February a total of 80 units.
- Product with `product_id = 3` was ordered in February a total of (2 + 3) = 5 units.
- Product with `product_id = 4` was not ordered in February 2020.
- Product with `product_id = 5` was ordered in February a total of (50 + 50) = 100 units.

## ANSWER
```sql
SELECT p.product_name AS product_name, sum(o.unit) AS unit FROM Products p
JOIN Orders o USING (product_id)
WHERE YEAR(o.order_date)='2020' AND MONTH(o.order_date)='02'
GROUP BY p.product_id
HAVING SUM(o.unit)>=100
```

--------------------------------------------------------------------------------------

## [1517 - Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails)

## Table: Users

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| name        | varchar |
| mail        | varchar |

`user_id` is the primary key (column with unique values) for this table.  
This table contains information about the users signed up on a website. Some e-mails are invalid.

## Problem Statement

Write a solution to find the users who have valid emails.

A valid e-mail has a prefix name and a domain where:

- The prefix name is a string that may contain letters (upper or lower case), digits, underscore '_', period '.', and/or dash '-'. The prefix name must start with a letter.
- The domain is `@leetcode.com`.

Return the result table in any order.

### Example 1:

**Input:**  
Users table:

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 2       | Jonathan  | jonathanisgreat         |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |
| 5       | Marwan    | quarz#2020@leetcode.com |
| 6       | David     | david69@gmail.com       |
| 7       | Shapiro   | .shapo@leetcode.com     |

**Output:**  

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |

**Explanation:**  
- The mail of user 2 does not have a domain.
- The mail of user 5 has the `#` sign, which is not allowed.
- The mail of user 6 does not have the `leetcode.com` domain.
- The mail of user 7 starts with a period.

## ANSWER
```sql
SELECT * 
FROM Users
WHERE mail REGEXP '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$';

```
