## COALESCE Function in MySQL

A coalesce function in SQL is used to return the first non-null expression in a list of expressions. 
It's quite handy for dealing with situations where you want to replace null values with some default or non-null value.

Let's say we have a table named customers with the following schema:

```sql
CREATE TABLE customers(
       id INT PRIMARY KEY,
       first_name VARCHAR(50),
       last_name VARCHAR(50),
       email VARCHAR(100),
       phone VARCHAR(20));
```

And some data to the table:
```sql
INSERT INTO customers (id, first_name, last_name, email, phone)
VALUES
(1, 'John', 'Doe', NULL, '123-456-7890'),
(2, NULL, 'Smith', 'smith@example.com', NULL),
(3, 'Alice', 'Johnson', 'alice@example.com', '987-654-3210');
```

|  id  |  first_name  | last_name   |       email       |    phone     |
|:----:|:------------:|:-----------:|:-----------------:|:------------:|      
|   1  |    John      |    Doe      | NULL              | 123-456-7890 |
|   2  |    NULL      |   Smith     | smith@example.com | NULL         |
|   3  |    Alice     |   Johnson   | alice@example.com | 987-654-3210 |


Now let's say we want to select the customer's email, but if it is null we want to display their phone number instead. We can use the COALESCE function for this 

```sql
SELECT id,
       last_name,
       COALESCE(email, phone) AS contact_info
FROM customers;
```

| id | last_name |   contact_info    |
|:--:|:---------:|:-----------------:|
| 1  |   Doe     |   123-456-7890    |
| 2  |   Smith   | smith@example.com |
| 3  |  Johnson  | alice@example.com |
