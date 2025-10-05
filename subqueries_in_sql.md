
# Understanding Subqueries in SQL

A **subquery** is a query within another query. It is often used to perform a secondary operation that provides values for the main query. Subqueries can be used in the `SELECT`, `FROM`, or `WHERE` clauses.

## Types of Subqueries:
1. **Scalar Subquery**: Returns a single value (e.g., a single number or string).
2. **Multi-row Subquery**: Returns multiple rows.
3. **Multi-column Subquery**: Returns multiple columns.
4. **Correlated Subquery**: The inner query refers to columns from the outer query.

---

## 1. Scalar Subquery

This subquery returns a single value and is often used in the `WHERE` clause.

**Scenario**: You are asked to find employees who earn more than the average salary in a company.

### SQL Query:
```sql
SELECT employee_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

**Explanation**:
- The inner subquery `(SELECT AVG(salary) FROM employees)` calculates the average salary of all employees.
- The outer query fetches the `employee_name` and `salary` for employees whose salary is greater than the average salary calculated by the subquery.

---

## 2. Multi-row Subquery

This subquery returns multiple rows and is often used in the `WHERE` clause with operators like `IN`, `NOT IN`.

**Scenario**: You want to find the employees who belong to departments that have more than 10 employees.

### SQL Query:
```sql
SELECT employee_name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING COUNT(*) > 10
);
```

**Explanation**:
- The inner subquery finds the `department_id`s that have more than 10 employees.
- The outer query fetches the `employee_name` for employees who belong to those departments.

---

## 3. Multi-column Subquery

This subquery returns multiple columns and is often used in the `WHERE` clause.

**Scenario**: You want to find employees who work in the same department and have the same salary as other employees.

### SQL Query:
```sql
SELECT employee_name, department_id, salary
FROM employees
WHERE (department_id, salary) IN (
    SELECT department_id, salary
    FROM employees
    WHERE employee_name <> 'John Doe'
);
```

**Explanation**:
- The inner subquery returns pairs of `department_id` and `salary` for employees other than 'John Doe'.
- The outer query fetches the `employee_name`, `department_id`, and `salary` for employees who work in the same department and have the same salary as someone else.

---

## 4. Correlated Subquery

A correlated subquery is one where the inner query references columns from the outer query. It’s evaluated for each row processed by the outer query.

**Scenario**: You want to find employees who earn more than the average salary in their own department.

### SQL Query:
```sql
SELECT employee_name, salary, department_id
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);
```

**Explanation**:
- The inner subquery calculates the average salary for each `department_id`, but it refers to `e.department_id` from the outer query.
- The outer query compares each employee’s salary with the average salary of their department.

---

## 5. Subqueries in the `FROM` Clause

You can use subqueries in the `FROM` clause to create temporary tables or derive complex datasets.

**Scenario**: You want to get the average salary for each department, but in a more complex setup, you may want to join with other data.

### SQL Query:
```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM (
    SELECT department_id, salary
    FROM employees
    WHERE salary > 30000
) AS high_paid_employees
GROUP BY department_id;
```

**Explanation**:
- The inner subquery `(SELECT department_id, salary FROM employees WHERE salary > 30000)` fetches employees who earn more than $30,000.
- The outer query calculates the average salary for each department from the employees who meet that condition.

---

## Subquery Performance Considerations:
- **Avoid using subqueries in `SELECT` or `FROM` clauses if possible**: Subqueries can sometimes be inefficient, particularly when they need to be evaluated multiple times (e.g., correlated subqueries).
- **Use `JOIN` instead of subqueries when applicable**: In some cases, using `JOIN` operations can perform better than subqueries, especially in larger datasets.

---

## Complete Code Example

Let's put everything together. Here's an example that combines multiple subquery techniques in a more complex scenario.

**Scenario**: You work in a hospital database. You want to find the top 3 doctors based on their average patient ratings, and you want to ensure that these doctors have seen at least 5 patients.

**Tables**:
- **doctors** (doctor_id, name)
- **appointments** (appointment_id, doctor_id, patient_id, rating)

### SQL Query:
```sql
SELECT doctor_id, name, AVG(rating) AS avg_rating
FROM doctors
WHERE doctor_id IN (
    SELECT doctor_id
    FROM appointments
    GROUP BY doctor_id
    HAVING COUNT(DISTINCT patient_id) >= 5
)
GROUP BY doctor_id
ORDER BY avg_rating DESC
LIMIT 3;
```

**Explanation**:
- The inner subquery selects `doctor_id`s that have at least 5 distinct patients (using `HAVING COUNT(DISTINCT patient_id) >= 5`).
- The outer query selects doctors from the `doctors` table who have been in the list of doctors returned by the subquery.
- It then calculates the average rating (`AVG(rating)`) for each doctor and orders them by the average rating in descending order, returning the top 3 doctors.

---

## Key Takeaways:
- Subqueries can be used to filter data, compute aggregates, or provide conditions for the main query.
- They can be placed in the `WHERE`, `FROM`, or `SELECT` clauses depending on the use case.
- **Correlated subqueries** can be powerful but should be used with caution as they can be inefficient for large datasets.
- For more complex queries, consider using **JOINs** as an alternative to subqueries, especially when working with multiple related tables.

