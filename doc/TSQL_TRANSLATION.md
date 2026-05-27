# T-SQL ↔ SQLite Translation Reference

**Built by: Adewale Samson Adeagbo · MS SQL Server Simulator v10 Enterprise Edition · 2026**

The simulator includes a 30+ rule translation engine that auto-converts Microsoft T-SQL syntax to SQLite at execution time. This document explains every rule.

---

## 🎛 Translation Modes

The status bar shows a clickable badge:

| Badge | Mode | Behaviour |
|---|---|---|
| `T-SQL: AUTO` (default) | Translate everything, log changes to Messages | Recommended for most users |
| `T-SQL: STRICT` | Translate, but flag every substitution prominently | Good for learning the differences |
| `T-SQL: OFF` | Pass query straight to SQLite | Use to see raw error messages from T-SQL syntax |

**Click the badge to cycle modes.** Persisted in localStorage.

---

## 📋 Complete Rule Reference

### Query Structure

| T-SQL | SQLite | Notes |
|---|---|---|
| `SELECT TOP 10 * FROM t` | `SELECT * FROM t LIMIT 10` | Auto-appends `LIMIT` if not already present |
| `OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY` | `LIMIT 10 OFFSET 20` | Modern T-SQL pagination |
| `GO` (own line) | Splits into separate batches | Each batch executes independently |

### Date / Time Functions

| T-SQL | SQLite | Notes |
|---|---|---|
| `GETDATE()` | `datetime('now','localtime')` | Local server time |
| `GETUTCDATE()` | `datetime('now')` | UTC time |
| `SYSDATETIME()` | `datetime('now','localtime')` | Modern variant |
| `CURRENT_TIMESTAMP` | `CURRENT_TIMESTAMP` | Native in both |
| `YEAR(d)` | `CAST(STRFTIME('%Y',d) AS INTEGER)` | Returns INTEGER |
| `MONTH(d)` | `CAST(STRFTIME('%m',d) AS INTEGER)` | Returns INTEGER |
| `DAY(d)` | `CAST(STRFTIME('%d',d) AS INTEGER)` | Returns INTEGER |
| `DATEPART(year, d)` | `CAST(STRFTIME('%Y',d) AS INTEGER)` | Accepts year/month/day/hour/minute/second |
| `DATEDIFF(day, a, b)` | `CAST((julianday(b)-julianday(a))*1 AS INTEGER)` | Other units: hour ×24, minute ×1440, second ×86400 |
| `DATEADD(day, 7, d)` | `datetime(d, '+7 days')` | Negative N also supported |

### NULL Handling

| T-SQL | SQLite | Notes |
|---|---|---|
| `ISNULL(x, 'N/A')` | `IFNULL(x, 'N/A')` | NULL default value |
| `COALESCE(a, b, c)` | `COALESCE(a, b, c)` | Native in both |
| `NULLIF(a, b)` | `NULLIF(a, b)` | Native in both |

### Conditional Logic

| T-SQL | SQLite | Notes |
|---|---|---|
| `IIF(cond, a, b)` | `(CASE WHEN cond THEN a ELSE b END)` | Recursive (nested IIFs supported) |
| `CHOOSE(2, 'A', 'B', 'C')` | `(CASE WHEN 2=1 THEN 'A' WHEN 2=2 THEN 'B' WHEN 2=3 THEN 'C' END)` | Index-based pick |
| `CASE WHEN ... THEN ... END` | `CASE WHEN ... THEN ... END` | Native in both |

### String Functions

| T-SQL | SQLite | Notes |
|---|---|---|
| `LEN(s)` | `LENGTH(s)` | String length |
| `CHARINDEX('@', email)` | `INSTR(email, '@')` | Args flipped automatically |
| `SUBSTRING(s, 2, 5)` | `SUBSTRING(s, 2, 5)` | Native in SQLite |
| `STUFF(s, start, len, ins)` | `(SUBSTR(s,1,start-1) \|\| ins \|\| SUBSTR(s,start+len))` | String replace |
| `CONCAT(a, b, c)` | `CONCAT(a, b, c)` or `a \|\| b \|\| c` | Both supported |
| `REPLACE(s, old, new)` | `REPLACE(s, old, new)` | Native in both |
| `UPPER(s)` / `LOWER(s)` | `UPPER(s)` / `LOWER(s)` | Native in both |

