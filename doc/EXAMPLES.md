# 📚 Runnable T-SQL Examples

**30+ ready-to-run queries** for **MS SQL Server Simulator v10 Enterprise Edition**.

Every example below is **authentic Microsoft T-SQL syntax** that runs unchanged in the simulator thanks to the 65+ rule auto-translation engine. Load one of the 13 sample databases (Tools → Load Sample Database) and paste any example into the editor.

> Built by **Adewale Samson Adeagbo** · HMG Concepts · [cssadewale.pages.dev](https://cssadewale.pages.dev)

---

## 📖 How to Use

1. Press `Ctrl+N` for a new query window
2. Paste any example below
3. Press `F5` to execute
4. Watch the **Messages** tab — it tells you which T-SQL rules were translated

---

## 🟢 Beginner — SELECT Basics (Examples 1–8)

### 1. SELECT TOP — Authentic T-SQL paging

```sql
SELECT TOP 10
    first_name,
    last_name,
    department,
    salary
FROM employees
ORDER BY salary DESC;
```

*Translation:* `TOP 10` → `LIMIT 10` automatically appended.

---

### 2. WHERE with multiple conditions

```sql
SELECT *
FROM employees
WHERE department IN ('Engineering', 'Sales')
  AND salary BETWEEN 500000 AND 1000000
  AND city = 'Lagos';
```

---

### 3. Pattern matching with LIKE

```sql
SELECT first_name, last_name, city
FROM employees
WHERE first_name LIKE 'A%'
   OR last_name LIKE '%i';
```

---

### 4. NULL handling with ISNULL

```sql
SELECT
    first_name,
    ISNULL(city, 'Unknown') AS city,
    ISNULL(phone, 'No phone') AS contact
FROM customers;
```

*Translation:* `ISNULL` → SQLite `IFNULL`.

---

### 5. String length with LEN

```sql
SELECT
    first_name,
    LEN(first_name) AS name_length,
    LEN(last_name) AS surname_length
FROM employees
WHERE LEN(first_name) > 5;
```

*Translation:* `LEN()` → `LENGTH()`.

---

### 6. Find position with CHARINDEX

```sql
SELECT
    customer_name,
    email,
    CHARINDEX('@', email) AS at_position
FROM customers;
```

*Translation:* `CHARINDEX(needle, hay)` → `INSTR(hay, needle)` (arguments swapped automatically).

---

### 7. Date functions: GETDATE, YEAR, MONTH

```sql
SELECT
    first_name,
    hire_date,
    YEAR(hire_date) AS year_joined,
    MONTH(hire_date) AS month_joined,
    GETDATE() AS today
FROM employees
ORDER BY hire_date;
```

*Translation:* `GETDATE()` → `datetime('now','localtime')`, `YEAR()` → `STRFTIME('%Y',...)`.

---

### 8. Conditional with IIF

```sql
SELECT
    first_name,
    salary,
    IIF(salary > 800000, 'High',
        IIF(salary > 500000, 'Mid', 'Low')) AS salary_band,
    IIF(perf_score >= 4.5, '⭐ Top', 'Standard') AS performance
FROM employees;
```

*Translation:* Nested `IIF` → nested `CASE WHEN ... THEN ... ELSE ... END`.

---

## 🟦 Intermediate — JOINs & Aggregates (Examples 9–16)

### 9. INNER JOIN with two tables

```sql
SELECT
    e.first_name,
    e.last_name,
    e.salary,
    d.budget AS dept_budget,
    d.head AS dept_head
FROM dbo.employees e
INNER JOIN dbo.departments d ON e.department = d.department
ORDER BY e.salary DESC;
```

*Translation:* `dbo.` schema prefix dropped.

---

### 10. LEFT JOIN with COALESCE

```sql
SELECT
    c.customer_name,
    c.tier,
    COUNT(o.order_id) AS total_orders,
    COALESCE(SUM(o.total_amount), 0) AS lifetime_value
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.customer_name, c.tier
ORDER BY lifetime_value DESC;
```

---

### 11. GROUP BY with HAVING

```sql
SELECT
    department,
    COUNT(*) AS headcount,
    ROUND(AVG(salary), 0) AS avg_salary,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary
FROM employees
GROUP BY department
HAVING COUNT(*) >= 3
ORDER BY avg_salary DESC;
```

---

### 12. CASE expressions

```sql
SELECT
    region,
    COUNT(*) AS order_count,
    SUM(CASE WHEN status = 'Delivered' THEN total_amount ELSE 0 END) AS delivered_revenue,
    SUM(CASE WHEN status = 'Cancelled' THEN total_amount ELSE 0 END) AS lost_revenue,
    ROUND(100.0 * SUM(CASE WHEN status = 'Delivered' THEN 1 ELSE 0 END) / COUNT(*), 1) AS delivery_rate_pct
FROM orders
GROUP BY region
ORDER BY delivered_revenue DESC;
```

---

### 13. DATEDIFF — Days since hire

```sql
SELECT TOP 10
    first_name,
    hire_date,
    DATEDIFF(day, hire_date, GETDATE()) AS days_employed,
    DATEDIFF(day, hire_date, GETDATE()) / 365 AS years_employed
FROM employees
ORDER BY days_employed DESC;
```

*Translation:* `DATEDIFF` → julianday math.

---

### 14. DATEADD — Future date calculation

```sql
SELECT
    first_name,
    hire_date,
    DATEADD(year, 5, hire_date) AS five_year_anniversary,
    DATEADD(day, 90, GETDATE()) AS ninety_days_from_now
FROM employees
ORDER BY hire_date;
```

*Translation:* `DATEADD` → `datetime(d, '+N units')`.

---

### 15. CONVERT and CAST

```sql
SELECT
    first_name,
    salary,
    CONVERT(VARCHAR, salary) AS salary_text,
    CAST(salary AS REAL) / 1000 AS salary_thousands,
    'NGN ' + CONVERT(VARCHAR, salary) AS display
FROM employees;
```

*Translation:* `CONVERT(type, val)` → `CAST(val AS type)`, `+` string concat → `||`.

---

### 16. Subquery in SELECT

```sql
SELECT
    e.first_name,
    e.department,
    e.salary,
    (SELECT AVG(salary) FROM employees WHERE department = e.department) AS dept_avg,
    e.salary - (SELECT AVG(salary) FROM employees WHERE department = e.department) AS vs_dept_avg
FROM employees e
ORDER BY vs_dept_avg DESC;
```

---

## 🟧 Advanced — CTEs, Window Functions, PIVOT (Examples 17–24)

### 17. CTE — Common Table Expression

```sql
WITH dept_stats AS (
    SELECT
        department,
        COUNT(*) AS headcount,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
),
company_avg AS (
    SELECT AVG(salary) AS overall_avg FROM employees
)
SELECT
    d.department,
    d.headcount,
    ROUND(d.avg_salary, 0) AS avg_salary,
    ROUND(c.overall_avg, 0) AS company_avg,
    ROUND(d.avg_salary - c.overall_avg, 0) AS vs_company
FROM dept_stats d, company_avg c
ORDER BY vs_company DESC;
```

---

### 18. Window Function — RANK by department

```sql
SELECT
    first_name,
    department,
    salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank,
    DENSE_RANK() OVER (ORDER BY salary DESC) AS overall_rank,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_num
FROM employees
ORDER BY department, dept_rank;
```

---

### 19. Running total with SUM OVER

```sql
SELECT
    txn_date,
    description,
    txn_type,
    amount,
    SUM(CASE WHEN txn_type = 'Credit' THEN amount ELSE -amount END)
        OVER (ORDER BY txn_date, txn_id) AS running_balance
FROM transactions
ORDER BY txn_date, txn_id;
```

---

### 20. LAG / LEAD — Period-over-period change

```sql
SELECT
    txn_date,
    amount,
    LAG(amount) OVER (ORDER BY txn_date) AS prev_amount,
    LEAD(amount) OVER (ORDER BY txn_date) AS next_amount,
    amount - LAG(amount) OVER (ORDER BY txn_date) AS change_from_prev
FROM transactions
WHERE txn_type = 'Credit'
ORDER BY txn_date;
```

---

### 21. PIVOT — Region totals as columns (NEW v10.1)

```sql
SELECT region, [Lagos], [Abuja], [Kano]
FROM (SELECT region, total_amount FROM orders) AS src
PIVOT (SUM(total_amount) FOR region IN ([Lagos], [Abuja], [Kano])) AS pvt;
```

*Translation:* `PIVOT` → conditional aggregates with `CASE`.

---

### 22. MERGE — UPSERT pattern (NEW v10.1)

```sql
MERGE INTO employees AS target
USING (SELECT 99 AS id, 'Adaeze' AS nm, 850000 AS sal) AS source (id, nm, sal)
ON target.employee_id = source.id
WHEN MATCHED THEN UPDATE SET salary = source.sal
WHEN NOT MATCHED THEN INSERT (employee_id, first_name, salary)
    VALUES (source.id, source.nm, source.sal);
```

*Translation:* `MERGE` → `INSERT … ON CONFLICT DO UPDATE`.

---

### 23. STRING_AGG — Concatenate within a group

```sql
SELECT
    department,
    COUNT(*) AS headcount,
    STRING_AGG(first_name, ', ') AS team_members
FROM employees
GROUP BY department
ORDER BY headcount DESC;
```

*Translation:* `STRING_AGG` → `GROUP_CONCAT`.

---

### 24. FORMAT — Currency, percentage, number (NEW v10.1)

```sql
SELECT
    first_name,
    department,
    FORMAT(salary, 'C') AS pay_currency,
    FORMAT(salary, 'N') AS pay_number,
    FORMAT(perf_score / 5.0, 'P') AS performance_pct
FROM employees
ORDER BY salary DESC;
```

*Translation:* `FORMAT(n,'C')` → `'$' || printf('%,.2f', n)`.

---

## 🟥 Enterprise — System, Variables, DDL (Examples 25–32)

### 25. Variables — DECLARE / SET / @ references

```sql
DECLARE @minSalary INT = 600000;
DECLARE @dept VARCHAR(50) = 'Engineering';
DECLARE @asOfDate DATE = '2026-12-31';

SELECT
    first_name,
    salary,
    hire_date,
    DATEDIFF(day, hire_date, @asOfDate) AS days_at_date
FROM employees
WHERE department = @dept
  AND salary > @minSalary
ORDER BY salary DESC;
```

*Translation:* `@minSalary`, `@dept`, `@asOfDate` substituted before execution.

---

### 26. System variables (NEW v10.1)

```sql
SELECT
    @@VERSION AS server_version,
    @@SERVERNAME AS server_name;
```

*Result:* Returns simulator version + builder credit.

---

### 27. sys.tables / INFORMATION_SCHEMA queries

```sql
-- List all user tables
SELECT TABLE_NAME, TABLE_TYPE
FROM INFORMATION_SCHEMA.TABLES
ORDER BY TABLE_NAME;

-- All columns of all tables
SELECT TABLE_NAME, COLUMN_NAME, DATA_TYPE, IS_NULLABLE
FROM INFORMATION_SCHEMA.COLUMNS
ORDER BY TABLE_NAME, ORDINAL_POSITION;

-- sys.tables direct
SELECT name AS table_name, object_id FROM sys.tables;
```

*Translation:* Mapped to `sqlite_master` + `pragma_table_info`.

---

### 28. GO batch separator

```sql
CREATE TABLE temp_log (
    id INT IDENTITY(1,1) PRIMARY KEY,
    msg TEXT,
    logged_at DATETIME DEFAULT GETDATE()
);
GO

INSERT INTO temp_log (msg) VALUES ('Batch 1 complete');
INSERT INTO temp_log (msg) VALUES ('Batch 2 complete');
INSERT INTO temp_log (msg) VALUES ('Batch 3 complete');
GO

SELECT * FROM temp_log;
GO

PRINT 'Done logging.';
```

*Translation:* `GO` splits into 3 batches; `IDENTITY(1,1)` dropped; `PRINT` → result row.

---

### 29. CREATE INDEX with EXPLAIN

```sql
-- Create an index
CREATE INDEX idx_employees_dept_salary
ON employees(department, salary DESC);
GO

-- See the plan use it
EXPLAIN QUERY PLAN
SELECT * FROM employees
WHERE department = 'Engineering'
ORDER BY salary DESC;
```

*Tip:* Compare the plan with/without the index — the simulator highlights `✓ SEARCH` (uses index) vs `⚠ SCAN` (full scan).

---

### 30. Transaction with ROLLBACK

```sql
BEGIN TRANSACTION;

UPDATE employees
SET salary = salary * 1.50
WHERE department = 'Sales';

-- Check the damage before committing
SELECT department, COUNT(*), AVG(salary) AS new_avg
FROM employees
WHERE department = 'Sales'
GROUP BY department;

-- Don't commit — roll back!
ROLLBACK TRANSACTION;

-- Verify rollback worked
SELECT department, AVG(salary) AS restored_avg
FROM employees
WHERE department = 'Sales'
GROUP BY department;
```

---

### 31. Recursive CTE — Generate a date series

```sql
WITH RECURSIVE date_series(d, n) AS (
    SELECT '2026-01-01', 1
    UNION ALL
    SELECT date(d, '+1 day'), n + 1
    FROM date_series
    WHERE n < 30
)
SELECT
    d AS date,
    STRFTIME('%w', d) AS day_of_week,
    CASE STRFTIME('%w', d)
        WHEN '0' THEN 'Sunday'
        WHEN '6' THEN 'Saturday'
        ELSE 'Weekday'
    END AS day_type
FROM date_series;
```

---

### 32. Complete reporting query (combines 10+ features)

```sql
-- Quarterly Sales Report by Region and Category
-- Builder: Adewale Samson Adeagbo · MS SQL Server Simulator v10
DECLARE @minRevenue INT = 100000;

WITH quarterly AS (
    SELECT
        region,
        category,
        YEAR(order_date) AS year,
        ((MONTH(order_date) - 1) / 3) + 1 AS quarter,
        COUNT(*) AS order_count,
        SUM(total_amount) AS revenue,
        AVG(total_amount) AS avg_order,
        SUM(quantity) AS units_sold
    FROM orders
    WHERE status != 'Cancelled'
    GROUP BY region, category, YEAR(order_date), ((MONTH(order_date) - 1) / 3) + 1
)
SELECT TOP 20
    region,
    category,
    year,
    'Q' + CONVERT(VARCHAR, quarter) AS quarter,
    order_count,
    FORMAT(revenue, 'C') AS revenue,
    ROUND(avg_order, 0) AS avg_order_value,
    units_sold,
    RANK() OVER (PARTITION BY region ORDER BY revenue DESC) AS region_rank,
    IIF(revenue >= @minRevenue, '✅ Hit Target', '❌ Below Target') AS status
FROM quarterly
WHERE revenue > 0
ORDER BY revenue DESC;
GO

PRINT 'Report complete. Built by Adewale Samson Adeagbo.';
```

*Translations used:* `TOP`, `IIF`, `YEAR`, `MONTH`, `CONVERT`, `FORMAT`, `+` concat, `DECLARE/@vars`, `RANK() OVER`, `GO`, `PRINT`.

---

## 🎯 Bonus Examples

### About the Builder

```sql
SELECT
    'Adewale Samson Adeagbo' AS Name,
    'Data Scientist · EdTech Builder · AI-Augmented Solutions Developer' AS Role,
    'HMG Concepts (est. 2015)' AS Brand,
    'Lagos, Nigeria' AS Location,
    15 AS YearsTeaching,
    12 AS LiveProjects,
    'https://cssadewale.pages.dev' AS Portfolio,
    'https://linkedin.com/in/adewalesamsonadeagbo' AS LinkedIn,
    'https://github.com/cssadewale' AS GitHub,
    '+234 810 086 6322' AS WhatsApp;
```

### HMG Concepts Subsidiaries

```sql
SELECT * FROM (VALUES
    ('HMG Academy', 'Virtual learning institution', 'hmgacademy.pages.dev'),
    ('HMG Technologies', 'EdTech and data solutions', 'built-in-house'),
    ('HMG Media', 'Educational content and community', 'hmgconcepts.pages.dev')
) AS subsidiaries(name, mission, url);
```

---

## 🛠 Where to Go Next

- **Press F1** in the app for the searchable feature help
- **Tools → Activity Monitor** to see your queries logged in real time
- **Tools → SQL Server Profiler** for the full event trace
- **Tools → Query Store** to see HOT/WARM/COLD heat-coded patterns
- **Tools → Programmability** to create Stored Procedures, Views, and Triggers
- **Tools → Backup & Restore** to round-trip your work as a `.bak` file
- **Help → T-SQL Translation Map** for the complete 65+ rule reference

---

*Built with 💚 by [**Adewale Samson Adeagbo**](https://cssadewale.pages.dev) · HMG Concepts · 2026 · MIT Licence*
