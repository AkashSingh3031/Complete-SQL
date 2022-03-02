# `Complete-SQL`

## Table of Contents 📋
| **SNo.** | **Topic** | **Sub Topic** |
| -------- | --------- | ------------- |
| 1.       | [Retrieving Data From a Single Table](#1-retrieving-data-from-a-single-table) | [SELECT Clause](#11-select-clause) <br> [WHERE Clause](#12-where-clause) <br> [AND, OR & NOT Operators](#13-and-or--not-operators) <br> [IN Operators](#14-in-operators)|

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
      
      ```sql
      SELECT first_name, last_name
      FROM customers;
      ```
      
      | first_name | last_name |
      |------------|-----------|
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
           (unit_price * 1.1) AS 'new_price`
         FROM products;
         ```
      
         | name | unit_price | new_price |
         |------|------------|-----------|
         |      |            |           |
   
   - ## 1.2 WHERE Clause
      ```sql
      SELECT *
      FROM customers
      WHERE points > 3000;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |           |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE state = 'va';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |            |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date > '1990-01-01';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
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
         
   - ### 1.3 AND, OR & NOT Operators
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date > '1990-01-01' AND points > 1000;
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
      |             |           |           |        |       |          |            |
      
      ```sql
      SELECT *
      FROM customers
      WHERE birth_date > '1990-01-01' OR points > 1000 AND state = 'va';
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
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
      
      ```sql
      SELECT *
      FROM customers
      WHERE state NOT IN ('va', 'ga', 'fl');
      ```
      | customer_id | first_name | last_name | points | state | phone_no | birth_date |
      |-------------|------------|-----------|--------|-------|----------|------------|
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