### Type Conversion

| T-SQL | SQLite | Notes |
|---|---|---|
| `CAST(x AS INTEGER)` | `CAST(x AS INTEGER)` | Native in both |
| `CONVERT(INTEGER, x)` | `CAST(x AS INTEGER)` | Style parameter dropped |
| `TRY_CAST(x AS INT)` | `CAST(x AS INT)` | SQLite returns NULL on failure |
| `TRY_CONVERT(INT, x)` | `CAST(x AS INT)` | Same |

### Identity / UUID

| T-SQL | SQLite | Notes |
|---|---|---|
| `NEWID()` | `lower(hex(randomblob(16)))` | UUID-like string |
| `IDENTITY(1,1)` | Dropped — use `INTEGER PRIMARY KEY` | SQLite uses rowid |

### Identifiers

| T-SQL | SQLite | Notes |
|---|---|---|
| `[bracket]` identifiers | `"quoted"` identifiers | Outside string literals only |
| `dbo.table` | `table` | Schema prefix dropped |

### DDL Types

| T-SQL | SQLite | Notes |
|---|---|---|
| `NVARCHAR(MAX)`, `VARCHAR(255)`, `NCHAR(10)` | `TEXT` | SQLite is type-flexible |
| `BIT` | `INTEGER` | 0/1 values |
| `MONEY`, `SMALLMONEY` | `REAL` | Floating point |
| `DATETIME2`, `DATETIMEOFFSET` | `DATETIME` | All collapse to TEXT internally |
| `UNIQUEIDENTIFIER` | `TEXT` | Store UUID as string |
| `INT IDENTITY(1,1) PRIMARY KEY` | `INTEGER PRIMARY KEY` | rowid auto-increments |

### Variables and Batches

| T-SQL | SQLite | Notes |
|---|---|---|
| `DECLARE @x INT = 10` | JS variable stored | Type ignored; value remembered |
| `DECLARE @s VARCHAR(50)` | JS variable stored as null | Value assigned later |
| `SET @x = 20` | JS variable updated | |
| `@x` (reference anywhere) | Literal substituted | Strings auto-quoted, numbers passed through |
| `PRINT 'Hello'` | `SELECT 'Hello' AS [PRINT]` | Shows as result row |
| `GO` (batch separator) | Batches split and run sequentially | Standard SSMS pattern |

### System Catalogs

| T-SQL | SQLite | Notes |
|---|---|---|
| `sys.tables` | `(SELECT name, 'U' AS type, rowid AS object_id FROM sqlite_master WHERE type='table')` | Catalog subquery |
| `sys.columns` | `(SELECT m.name AS table_name, p.name AS column_name, p.type AS data_type FROM sqlite_master m, pragma_table_info(m.name) p WHERE m.type='table')` | Joined |
| `sys.databases` | `(SELECT 'master' AS name, 1 AS database_id)` | Single DB |
| `INFORMATION_SCHEMA.TABLES` | Mapped to sqlite_master with TABLE_CATALOG/SCHEMA columns | ANSI standard |
| `INFORMATION_SCHEMA.COLUMNS` | Mapped to pragma_table_info join | ANSI standard |
| `sp_help 'tablename'` | `PRAGMA table_info('tablename')` | Schema introspection |
| `sp_columns 'tablename'` | `PRAGMA table_info('tablename')` | Same |
| `sp_tables` | `SELECT name FROM sqlite_master WHERE type='table'` | Table list |

---

## 💡 Worked Examples

### Example 1 — Authentic T-SQL using many translations

```sql
DECLARE @minSalary INT = 600000;
DECLARE @maxDate DATE = '2026-12-31';

SELECT TOP 10
    [first_name],
    ISNULL([city], 'Unknown') AS city,
    LEN([first_name]) AS name_length,
    YEAR(hire_date) AS hire_year,
    DATEDIFF(day, hire_date, GETDATE()) AS days_employed,
    IIF(salary > 800000, 'High',
        IIF(salary > 500000, 'Mid', 'Low')) AS band,
    CONVERT(VARCHAR, salary) AS salary_text
FROM dbo.employees
WHERE salary > @minSalary
  AND hire_date <= @maxDate
ORDER BY salary DESC;
GO

PRINT 'Query complete.';
```

