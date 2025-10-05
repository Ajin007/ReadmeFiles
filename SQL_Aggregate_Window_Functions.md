
# Aggregate and Window Functions in SQL

## 1. Aggregate Functions

Aggregate functions are used to perform calculations on a set of values and return a single value. Common aggregate functions include:

- **COUNT()**: Returns the number of rows in a set.
- **SUM()**: Returns the sum of a numeric column.
- **AVG()**: Returns the average value of a numeric column.
- **MIN()**: Returns the smallest value in a set.
- **MAX()**: Returns the largest value in a set.

### Example Table: `Employee_Salaries`

| Employee_ID | Name     | Department  | Salary |
|-------------|----------|-------------|--------|
| 101         | John     | HR          | 50000  |
| 102         | Jane     | IT          | 60000  |
| 103         | Jack     | HR          | 55000  |
| 104         | Jill     | IT          | 65000  |
| 105         | James    | IT          | 70000  |
| 106         | Jaden    | HR          | 52000  |

#### **Aggregate Functions Example**

1. **Sum of Salaries**:
```sql
SELECT SUM(Salary) AS Total_Salary FROM Employee_Salaries;
```
**Output**:
| Total_Salary |
|--------------|
| 402000       |

2. **Average Salary**:
```sql
SELECT AVG(Salary) AS Average_Salary FROM Employee_Salaries;
```
**Output**:
| Average_Salary |
|----------------|
| 60000          |

3. **Count of Employees in IT Department**:
```sql
SELECT Department, COUNT(*) AS Employee_Count 
FROM Employee_Salaries
WHERE Department = 'IT'
GROUP BY Department;
```
**Output**:
| Department | Employee_Count |
|------------|----------------|
| IT         | 3              |

4. **Maximum Salary**:
```sql
SELECT MAX(Salary) AS Max_Salary FROM Employee_Salaries;
```
**Output**:
| Max_Salary |
|------------|
| 70000      |

---

## 2. Window Functions

Window functions operate on a set of rows related to the current row. They are used to perform calculations across a specified range of rows, and unlike aggregate functions, they do not collapse the result set.

Common window functions include:

- **ROW_NUMBER()**: Assigns a unique number to each row based on a given order.
- **RANK()**: Assigns a rank to each row within a result set, with gaps in ranks for ties.
- **DENSE_RANK()**: Similar to `RANK()` but without gaps for ties.
- **NTILE()**: Divides rows into a specified number of buckets.
- **SUM()**, **AVG()**, **MIN()**, **MAX()**: Can be used as window functions to perform calculations over a window of rows.

#### Example with Window Functions

1. **Row Number**:
```sql
SELECT Employee_ID, Name, Department, Salary,
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum
FROM Employee_Salaries;
```
**Output**:
| Employee_ID | Name     | Department  | Salary | RowNum |
|-------------|----------|-------------|--------|--------|
| 105         | James    | IT          | 70000  | 1      |
| 104         | Jill     | IT          | 65000  | 2      |
| 102         | Jane     | IT          | 60000  | 3      |
| 103         | Jack     | HR          | 55000  | 4      |
| 106         | Jaden    | HR          | 52000  | 5      |
| 101         | John     | HR          | 50000  | 6      |

2. **Rank Based on Salary**:
```sql
SELECT Employee_ID, Name, Department, Salary,
       RANK() OVER (ORDER BY Salary DESC) AS Salary_Rank
FROM Employee_Salaries;
```
**Output**:
| Employee_ID | Name     | Department  | Salary | Salary_Rank |
|-------------|----------|-------------|--------|-------------|
| 105         | James    | IT          | 70000  | 1           |
| 104         | Jill     | IT          | 65000  | 2           |
| 102         | Jane     | IT          | 60000  | 3           |
| 103         | Jack     | HR          | 55000  | 4           |
| 106         | Jaden    | HR          | 52000  | 5           |
| 101         | John     | HR          | 50000  | 6           |

