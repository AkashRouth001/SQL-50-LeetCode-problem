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
