### Create a sample table called customers with some dummy data

```sql
CREATE TABLE customers (
    customer_id INT,
    customer_name VARCHAR(50)
);

INSERT INTO customers (customer_id, customer_name) VALUES (1, 'John Doe');
INSERT INTO customers (customer_id, customer_name) VALUES (2, 'Jane Smith');
INSERT INTO customers (customer_id, customer_name) VALUES (3, 'Alice Johnson');
INSERT INTO customers (customer_id, customer_name) VALUES (4, 'Bob Brown');
INSERT INTO customers (customer_id, customer_name) VALUES (5, 'Charlie Davis');

```

### OUTPUT
| customer_id | customer_name |
| ----------- | ------------- |
|     1       | John Doe      |
|     2       | Jane Smith    |
|     3       | Alice Johnson |
|     4       | Bob Brown     |
|     5       | Charlie Davis |
