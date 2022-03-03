# `Complete-SQL`

## Table of Contents 📋
| **SNo.** | **Topic** | **Sub Topic** |
| -------- | --------- | ------------- |
| 1.       | [Retrieving Data From a Single Table](#1-retrieving-data-from-a-single-table) | [SELECT Clause](#11-select-clause) <br> [WHERE Clause](#12-where-clause) <br> [AND, OR & NOT Operators](#13-and-or--not-operators) <br> [IN Operators](#14-in-operators) <br> [BETWEEN Operators](#15-between-operators) <br> [LIKE Operators](#16-like-operators) <br> [REGEXP Operators](#17-regexp-operators) <br> [IS NULL Operators](#18-is-null-operators) <br> [ORDER BY Operators](#19-order-by-operators) <br> [LIMIT Clause](#110-limit-clause)|
| 2.       | [Retrieving Data From a Multiple Table](#2-retrieving-data-from-a-multiple-table) |    |
---

## 1. Retrieving Data From a Single Table
   - ### 1.1 SELECT Clause
      ```sql
      SELECT *
      FROM customers;
      ```
      | customer_id| first_name | last_name | points | state | phone_no | birth_date |
      |-------------|-----------|-----------|--------|-------|----------|------------|
      |             |           |           |        |       |          |            |
      |             |           |           |        |       |          |            |
      
      ```sql
      SELECT first_name, last_name
      FROM customers;
      ```
      | first_name | last_name |
      |------------|-----------|
      |            |           |
      |            |           |
      
      ```sql
      SELECT 
        first_name, 
        last_name,
        points,
        (points % 10) AS 'discount factor'
      FROM customers;
      ```
      
      | first_name | last_name | points | discount factor |
      |------------|-----------|--------|-----------------|
      |            |           |        |                 |
      |            |           |        |                 |

      `Exercise`
      - Return All the Products
         - name
         - unit price
         - new price (unit price * 1.1)

         `Solution`
         ```sql
         SELECT 
           name,
           unit_price,
           (unit_price * 1.1) AS new_price
         FROM products;
         ```
      
         | name | unit_price | new_price |
         |------|------------|-----------|
         |      |            |           |
         |      |            |           |
   
   - ## 1.2 WHERE Clause
      ```sql
      SELECT *
      FROM customers
      WHERE points > 3000;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE state = 'va';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date > '1990-01-01';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Get the orders places this years

         `Solution`
         ```sql
         SELECT *
         FROM orders
         WHERE order_date >= '2022-01-01';
         ```
         | order_id | customer_id | first_name | last_name | points | status | order_date |
         |----------|-------------|------------|-----------|--------|--------|------------|
         |          |             |            |           |        |        |            |
         |          |             |            |           |        |        |            |
         
   - ### 1.3 AND, OR & NOT Operators
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date > '1990-01-01' AND points > 1000;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date > '1990-01-01' OR points > 1000 AND state = 'va';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE NOT (birth_date > '1990-01-01' OR points > 1000);
      ```
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date <= '1990-01-01' AND points <= 1000;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - From the order_items table, get the item
         - For order #6
         - where the total price is greater than 30

         `Solution`
         ```sql
         SELECT *
         FROM order_items
         WHERE order_id = 6 AND unit_price * quantity > 30;
         ```
         | order_id | product_id | unit_price | quantity | order_item |
         |----------|------------|------------|----------|------------|
         |          |            |            |          |            |
         |          |            |            |          |            |
         
   - ### 1.4 IN Operators
      ```sql
      SELECT *
      FROM customers
      WHERE state = 'va' OR state = 'ga' OR state = 'fl';
      ```
      ```sql
      SELECT *
      FROM customers
      WHERE state IN ('va', 'ga', 'fl');
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE state NOT IN ('va', 'ga', 'fl');
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Return products with
         - quantity in stock equal to 49, 38, 72

         `Solution`
         ```sql
         SELECT *
         FROM products
         WHERE quantity_in_stock IN (49, 38, 72);
         ```
         | order_id | product_id | unit_price | quantity_in_stocks | order_item |
         |----------|------------|------------|--------------------|------------|
         |          |            |            |                    |            |
         |          |            |            |                    |            |
         
   - ### 1.5 BETWEEN Operators
      ```sql
      SELECT *
      FROM customers
      WHERE points >= 1000 AND points <= 3000;
      ```
      ```sql
      SELECT *
      FROM customers
      WHERE points BETWEEN 1000 AND 3000;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Return customers born
         - between 1/1/1990 AND 1/1/2000

         `Solution`
         ```sql
         SELECT *
         FROM customers
         WHERE birth_date BETWEEN '1990-01-01` AND `2000-01-01`;
         ```
         | customer_id | first_name | last_name | points | state | phone_no | birth_date |
         |-------------|------------|-----------|--------|-------|----------|------------|
         |             |            |           |        |       |          |            |
         |             |            |           |        |       |          |            |
         
   - ### 1.6 LIKE Operators
      - `% -----> Any number of characters`
      - `_ -----> Single Character`
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE 'b%';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE 'brush%';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE '%b%';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE '%y';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE '_y';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE '_______y';  
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE 'b_______y';  
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Get the customers whose
         - addresses contain TRAIL or AVENUE
         - phone number end with 9

         `Solution`         
         
         - `addresses contain TRAIL or AVENUE`
         ```sql
         SELECT *
         FROM customers
         WHERE 
            address LIKE '%trail%' OR 
            address LIKE '%avenue%';  
         ```
         | customer_id | first_name | last_name | points | address | phone_no | birth_date |
         |-------------|------------|-----------|--------|---------|----------|------------|
         |             |            |           |        |         |          |            |
         |             |            |           |        |         |          |            |
         
         - `phone number end with 9`
         ```sql
         SELECT *
         FROM customers
         WHERE  phone_no LIKE '%9';  
         ```
         | customer_id | first_name | last_name | points | address | phone_no | birth_date |
         |-------------|------------|-----------|--------|---------|----------|------------|
         |             |            |           |        |         |          |            |
         |             |            |           |        |         |          |            |
         
   - ### 1.7 REGEXP Operators
      - `^ -----> beginning`
      - `$ -----> end`
      - `| -----> logical or`
      - `[gim]e -----> ge, ie, me`
      - `e[faq] -----> ef, ea, eq`
      - `[a-f]g -----> ag, bg, cg, dg, eg, fg`
      ```sql
      SELECT *
      FROM customers
      WHERE last_name LIKE '%brush%';
      ```
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP 'brush';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP '^brush';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP 'brush$';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP 'brush|mac';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP 'brush|mac|field';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP '^brush|mac|field';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP 'brush$|mac|field';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP '[gim]e';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP 'e[abc]';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE last_name REGEXP '[a-h]e';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Get the customers whose
         - first names are ELKA or AMAR
         - last names end with EY or ON
         - last names start with MY or contains SE
         - last names contain B followed by R or U

         `Solution`
         - `first names are ELKA or AMAR`
         ```sql
         SELECT *
         FROM customers
         WHERE first_name REGEXP 'elka | amar';
         ```
         | customer_id | first_name | last_name | points | state | phone_no | birth_date |
         |-------------|------------|-----------|--------|-------|----------|------------|
         |             |            |           |        |       |          |            |
         |             |            |           |        |       |          |            |
         
         - `last names end with EY or ON`
         ```sql
         SELECT *
         FROM customers
         WHERE last_name REGEXP 'ey$ | on$';
         ```
         | customer_id | first_name | last_name | points | state | phone_no | birth_date |
         |-------------|------------|-----------|--------|-------|----------|------------|
         |             |            |           |        |       |          |            |
         |             |            |           |        |       |          |            |
         
         - `last names start with MY or contains SE`
         ```sql
         SELECT *
         FROM customers
         WHERE last_name REGEXP '^my | se';
         ```
         | customer_id | first_name | last_name | points | state | phone_no | birth_date |
         |-------------|------------|-----------|--------|-------|----------|------------|
         |             |            |           |        |       |          |            |
         |             |            |           |        |       |          |            |
         
         - `last names contain B followed by R or U`
         ```sql
         SELECT *
         FROM customers
         WHERE last_name REGEXP 'b[ru]';
         ```sql
         SELECT *
         FROM customers
         WHERE last_name REGEXP 'br | bu';
         ```
         | customer_id | first_name | last_name | points | state | phone_no | birth_date |
         |-------------|------------|-----------|--------|-------|----------|------------|
         |             |            |           |        |       |          |            |
         |             |            |           |        |       |          |            |
         
   - ### 1.8 IS NULL Operators
      ```sql
      SELECT *
      FROM customers
      WHERE phone_no IS NULL;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE phone_no IS NOT NULL;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Get the orders that are not shipped

         `Solution`
         ```sql
         SELECT *
         FROM orders
         WHERE shipped_date IS NULL;
         ```
         | order_id | customer_id | first_name | last_name | points | status | shipped_date | order_date |
         |----------|-------------|------------|-----------|--------|--------|--------------|------------|
         |          |             |            |           |        |        |              |            |
         |          |             |            |           |        |        |              |            |
         
   - ### 1.9 ORDER BY Operators
      ```sql
      SELECT *
      FROM customers
      ORDER BY first_name;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      ORDER BY first_name DESC;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      ORDER BY first_name, state;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      ORDER BY first_name DESC, state DESC;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT first_name, last_name
      FROM customers
      ORDER BY birth_date;
      ```
      |first_name  | last_name |
      |------------|-----------|
      |            |           |
      |            |           |
      
      ```sql
      SELECT first_name, last_name, 10 AS points
      FROM customers
      ORDER BY first_name, points;
      ```
      ```sql
      SELECT first_name, last_name, 10 AS points
      FROM customers
      ORDER BY 1, 3;
      ```
      |first_name  | last_name | points |
      |------------|-----------|--------|
      |            |           |        |
      |            |           |        |
         
   - ### 1.10 LIMIT Clause
      - `LIMIT 6 -----> print first 6 rows(1, 2, 3, 4, 5, 6)`
      - `LIMIT 6, 3 -----> Skip first 6 rows(1, 2, 3, 4, 5, 6) then print 3 rows(7, 8, 9)`

      ```sql
      SELECT *
      FROM customers
      LIMIT 6;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      LIMIT 6, 3;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      |             |            |           |        |       |          |            |

      `Exercise`
      - Get the top three loyal customers

         `Solution`
         ```sql
         SELECT *
         FROM customers
         ORDER BY points DESC
         LIMIT 3;
         ```
         | customer_id | first_name | last_name | points | state | phone_no | birth_date |
         |-------------|------------|-----------|--------|-------|----------|------------|
         |             |            |           |        |       |          |            |
         |             |            |           |        |       |          |            |
      
## 2. Retrieving Data From a Multiple Table