**What runs under the hood:**

```sql
-- declared @minSalary = 600000
-- declared @maxDate = 2026-12-31

SELECT 
    "first_name",
    IFNULL("city", 'Unknown') AS city,
    LENGTH("first_name") AS name_length,
    CAST(STRFTIME('%Y', hire_date) AS INTEGER) AS hire_year,
    CAST((julianday(datetime('now','localtime')) - julianday(hire_date)) * 1 AS INTEGER) AS days_employed,
    (CASE WHEN salary > 800000 THEN 'High'
        ELSE (CASE WHEN salary > 500000 THEN 'Mid' ELSE 'Low' END) END) AS band,
    CAST(salary AS VARCHAR) AS salary_text
FROM employees
WHERE salary > 600000
  AND hire_date <= '2026-12-31'
ORDER BY salary DESC LIMIT 10;
-- (GO batch separator splits here)
SELECT 'Query complete.' AS [PRINT];
```

### Example 2 — Querying system catalogs

```sql
-- T-SQL
SELECT TOP 5 TABLE_NAME FROM INFORMATION_SCHEMA.TABLES;

-- Auto-translates to:
SELECT TABLE_NAME FROM (
  SELECT 'master' AS TABLE_CATALOG, 'dbo' AS TABLE_SCHEMA,
         name AS TABLE_NAME, 'BASE TABLE' AS TABLE_TYPE
  FROM sqlite_master WHERE type='table'
) LIMIT 5;
```

### Example 3 — DDL with T-SQL types

```sql
-- T-SQL
CREATE TABLE [Customer] (
    CustomerID INT IDENTITY(1,1) PRIMARY KEY,
    Name NVARCHAR(255) NOT NULL,
    IsActive BIT DEFAULT 1,
    Balance MONEY DEFAULT 0,
    CreatedAt DATETIME2 DEFAULT GETDATE(),
    PublicID UNIQUEIDENTIFIER DEFAULT NEWID()
);

-- Auto-translates to:
CREATE TABLE "Customer" (
    CustomerID INT  PRIMARY KEY,
    Name TEXT NOT NULL,
    IsActive INTEGER DEFAULT 1,
    Balance REAL DEFAULT 0,
    CreatedAt DATETIME DEFAULT datetime('now','localtime'),
    PublicID TEXT DEFAULT lower(hex(randomblob(16)))
);
```

---

## ⚠ Known Limitations

These constructs are NOT translated (will error):

- `MERGE` statements (use `INSERT ... ON CONFLICT` in SQLite)
- `TRY ... CATCH` blocks (SQLite has no procedural error handling in queries)
- `THROW` / `RAISERROR` (no equivalent)
- `CURSOR` declarations (SQLite uses statements only)
- Window function `FRAME` clauses with `RANGE` (`ROWS` works)
- Temp tables `#temp`, `##temp` (use regular tables prefixed with `temp_`)
- Table variables `@tableVar` (use regular tables)
- `FOR JSON` / `FOR XML` clauses (no equivalent)
- Linked Server `OPENQUERY` / `OPENROWSET` (single DB only)
- `EXECUTE AS` impersonation (no security enforcement)
- Full-text search `CONTAINS()`, `FREETEXT()` (use `LIKE`)

For unsupported syntax, switch to `T-SQL: OFF` to see SQLite's native error.

---

## 🤝 Contributing a New Rule

Want to add a translation rule? Edit `index.html` directly. In the V10 script block, locate the `TSQL_RULES` array and add an entry:

```javascript
{
  name: 'MyNewRule',
  test: /\bMY_FUNC\s*\(/i,  // detect with regex
  apply: s => s.replace(/\bMY_FUNC\s*\(/gi, 'SQLITE_EQUIVALENT(')
}
```

Then add a row to this document and submit a PR.

---

*Built with 💚 by [Adewale Samson Adeagbo](https://cssadewale.pages.dev) · HMG Concepts · 2026*
