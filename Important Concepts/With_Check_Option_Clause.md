# MySQL With Check Option Clause

Sometimes, you create a view to reveal the partial data of a table. However, a simple view is updatable, and therefore,
it is possible to update data that is not visible through the view. This update makes the view inconsistent.
To ensure the consistency of the view, you use the WITH CHECK OPTION clause when you create or modify the view.

The WITH CHECK OPTION is an optional clause of the CREATE VIEW statement. 
This WITH CHECK OPTION prevents you from updating or inserting rows that are not visible through the view.

In other words, whenever you update or insert a row of the base tables through a view, 
MySQL ensures that the insert or update operation conforms with the definition of the view.

```sql
CREATE OR REPLACE VIEW view_name
AS
  select_statement
WITH CHECK OPTION;
```

In this syntax, you add the WITH CHECK OPTION clause at the end of the CREATE VIEW statement.

```sql
CREATE DATABASE mydb;

USE mydb;

CREATE TABLE employees(
    id INT AUTO_INCREMENT PRIMARY KEY,
    type VARCHAR(50) NOT NULL,
    name VARCHAR(255) NOT NULL
);

INSERT INTO employees (type, name) 
VALUES
('Full-time', 'John Doe'),
('Contractor', 'Jane Smith'),
('Temp', 'Alice Johnson'),
('Full-time', 'Bob Anderson'),
('Contractor', 'Charlie Brown'),
('Temp', 'David Lee'),
('Full-time', 'Eva Martinez'),
('Contractor', 'Frank White'),
('Temp', 'Grace Taylor'),
('Full-time', 'Henry Walker'),
('Contractor', 'Ivy Davis'),
('Temp', 'Jack Turner'),
('Full-time', 'Kelly Harris'),
('Contractor', 'Leo Wilson'),
('Temp', 'Mia Rodriguez'),
('Full-time', 'Nick Carter'),
('Contractor', 'Olivia Clark'),
('Temp', 'Pauline Hall'),
('Full-time', 'Quincy Adams');

SELECT * FROM employees;
```

| id | type       | name          |
|:--:|:----------:|:-------------:|
|  1 | Full-time  | John Doe      |
|  2 | Contractor | Jane Smith    |
|  3 | Temp       | Alice Johnson |
|  4 | Full-time  | Bob Anderson  |
|  5 | Contractor | Charlie Brown |
|  6 | Temp       | David Lee     |
|  7 | Full-time  | Eva Martinez  |
|  8 | Contractor | Frank White   |
|  9 | Temp       | Grace Taylor  |
| 10 | Full-time  | Henry Walker  |
| 11 | Contractor | Ivy Davis     |
| 12 | Temp       | Jack Turner   |
| 13 | Full-time  | Kelly Harris  |
| 14 | Contractor | Leo Wilson    |
| 15 | Temp       | Mia Rodriguez |
| 16 | Full-time  | Nick Carter   |
| 17 | Contractor | Olivia Clark  |
| 18 | Temp       | Pauline Hall  |
| 19 | Full-time  | Quincy Adams  |


Second, create a view called contractors based on the employees table

```sql
CREATE OR REPLACE VIEW contractors
AS
SELECT id, type, name
FROM
  employees
WHERE
type = 'Contractor';

SELECT * FROM contractors;
```

| id | type       | name          |
|:--:|:----------:|:-------------:|
|  2 | Contractor | Jane Smith    |
|  5 | Contractor | Charlie Brown |
|  8 | Contractor | Frank White   |
| 11 | Contractor | Ivy Davis     |
| 14 | Contractor | Leo Wilson    |
| 17 | Contractor | Olivia Clark  |



The contractors view is updatable. For example, you can insert a new row into the employees table via the contractor view:

```sql
INSERT INTO contractors(name, type)
VALUES('Andy Black', 'Contractor');
```

OUTPUT:
```
Query OK, 1 row affected (0.00 sec)
```

The statement inserts a new employee with the type Contractor into the employees table via the contractors view.

Fourth, retrieve data from the contractors view:

```sql
SELECT * FROM contractors
```

| id | type       | name          |
|:--:|:----------:|:-------------:|
|  2 | Contractor | Jane Smith    |
|  5 | Contractor | Charlie Brown |
|  8 | Contractor | Frank White   |
| 11 | Contractor | Ivy Davis     |
| 14 | Contractor | Leo Wilson    |
| 17 | Contractor | Olivia Clark  |
| 20 | Contractor | Andy Black    |


The output shows that Andy Black has been added successfully.

**The problem is that you can add an employee with other types such as Full-time into the employees table via the contractors view.** For example:

INSERT INTO contractors(name, type)
VALUES('Deric Seetoh', 'Full-time')

Query OK, 1 row affected (0.00 sec)

This statement successfully inserts a new row that is not visible via the contractors view into the employees table.
**To prevent this, you need to add the WITH CHECK OPTION clause to the CREATE OR REPLACE VIEW statement like this:**

```sql
CREATE OR REPLACE VIEW contractors
AS
SELECT id, type, name
FROM
  employees
WHERE
  type = 'Contractor'
WITH CHECK OPTION;
```

**If you attempt to insert or update rows that are not visible via the contractor, you’ll get an error. For example:**
```sql
INSERT INTO contractors(name, type)
VALUES('Brad Knox', 'Full-time')
```
OUTPUT:
```
ERROR 1369 (HY000): CHECK OPTION failed 'mydb.contractors'
```

Because of the WITH CHECK OPTION, MySQL checks if the INSERT statement conforms with the SELECT statement that defines the view. 
If the INSERT statement does not conform, MySQL rejects it and issues an error.


Include the `WITH CHECK OPTION` clause in the CREATE VIEW statement to ensure the consistency of the view.