3. **Total Salary per Department (Window Function)**:
```sql
SELECT Employee_ID, Name, Department, Salary,
       SUM(Salary) OVER (PARTITION BY Department) AS Dept_Total_Salary
FROM Employee_Salaries;
```
**Output**:
| Employee_ID | Name     | Department  | Salary | Dept_Total_Salary |
|-------------|----------|-------------|--------|-------------------|
| 101         | John     | HR          | 50000  | 259000            |
| 103         | Jack     | HR          | 55000  | 259000            |
| 106         | Jaden    | HR          | 52000  | 259000            |
| 102         | Jane     | IT          | 60000  | 195000            |
| 104         | Jill     | IT          | 65000  | 195000            |
| 105         | James    | IT          | 70000  | 195000            |

4. **Average Salary per Department**:
```sql
SELECT Employee_ID, Name, Department, Salary,
       AVG(Salary) OVER (PARTITION BY Department) AS Dept_Avg_Salary
FROM Employee_Salaries;
```
**Output**:
| Employee_ID | Name     | Department  | Salary | Dept_Avg_Salary |
|-------------|----------|-------------|--------|-----------------|
| 101         | John     | HR          | 50000  | 51833.33        |
| 103         | Jack     | HR          | 55000  | 51833.33        |
| 106         | Jaden    | HR          | 52000  | 51833.33        |
| 102         | Jane     | IT          | 60000  | 65000           |
| 104         | Jill     | IT          | 65000  | 65000           |
| 105         | James    | IT          | 70000  | 65000           |

---

## 3. Summary of Key Differences Between Aggregate and Window Functions

| **Aggregate Functions**                       | **Window Functions**                     |
|-----------------------------------------------|------------------------------------------|
| Collapse the result set to a single row       | Operate on a set of rows without collapsing the result set |
| Must use `GROUP BY` for grouping data         | Can calculate over a window of rows without needing `GROUP BY` |
| Return a single value for each group (if `GROUP BY` is used) | Return a value for each row within the window |
| Example: `SUM(Salary)`, `COUNT(*)`, `AVG(Salary)` | Example: `ROW_NUMBER()`, `RANK()`, `SUM(Salary) OVER` |

---

## Conclusion

- **Aggregate functions** are used for calculations like sums, averages, and counts over groups of data.
- **Window functions** allow you to perform calculations across a set of rows while keeping the result set intact, providing more granular analysis and insights.

Feel free to copy the code and try it out to understand how each function works!


# SQL Aggregate and Window Functions

## Table Setup

First, create the `faculty` table and insert sample data to demonstrate the concepts.

### Create Table and Insert Data

```sql
CREATE TABLE faculty (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(100),
    salary DECIMAL(10, 2)
);

-- Inserting sample data
INSERT INTO faculty (id, name, department, salary) VALUES
(1, 'Dr. Victor Gray', 'Biology', 93000),
(2, 'Dr. Betty Rose', 'Biology', 91000),
(3, 'Dr. Wendy Moss', 'Biology', 91000),
(4, 'Dr. Adam Kane', 'Computer Science', 95000),
(5, 'Dr. Rachel Green', 'Computer Science', 93000),
(6, 'Dr. Monica Bellucci', 'Physics', 100000),
(7, 'Dr. Lisa White', 'Physics', 95000);
```

---

## **1. Aggregate Functions**

Aggregate functions are used to perform calculations across a set of rows. Common examples include `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`.

### Example 1: `COUNT()`

Find the total number of professors in each department.

```sql
SELECT department, COUNT(*) AS total_professors
FROM faculty
GROUP BY department;
```

#### Output:

| department       | total_professors |
|------------------|------------------|
| Biology          | 3                |
| Computer Science | 2                |
| Physics          | 2                |

### Example 2: `SUM()`

Calculate the total salary for each department.

```sql
SELECT department, SUM(salary) AS total_salary
FROM faculty
GROUP BY department;
```

#### Output:

| department       | total_salary |
|------------------|--------------|
| Biology          | 275000       |
| Computer Science | 188000       |
| Physics          | 195000       |

### Example 3: `AVG()`

Find the average salary for each department.

```sql
SELECT department, AVG(salary) AS avg_salary
FROM faculty
GROUP BY department;
```

#### Output:

| department       | avg_salary |
|------------------|------------|
| Biology          | 91666.67   |
| Computer Science | 94000.00   |
| Physics          | 97500.00   |

### Example 4: `MIN()` and `MAX()`

Find the highest and lowest salary in each department.

```sql
SELECT department, MIN(salary) AS min_salary, MAX(salary) AS max_salary
FROM faculty
GROUP BY department;
```

#### Output:

| department       | min_salary | max_salary |
|------------------|------------|------------|
| Biology          | 91000.00   | 93000.00   |
| Computer Science | 93000.00   | 95000.00   |
| Physics          | 95000.00   | 100000.00  |

---

## **2. Advanced Aggregate Functions**

### Example 1: `GROUP_CONCAT()`

Concatenate all professor names from each department into a single string.

```sql
SELECT department, GROUP_CONCAT(name ORDER BY salary DESC) AS professors
FROM faculty
GROUP BY department;
```

#### Output:

| department       | professors                              |
|------------------|-----------------------------------------|
| Biology          | Dr. Victor Gray,Dr. Betty Rose,Dr. Wendy Moss |
| Computer Science | Dr. Adam Kane,Dr. Rachel Green          |
| Physics          | Dr. Monica Bellucci,Dr. Lisa White      |

### Example 2: `HAVING` – Filter After Aggregation

Find departments where the total salary is greater than 200,000.

```sql
SELECT department, SUM(salary) AS total_salary
FROM faculty
GROUP BY department
HAVING SUM(salary) > 200000;
```

#### Output:

| department       | total_salary |
|------------------|--------------|
| Biology          | 275000       |
| Computer Science | 188000       |

### Example 3: `ROLLUP` and `CUBE` – Subtotals and Grand Totals

#### Using `ROLLUP`

```sql
SELECT department, SUM(salary) AS total_salary
FROM faculty
GROUP BY department WITH ROLLUP;
```

#### Output:

| department       | total_salary |
|------------------|--------------|
| Biology          | 275000       |
| Computer Science | 188000       |
| Physics          | 195000       |
| NULL             | 658000       |  (Grand Total)

---

## **3. Window Functions**

Window functions operate across a range of rows, allowing for row-by-row calculations without collapsing the result set.

### Example 1: `DENSE_RANK()` – Ranking Professors by Salary

Rank professors within each department by salary in descending order.

```sql
SELECT name, department, salary,
       DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS salary_rank
FROM faculty;
```

#### Output:

| name               | department       | salary | salary_rank |
|--------------------|------------------|--------|-------------|
| Dr. Victor Gray    | Biology          | 93000  | 1           |
| Dr. Betty Rose     | Biology          | 91000  | 2           |
| Dr. Wendy Moss     | Biology          | 91000  | 2           |
| Dr. Adam Kane      | Computer Science | 95000  | 1           |
| Dr. Rachel Green   | Computer Science | 93000  | 2           |
| Dr. Monica Bellucci| Physics          | 100000 | 1           |
| Dr. Lisa White     | Physics          | 95000  | 2           |

### Example 2: `ROW_NUMBER()` – Assigning Unique Row Numbers

Assign a unique row number to each professor within their department.

```sql
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_number
FROM faculty;
```

#### Output:

| name               | department       | salary | row_number |
|--------------------|------------------|--------|------------|
| Dr. Victor Gray    | Biology          | 93000  | 1          |
| Dr. Betty Rose     | Biology          | 91000  | 2          |
| Dr. Wendy Moss     | Biology          | 91000  | 3          |
| Dr. Adam Kane      | Computer Science | 95000  | 1          |
| Dr. Rachel Green   | Computer Science | 93000  | 2          |
| Dr. Monica Bellucci| Physics          | 100000 | 1          |
| Dr. Lisa White     | Physics          | 95000  | 2          |

