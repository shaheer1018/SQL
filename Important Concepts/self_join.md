## Sample Data
```sql
CREATE TABLE employees (
    employee_id INT,
    employee_name VARCHAR(50),
    manager_id INT
);

INSERT INTO employees (employee_id, employee_name, manager_id) VALUES (1, 'John Doe', NULL);
INSERT INTO employees (employee_id, employee_name, manager_id) VALUES (2, 'Jane Smith', 1);
INSERT INTO employees (employee_id, employee_name, manager_id) VALUES (3, 'Alice Johnson', 1);
INSERT INTO employees (employee_id, employee_name, manager_id) VALUES (4, 'Bob Brown', 2);
INSERT INTO employees (employee_id, employee_name, manager_id) VALUES (5, 'Charlie Davis', 3);

```

| employee_id | employee_name | manager_id |
|:------------|:-------------:|:----------:|
|           1 | John Doe      |       NULL |
|           2 | Jane Smith    |          1 |
|           3 | Alice Johnson |          1 |
|           4 | Bob Brown     |          2 |
|           5 | Charlie Davis |          3 |



```sql
SELECT e.employee_name AS employee_name,
       m.employee_name AS manager_name
FROM employees e 
JOIN employees m 
     ON e.manager_id = m.employee_id
```

| employee_name | manager_name  |
|:-------------:|:-------------:|
| Alice Johnson | John Doe      |
| Jane Smith    | John Doe      |
| Bob Brown     | Jane Smith    |
| Charlie Davis | Alice Johnson |