### Example 3: `SUM()` Over a Window – Cumulative Salary

Calculate the cumulative salary for each department.

```sql
SELECT name, department, salary,
       SUM(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS cumulative_salary
FROM faculty;
```

#### Output:

| name               | department       | salary | cumulative_salary |
|--------------------|------------------|--------|-------------------|
| Dr. Victor Gray    | Biology          | 93000  | 93000             |
| Dr. Betty Rose     | Biology          | 91000  | 184000            |
| Dr. Wendy Moss     | Biology          | 91000  | 275000            |
| Dr. Adam Kane      | Computer Science | 95000  | 95000             |
| Dr. Rachel Green   | Computer Science | 93000  | 188000            |
| Dr. Monica Bellucci| Physics          | 100000 | 100000            |
| Dr. Lisa White     | Physics          | 95000  | 195000            |

---

## **4. Advanced Window Functions**

### Example 1: `NTILE()` – Distributing Rows into Groups

Distribute professors into 2 groups based on salary.

```sql
SELECT name, department, salary,
       NTILE(2) OVER (ORDER BY salary DESC) AS salary_group
FROM faculty;
```

#### Output:

| name               | department       | salary | salary_group |
|--------------------|------------------|--------|--------------|
| Dr. Monica Bellucci| Physics          | 100000 | 1            |
| Dr. Adam Kane      | Computer Science | 95000  | 1            |
| Dr. Lisa White     | Physics          | 95000  | 1            |
| Dr. Victor Gray    | Biology          | 93000  | 2            |
| Dr. Rachel Green   | Computer Science | 93000  | 2            |
| Dr. Betty Rose     | Biology          | 91000  | 2            |
| Dr. Wendy Moss     | Biology          | 91000  | 2            |

### Example 2: `LEAD()` – Accessing the Next Row’s Data

Get the next salary for each professor.

```sql
SELECT name, department, salary,
       LEAD(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS next_salary
FROM faculty;
```

#### Output:

| name               | department       | salary | next_salary |
|--------------------|------------------|--------|-------------|
| Dr. Monica Bellucci| Physics          | 100000 | 95000       |
| Dr. Lisa White     | Physics          | 95000  | NULL        |
| Dr. Adam Kane      | Computer Science | 95000  | 93000       |
| Dr. Rachel Green   | Computer Science | 93000  | NULL        |
| Dr. Victor Gray    | Biology          | 93000  | 91000       |
| Dr. Betty Rose     | Biology          | 91000  | 91000       |
| Dr. Wendy Moss     | Biology          | 91000  | NULL        |

---

### Example 3: `PERCENT_RANK()` – Relative Rank as Percentage

Calculate the relative rank in percentage for each professor.

```sql
SELECT name, department, salary,
       PERCENT_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS percent_rank
FROM faculty;
```

#### Output:

| name               | department       | salary | percent_rank |
|--------------------|------------------|--------|--------------|
| Dr. Monica Bellucci| Physics          | 100000 | 0.000000     |
| Dr. Lisa White     | Physics          | 95000  | 1.000000     |
| Dr. Adam Kane      | Computer Science | 95000  | 0.000000     |
| Dr. Rachel Green   | Computer Science | 93000  | 1.000000     |
| Dr. Victor Gray    | Biology          | 93000  | 0.000000     |
| Dr. Betty Rose     | Biology          | 91000  | 0.500000     |
| Dr. Wendy Moss     | Biology          | 91000  | 0.500000     |

---

## Conclusion

By combining both **Aggregate Functions** and **Window Functions**, SQL allows you to perform advanced data analysis and generate meaningful insights across your data. Understanding and utilizing these concepts effectively will enable you to handle complex queries and reports.

Let me know if you'd like further explanations or have specific questions!


Feel free to copy the code and try it out to understand how each function works!
