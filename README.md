<div align="center">

# 🗄️ MS SQL Server Simulator
## v10 Enterprise Edition

### *A free, offline-capable, browser-based SQL Server Management Studio (SSMS) experience with enterprise features.*

**No backend. No installation. No AI API. No subscription. Single HTML file. Built by [Adewale Samson Adeagbo](https://cssadewale.pages.dev) on an Android tablet in Lagos, Nigeria.**

[![Version](https://img.shields.io/badge/version-v10.0_Enterprise-0078d4?style=for-the-badge)](#-version-history)
[![SQLite WASM](https://img.shields.io/badge/Engine-SQLite_WASM-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://sql-wasm.js.org/)
[![T-SQL](https://img.shields.io/badge/T--SQL-Auto_Translated-107c10?style=for-the-badge)](#-t-sql-auto-translation-engine)
[![Enterprise](https://img.shields.io/badge/Enterprise-Activity_Monitor_·_Profiler_·_Procedures_·_Always_On-107c10?style=for-the-badge)](#-v10-enterprise-features-new)
[![No AI API](https://img.shields.io/badge/AI_API-Not_Used-blue?style=for-the-badge)](#)
[![Offline Ready](https://img.shields.io/badge/Offline-Ready-00e5a0?style=for-the-badge)](#)
[![Mobile First](https://img.shields.io/badge/Mobile-Android_Optimised-f0b429?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![Single File](https://img.shields.io/badge/Single_File-~360KB_HTML-c678dd?style=for-the-badge)](index.html)

**Mimics the enterprise functionality of Microsoft SQL Server: SSMS layout, Object Explorer, Activity Monitor, SQL Server Profiler, Query Store, Stored Procedures, Views, Triggers, Security/Logins/Roles, Backup/Restore, Maintenance Plans, Always On dashboards, plus a 30+ rule T-SQL translation engine.**

[🚀 Live Demo](https://cssadewale.github.io/ms-sql-server-simulator/) · [📖 Features](#-features) · [⌨ Shortcuts](#%EF%B8%8F-keyboard-shortcuts) · [🚀 Deploy](#-deployment-guide) · [👤 Meet the Builder](#-about-the-builder)

</div>

---

## 📌 Table of Contents

1. [Overview](#-overview)
2. [Why This Project Exists](#-why-this-project-exists)
3. [What's New in v10 Enterprise Edition](#-whats-new-in-v10-enterprise-edition)
4. [SSMS Look-and-Feel Mapping](#-ssms-look-and-feel-mapping)
5. [Key Highlights](#-key-highlights)
6. [Technology Stack](#-technology-stack)
7. [V10 Enterprise Features (NEW)](#-v10-enterprise-features-new)
8. [T-SQL Auto-Translation Engine](#-t-sql-auto-translation-engine)
9. [All Features (80+, fully documented)](#-features)
10. [Quick Start](#-quick-start)
11. [Sample Databases](#-sample-databases)
12. [Keyboard Shortcuts](#%EF%B8%8F-keyboard-shortcuts)
13. [Repository Structure](#-repository-structure)
14. [Deployment Guide](#-deployment-guide)
15. [Continuous Deployment](#-continuous-deployment-github-actions)
16. [Architecture Notes](#-architecture-notes)
17. [Version History](#-version-history)
18. [About the Builder](#-about-the-builder)
19. [License](#-license)

---

## 🧭 Overview

**MS SQL Server Simulator v10 Enterprise Edition** is a single-file web application that emulates the **look, layout, and enterprise functionality** of Microsoft SQL Server Management Studio (SSMS) directly in your browser. It is powered by [sql.js](https://sql-wasm.js.org/) — a WebAssembly build of SQLite — providing a real, fully functional SQL engine running entirely client-side, with a comprehensive **T-SQL → SQLite translation layer** so you can write authentic Microsoft T-SQL syntax (`SELECT TOP`, `GETDATE()`, `ISNULL`, `IIF`, `DATEPART`, `sys.tables`, `INFORMATION_SCHEMA`, `DECLARE @var`, `GO` batches, and more) and have it just work.

The application reproduces the full SSMS user experience:

- **Title bar → Menu bar (File / Edit / View / Query / Tools / Window / Help)**
- **Standard toolbar** with grouped icon buttons and the familiar **green ▶ Execute** button
- **Object Explorer tree** on the left (Server → Databases → Tables → Columns / Keys / Indexes / Programmability / Security / Always On)
- **Tabbed query windows** (each tab represents a `SQLQuery#.sql` document)
- **Results / Messages / Chart / Statistics / ER Diagram / Execution Plan / Hints** tabs
- **Builder strip + blue status bar** at the bottom with connection state, server, user, database, T-SQL translation badge, line/column, row count, elapsed time

Everything runs in the browser. There is **no server, no installation, no npm, no build step, no Docker, no AI API call, and no per-query cost**. The entire application is one ~360 KB HTML file you can email, host on any static file server, or open from your file system.

> **Built on an Android tablet in Lagos, Nigeria** by Adewale Samson Adeagbo — no laptop, no local IDE. The entire application is a single HTML file you can edit in any text editor, including mobile editors like [Acode](https://acode.app/).

---

## 💡 Why This Project Exists

Real Microsoft SQL Server requires a Windows machine (or Docker/Linux container for SQL Server on Linux), a multi-gigabyte SSMS install, and an ODBC/TDS stack. For:

- **Tablet-only learners** (the author's daily reality)
- **Students** with limited disk space or no Windows access
- **Educators** in low-resource environments who need to teach T-SQL
- **Anyone wanting to practise SSMS workflows** without setting up a server
- **Developers** wanting a quick reference for T-SQL syntax mapping

…that barrier is real. **MS SQL Server Simulator v10** removes it. Open one HTML file → write authentic T-SQL → see results — with the **exact visual language and enterprise toolset SSMS users expect**, so the muscle memory transfers when you eventually do open the real SSMS.

It is also a personal demonstration of the **AI-Augmented Solutions Developer** approach: combining freely available tools (WebAssembly, CDN libraries, GitHub Pages, Cloudflare Pages), AI assistance for accelerated development, and deep domain knowledge in education and data — to produce production-grade enterprise software from any device, anywhere, for free, forever.

---

## ✨ What's New in v10 Enterprise Edition

v10 transforms the simulator from an SSMS-shell into a full enterprise workbench:

| Category | What's New | Where |
|---|---|---|
| **T-SQL Translation** | 30+ T-SQL constructs auto-translated to SQLite at execution time (`TOP`, `GETDATE`, `ISNULL`, `IIF`, `DATEPART`, `DATEDIFF`, `DATEADD`, `NEWID`, `[brackets]`, `IDENTITY`, `NVARCHAR(MAX)`, `MONEY`, `BIT`, `TRY_CAST`, `OFFSET/FETCH`, `sys.tables`, `INFORMATION_SCHEMA`, `sp_help`, `dbo.` prefix, etc.) | Status bar badge: `T-SQL: AUTO` |
| **Activity Monitor** | Real-time dashboard: total queries, avg duration, errors, uptime, table count, active connections, sparkline of recent execution times. Auto-refresh every 2 sec. | Tools menu / Ctrl+Alt+A |
| **SQL Server Profiler** | Trace table of every executed query (last 500): time, SPID, event class, SQL, duration, rows. Pause / clear / export as CSV. | Tools menu |
| **Query Store** | Aggregates queries by normalized pattern. Heat-coded by avg duration (🔥 HOT / 🟧 WARM / 🟦 COLD). | Tools menu |
| **Performance Dashboard** | Line chart of duration over time, p95 / max statistics, slowest-10 list. | Tools menu |
| **Programmability (Procs/Views/Triggers)** | Full CRUD for Stored Procedures (JS parameter substitution), Views (real SQLite VIEW), Triggers (real SQLite TRIGGER). | Tools menu + Object Explorer |
| **Security & Logins** | Manage simulated SQL Logins, Windows Logins, and 9 server roles (sysadmin, db_datareader, db_datawriter, public, etc.). | Tools menu |
| **Backup & Restore Wizard** | Multi-step wizard. Full database backup as `.bak` file (binary SQLite). Round-trips schema, data, indexes, views, triggers. | Tools menu |
| **Maintenance Plan Wizard** | 7 built-in tasks: Reorganize Indexes, Rebuild Indexes, Update Statistics (ANALYZE), Check Integrity, Vacuum/Shrink, Cleanup History, Full Backup. | Tools menu |
| **Import / Export Wizard** | Single hub for all import sources (CSV, JSON, SQL, SQLite, .bak, Excel-via-CSV) and 8 export targets. | Tools menu |
| **Database Diagrams** | SSMS-style table relationship diagram in dedicated modal. | Tools menu |
| **Always On Dashboard** | Visual HA cluster simulation: Primary + 3 Secondaries with sync state, lag, availability databases, listener config. | Tools menu |
| **Registered Servers** | Tree of saved server connections (like SSMS panel). | View menu |
| **Solution Explorer** | Treats saved queries as a project. | View menu |
| **Template Explorer** | SSMS-style hierarchical template tree with 20+ templates. | View menu |
| **GO Batch Separator** | Use `GO` on its own line to split scripts into multiple batches. | Editor |
| **DECLARE / SET / @vars** | Write `DECLARE @x INT = 10; SET @x = 20;` — references substituted automatically before execution. | Editor |
| **sys.tables / INFORMATION_SCHEMA** | Query system catalogs (translated to SQLite equivalents). | Editor |
| **Welcome Splash** | One-time splash on first load introducing the builder. | First load |
| **Builder Strip** | Permanent blue strip above status bar with builder name, role, and quick links. | Always visible |
| **JSON Import** | Imports JSON array of objects as a new table. | File menu |
| **Console Signature** | Browser console shows builder credit on startup. | F12 console |
| **Builder Identity** | About-the-Builder node in Object Explorer · status-bar builder credit · attribution in every export · pre-seeded new query header · Help menu "Meet the Builder" link | Throughout |

---

## 🖥 SSMS Look-and-Feel Mapping

| Real SSMS Element | This Simulator | Notes |
|---|---|---|
| Title bar with database name | ✅ Top bar with file + database + builder link | Shows active `SQLQuery#.sql (master)` |
| Menu bar (File · Edit · View · Query · Tools · Window · Help) | ✅ Full 7-menu bar | Identical menu names; near-identical items |
| Standard toolbar with grouped icons | ✅ Grouped toolbar | New / Open / Save / DB selector / ▶ Execute / ■ Stop / ✓ Parse / 🔍 Plan / Format |
| Green ▶ Execute button | ✅ Always visible, F5 shortcut | Identical green colour, identical position |
| Database selector dropdown | ✅ Database dropdown | Defaults to `master` |
| Object Explorer tree | ✅ Full tree + Programmability + Security + Always On | Server → Databases → master → Tables → table → Columns / Keys / Indexes / Programmability / Security |
| Right-click table → Script as / Design / Rename / DROP / SELECT TOP 1000 | ✅ Context menu | Right-click any table |
| Tabbed query documents | ✅ Tab bar | `SQLQuery1.sql`, `SQLQuery2.sql`, modified dot, close × |
| Results pane with Results / Messages tabs | ✅ Seven tabs | Results · Messages · Chart · Statistics · ER Diagram · Exec Plan · Hints |
| **Activity Monitor** | ✅ Real-time KPI dashboard | Tools menu / Ctrl+Alt+A |
| **SQL Server Profiler** | ✅ Trace table of 500 events | Tools menu |
| **Query Store** | ✅ Heat-coded pattern aggregation | Tools menu |
| **Stored Procedures / Views / Triggers** | ✅ Full CRUD + execution | Tools menu + Object Explorer |
| **Security folder (Logins, Roles)** | ✅ Full manage UI | Tools menu + Object Explorer |
| **Backup / Restore** | ✅ Multi-step wizard | Tools menu |
| **Maintenance Plan** | ✅ 7-task wizard | Tools menu |
| **Always On Availability Groups** | ✅ Visual dashboard | Tools menu (simulated) |
| Blue status bar | ✅ Bottom blue bar + T-SQL badge | Connection · Server · User · Database · Ln/Col · Rows · Time |
| IntelliSense (Ctrl+Space) | ✅ Autocomplete | Keywords + functions + types + table names |
| Find & Replace (Ctrl+H) | ✅ Find bar | Match count, next/prev, replace, replace-all |
| Execution Plan (Ctrl+L) | ✅ EXPLAIN QUERY PLAN | Highlights ✓ SEARCH vs ⚠ SCAN |
| Parse / Validate (Ctrl+F5) | ✅ Syntax check | Without executing side effects |
| Command palette (Ctrl+P) | ✅ Searchable command list | Every action |
| Dark / Light themes | ✅ Both themes | Authentic SSMS palettes |

---

## ✨ Key Highlights

| | Feature | Detail |
|---|---|---|
| 🗂 | **Single file** | The entire application is one `~360 KB` HTML file |
| 🔌 | **Zero installation** | Open in browser — no npm, no build, no server, no Docker |
| 📶 | **Offline-ready** | Works without internet after first page load (CDN libs cached) |
| 🆓 | **100% free** | No AI API, no backend, no subscription, no usage limits, no cloud bills |
| 📱 | **Mobile / tablet optimised** | Tested on Android tablets and Chrome mobile |
| 🗄️ | **13 sample databases** | Real Nigerian business and education data, one-click load, fully JOINable |
| 🛠 | **80+ features** | All inherited from QueryForge v8 + v9 SSMS shell + v10 enterprise modules |
| 🏢 | **Enterprise modules** | Activity Monitor, Profiler, Query Store, Stored Procs/Views/Triggers, Security, Backup/Restore, Maintenance, Always On |
| 🔄 | **T-SQL Translation** | 30+ rules auto-translate T-SQL to SQLite (TOP, GETDATE, ISNULL, IIF, DATEPART, sys.tables, etc.) |
| 👤 | **Builder identity embedded** | Splash, strip, status bar, Object Explorer, exports, console — 7 places |
| 🌓 | **Authentic SSMS dark theme** | Plus a clean light mode |
| 💾 | **Backup / Restore** | Round-trip the entire workspace as a `.bak` file |
| 📊 | **6 chart types + ER diagram** | Bar · Line · Pie · Doughnut · Polar · Scatter + auto-drawn ERD |
| 🧠 | **12 rule-based SQL hints** | Deterministic checks (no AI). Some hints offer click-to-apply fixes |

---

## 🛠 Technology Stack

All external libraries are loaded from [cdnjs.cloudflare.com](https://cdnjs.cloudflare.com) — free, open-source, and CDN-cached for offline use after first load. **There is no npm, no bundler, and no framework.**

| Library | Version | Purpose |
|---|---|---|
| [sql.js](https://github.com/sql-js/sql.js) | 1.10.2 | SQLite compiled to WebAssembly — the SQL engine |
| [PapaParse](https://www.papaparse.com/) | 5.4.1 | CSV parsing with auto type detection |
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Data visualisation — 6 chart types, PNG export |
| Google Fonts | — | Segoe UI · JetBrains Mono · Inter |

**Stack:** Pure HTML5 + CSS3 + Vanilla JavaScript. No React. No Vue. No TypeScript. No Tailwind. No Node.js. No backend.

---

## 🏢 V10 Enterprise Features (NEW)

### 1. Activity Monitor

**Where:** Tools menu → Activity Monitor · Keyboard: `Ctrl+Alt+A` · Object Explorer node

**What it shows:**
- **Total Queries** — Count with sparkline of recent execution times
- **Avg Query Time** — Last 20 queries, color-coded
- **Total Rows Returned** — Across all queries this session
- **Failed Queries** — Error count (cross-references Profiler)
- **Database Uptime** — hh:mm:ss this session
- **Tables in master** — User table count
- **Active Connections** — Current session info
- **SQL Engine** — sql.js / WASM version
- **Top 10 Recent Queries** — Time, event class, SQL excerpt, duration, rows

**Auto-refresh:** Every 2 seconds while modal is open.

**Why it matters:** Real SSMS Activity Monitor shows the same KPIs — this gives you the muscle memory and visual familiarity. Use it to spot performance regressions, count tables, and audit recent activity.

---

### 2. SQL Server Profiler

**Where:** Tools menu → SQL Server Profiler

**What it captures:** Every executed query (up to 500 most recent events):
- **Time** — Down to milliseconds
- **SPID** — Simulated server process ID
- **Event class** — `SQL:BatchCompleted`, `SQL:StmtCompleted`, `CREATE`, `DROP`, `ALTER`, `INSERT`, `UPDATE`, `DELETE`, `SELECT`, or error
- **SQL text** — First 200 chars
- **Duration** — milliseconds, color-coded
- **Rows** — Returned by SELECT
- **User** — `adewale` (builder)
- **DB** — `master`

**Controls:** Start/Stop recording · Clear all · Export trace as CSV (with builder attribution header)

**Why it matters:** Like real SQL Server Profiler / Extended Events. Track what your app is doing, find slow queries, audit DDL changes, debug errors.

---

### 3. Query Store

**Where:** Tools menu → Query Store

**What it does:** Aggregates queries by normalized SQL pattern (whitespace and case stripped). For each pattern:
- **Execution count**
- **Total time**
- **Average time**
- **Max time**
- **Heat classification** — 🔥 HOT (>100ms avg) · 🟧 WARM (>30ms avg) · 🟦 COLD (<30ms avg)

Sorted by total time. Top 20 shown.

**Why it matters:** SQL Server's Query Store identifies your most-expensive query patterns. This simulator brings the same insight to your local sessions.

---

### 4. Performance Dashboard

**Where:** Tools menu → Performance Dashboard

**What it shows:**
- 4 KPI cards: queries logged, average ms, 95th percentile ms, slowest ms
- **Line chart** of duration over the last 50 queries
- **Slowest 10 queries** table

**Why it matters:** Visual performance analysis. Spot trends (queries getting slower over time), outliers (one runaway query), and the long tail.

---

### 5. Programmability (Stored Procedures · Views · Triggers)

**Where:** Tools menu → Programmability · Object Explorer → Programmability folder

**Three tabs:**

**📜 Stored Procedures** — Click ➕ Create → enter name, parameters (e.g. `@dept, @minSalary`), body (SQL using `@params`). Execute with ▶ Exec → prompted for each parameter value → body runs with `@params` substituted as quoted strings or numbers.

**👁 Views** — Click ➕ Create → enter name, SELECT query → real SQLite `CREATE VIEW` runs. View appears in Object Explorer; click ▶ Query to `SELECT * FROM viewname`.

**⚡ Triggers** — Click ➕ Create → enter name, table, event (`AFTER INSERT` / `AFTER UPDATE` / `AFTER DELETE`), body → real SQLite `CREATE TRIGGER` runs. Trigger fires on the specified DML.

All three persist in `localStorage` between sessions.

**Why it matters:** Real-world SQL development includes stored procedures and triggers. This simulator lets you practise the patterns even though SQLite-WASM doesn't have native procedure support.

---

### 6. Security & Logins

**Where:** Tools menu → Security & Logins · Object Explorer → Security node

**Manage:**
- **SQL Logins** (`sa`, `adewale`, `app_reader`, `app_writer`)
- **Windows Logins** (`BUILTIN\Administrators`)
- **Roles** (`sysadmin`, `serveradmin`, `securityadmin`, `processadmin`, `setupadmin`, `bulkadmin`, `diskadmin`, `dbcreator`, `db_datareader`, `db_datawriter`, `public`)

**Actions:**
- Add new login (specify name, role)
- Enable / Disable any login
- Delete (except `sa` and `adewale` builder account)

**Why it matters:** Practise SSMS security workflows. Understand the role hierarchy. The builder account `adewale` is pre-configured as sysadmin.

> **Note:** These are simulated — SQLite WASM has no user/role enforcement. For educational visualisation only.

---

### 7. Backup & Restore Wizard

**Where:** Tools menu → Backup & Restore Wizard

**4-step wizard:**
1. **Backup Type** — Full Backup (only supported), Differential and Transaction Log shown but disabled
2. **Source Database** — `master`
3. **Destination** — Downloads as `master_backup_YYYY-MM-DDTHH-MM-SS.bak`
4. **Verification** — Tickbox for integrity check

Click **💾 Run Full Backup** → file downloads. The `.bak` is a SQLite binary that round-trips perfectly.

Click **↶ Restore from .bak** → file picker → confirmation → replaces current database.

**Why it matters:** The most common SQL DBA task. The `.bak` files can be exchanged between users, archived, or restored to a different device.

---

### 8. Maintenance Plan Wizard

**Where:** Tools menu → Maintenance Plan Wizard

**7 built-in tasks:**

| Task | Underlying SQL |
|---|---|
| 🔄 Reorganize Indexes | `REINDEX;` |
| 🏗 Rebuild Indexes | `REINDEX;` |
| 📊 Update Statistics | `ANALYZE;` |
| ✅ Check Database Integrity | `PRAGMA integrity_check;` |
| 🧹 Shrink/Vacuum Database | `VACUUM;` |
| 📜 Cleanup History | Removes query history >30 days old (JS) |
| 💾 Full Backup | Triggers `exportSqliteDb()` |

**Run modes:**
- **▶** per-task button — runs immediately, shows ✓ green or ✗ red
- **▶ Run Selected** — runs all checked tasks
- **▶▶ Run All** — runs all 7 in sequence

**Why it matters:** Real DBAs schedule these via SQL Agent jobs. This simulator lets you understand each task and its effect.

---

### 9. Import / Export Wizard

**Where:** Tools menu → Import / Export Wizard

**Single hub for all data movement:**

**📥 Import (6 sources):**
- CSV File · JSON File · SQL Script · SQLite DB · .bak Backup · Excel (save as CSV first)

**📤 Export (8 targets):**
- Results → CSV / JSON / HTML / Markdown / SQL INSERTs
- Database → .sqlite
- Schema → DDL .sql
- Full Backup → .bak

All exports include builder attribution headers.

---

### 10. Database Diagrams

**Where:** Tools menu → Database Diagrams

**What it shows:** SSMS-style auto-drawn table relationship diagram via HTML Canvas. Same engine as the ER Diagram tab in Results, but in a dedicated 920×580 modal for printing/screenshots.

---

### 11. Always On Dashboard (Visual)

**Where:** Tools menu → Always On Dashboard · Object Explorer node

**Shows:**
- Availability Group: `AG_HMG_PROD`
- 4 replicas: PRIMARY (read-write), 2 SECONDARIES (read-only, synchronized), 1 RESOLVING (failover scenario)
- Each with sync state, lag in ms
- Availability Databases table
- Listener config (`AGL_HMG_PROD.cssadewale.local:1433`)

**Why it matters:** Real SQL Server Always On dashboards look exactly like this. Educational visualisation for HA/DR concepts.

> **Note:** SQLite is single-node — this is a visual simulation only.

---

### 12. Registered Servers / Solution Explorer / Template Explorer

**Where:** View menu

- **Registered Servers** — Tree of saved server connections (mock demo servers shown)
- **Solution Explorer** — Treats saved queries as project items
- **Template Explorer** — SSMS-style hierarchical template tree with 20+ templates including:
  - SQL Server Templates (Create Database, Create Table, Create View, Create Index, Create Procedure)
  - DML (Basic SELECT, JOIN, CTE, Window Function, INSERT, UPDATE, DELETE)
  - DDL (CREATE / ALTER / DROP)
  - Reporting (Department Report, Sales Report, Customer LTV, Inventory Reorder, Academic Pass Rate)
  - **Builder Examples** (About the Builder Query, HMG Concepts Project List)

---

## 🔄 T-SQL Auto-Translation Engine

**The simulator translates Microsoft T-SQL syntax to SQLite at execution time.** Write authentic T-SQL — the engine handles the difference.

**Status bar badge:** `T-SQL: AUTO` (default) — click to cycle through `AUTO → STRICT → OFF`.

### 30+ Translation Rules

| You Type (T-SQL) | What Runs (SQLite) | Notes |
|---|---|---|
| `SELECT TOP 10 * FROM t` | `SELECT * FROM t LIMIT 10` | Auto-appends LIMIT |
| `GETDATE()` | `datetime('now','localtime')` | Local time |
| `GETUTCDATE()` | `datetime('now')` | UTC |
| `SYSDATETIME()` | `datetime('now','localtime')` | Modern variant |
| `ISNULL(x, 'N/A')` | `IFNULL(x, 'N/A')` | NULL default |
| `LEN(name)` | `LENGTH(name)` | String length |
| `CHARINDEX('@', email)` | `INSTR(email, '@')` | Args flipped automatically |
| `CONVERT(INTEGER, '42')` | `CAST('42' AS INTEGER)` | Type cast |
| `IIF(x > 1, 'A', 'B')` | `(CASE WHEN x > 1 THEN 'A' ELSE 'B' END)` | Recursive IIFs supported |
| `CHOOSE(2, 'A', 'B', 'C')` | `(CASE WHEN 2=1 THEN 'A' WHEN 2=2 THEN 'B' WHEN 2=3 THEN 'C' END)` | Index-based pick |
| `YEAR(hire_date)` | `CAST(STRFTIME('%Y', hire_date) AS INTEGER)` | Same for MONTH, DAY |
| `DATEPART(month, dt)` | `CAST(STRFTIME('%m', dt) AS INTEGER)` | All units mapped |
| `DATEDIFF(day, a, b)` | `CAST((julianday(b)-julianday(a))*1 AS INTEGER)` | Day-level math |
| `DATEADD(day, 7, dt)` | `datetime(dt, '+7 days')` | Add/subtract intervals |
| `NEWID()` | `lower(hex(randomblob(16)))` | UUID-like ID |
| `[bracket] identifiers` | `"quoted" identifiers` | Outside string literals |
| `DECLARE @x INT = 10` | JS variable substitution | `@x` references replaced later |
| `SET @x = 20` | JS variable update | Persisted in session |
| `PRINT 'Hello'` | `SELECT 'Hello' AS [PRINT]` | Shows as result row |
| `GO` batch separator | Each batch executed separately | Standard SSMS pattern |
| `sys.tables` | `sqlite_master` subquery | Catalog view |
| `sys.columns` | `pragma_table_info` join | Column catalog |
| `sys.databases` | Constant table | DB list |
| `INFORMATION_SCHEMA.TABLES` | Mapped to sqlite_master | ANSI standard |
| `INFORMATION_SCHEMA.COLUMNS` | Mapped to pragma_table_info | ANSI standard |
| `sp_help 'tbl'` | `PRAGMA table_info('tbl')` | Schema introspection |
| `sp_tables` | `SELECT name FROM sqlite_master WHERE type='table'` | Table list |
| `dbo.table` | `table` | Schema prefix dropped |
| `NVARCHAR(MAX)` in DDL | `TEXT` | Type-flexible |
| `BIT` column | `INTEGER` | 0/1 |
| `MONEY`, `SMALLMONEY` | `REAL` | Floating point |
| `DATETIME2`, `DATETIMEOFFSET` | `DATETIME` | Date types |
| `UNIQUEIDENTIFIER` | `TEXT` | UUID as string |
| `IDENTITY(1,1)` | Dropped (use `INTEGER PRIMARY KEY`) | SQLite uses rowid |
| `TRY_CAST` / `TRY_CONVERT` | `CAST` | SQLite returns NULL on failure |
| `OFFSET N ROWS FETCH NEXT M ROWS ONLY` | `LIMIT M OFFSET N` | Pagination |
| `STUFF(str, start, len, ins)` | `(SUBSTR(str,1,start-1) \|\| ins \|\| SUBSTR(str,start+len))` | String replace |

When any rule fires, the Messages tab shows `[T-SQL Translation applied: ruleName1, ruleName2, …]` so you know what changed.

**Modes:**
- **AUTO** (default) — translate every supported construct, log to Messages
- **STRICT** — same translation but more prominent logging
- **OFF** — pass query straight to SQLite (will fail on T-SQL syntax — useful for learning the differences)

---

## 🔬 Features

The simulator contains **80+ documented features**, each with an in-app help entry (press <kbd>F1</kbd>). Below is the categorised summary.

### 👤 Meet the Builder (7 touchpoints)

| Where | What |
|---|---|
| **Welcome Splash** | First-load presentation with bio, roles, story, "Don't show again" option |
| **Builder Strip** | Permanent blue bar above status bar with name, role, quick links to Portfolio · LinkedIn · GitHub · WhatsApp · Meet Builder. Hide via View menu. |
| **Status Bar Builder Credit** | Bottom-right: 👤 Adewale Adeagbo — clickable to open bio |
| **Object Explorer Builder Node** | Permanent node at bottom of tree |
| **Help Menu** | "Meet the Builder" as the first item with full bio modal |
| **Title Bar** | "by Adewale Samson Adeagbo 👤" as a clickable link |
| **Console** | Browser console (F12) shows builder credit on startup |
| **New Query Tabs** | Every new query tab pre-seeded with builder-attribution header comment |
| **All Exports** | CSV / JSON / HTML / Markdown / SQL / DDL exports include builder attribution headers |

### 🖥 SSMS UI Shell

Title Bar · Menu Bar (7 menus) · Standard Toolbar · Object Explorer Tree · Filter · Right-click Context Menus · Tabbed Query Documents · Results/Messages/Chart/Stats/ERD/Plan/Hints Tabs · SSMS-style Grid · Status Bar · SELECT TOP 1000 Generator · Command Palette · Resizable Splitters

### ✏ SQL Editor

Syntax Highlighting · Line Numbers · IntelliSense (Ctrl+Space) · SQL Formatter (Ctrl+Shift+F) · Find & Replace (Ctrl+H) · Comment Toggle (Ctrl+/) · Multi-Tab Editor · Tab indent · Font Size · Auto-save · Cursor position

### ▶ Query Execution

Execute (F5) · Execute All Statements · Parse / Validate (Ctrl+F5) · Display Execution Plan (Ctrl+L) · Cancel Query · **GO Batch Separator** · **DECLARE / SET / @variables**

### 📋 Results Grid

Sort columns · Multi-column sort (Shift+Click) · Filter rows · Regex filter · Inline cell edit · Right-click context · Bookmark rows · Pivot/Transpose · Copy whole table · Export (6 formats)

### 📈 Analysis & Visualisation

Chart Visualiser (6 chart types) · ER Diagram · Aggregator (∑) · NULL Heatmap (🔥) · Column Statistics

### 🛠 Query Tools

SQL Hints Analyser (12 rules, click-to-fix) · JOIN Helper · Visual Query Builder · Find Duplicates · Snapshot A/B + Diff

### 🗄 Data Management

Load Sample DB (13 datasets) · Import CSV · **Import JSON** · Import SQL script · Export `.sqlite` · Import `.sqlite` · Export Schema DDL · Create Table Wizard · Insert Row Form · Data Quality Validator

### ⚡ Productivity

Query Macro Recorder · Markdown Report Builder · Query History · Saved Queries (Ctrl+S) · SQL Notebook · Query Templates · SQL Snippets · Practice Challenges · T-SQL Reference Card · Settings & Options

### 🏢 V10 Enterprise Modules

**Activity Monitor · SQL Server Profiler · Query Store · Performance Dashboard · Programmability (Procs/Views/Triggers) · Security & Logins · Backup & Restore Wizard · Maintenance Plan Wizard · Import/Export Wizard · Database Diagrams · Always On Dashboard · Registered Servers · Solution Explorer · Template Explorer**

### 🔄 T-SQL Translation Layer

30+ rules. AUTO / STRICT / OFF modes. Translation map in Help menu.

---

## 🚀 Quick Start

### Option A — Use the Live URL (zero setup)

> **<https://cssadewale.github.io/ms-sql-server-simulator/>**

No login. No account. Open and start writing SQL.

### Option B — Download & Open Locally

```text
1. Download index.html from this repository (or clone the repo)
2. Open it in Chrome, Edge, Firefox, or Safari
3. First load fetches ~3 CDN libraries (~5 seconds, needs internet once)
4. All features work offline from this point forward
5. Click 📦 in the toolbar → load Employees → press F5 to execute
```

### Option C — Install as a Home-Screen App (Android / iOS)

```text
1. Open the live URL in Chrome (Android) or Safari (iOS)
2. Tap ⋮ menu → "Add to Home screen"
3. Name it "MS SQL Simulator" → tap Add
4. Opens fullscreen like a native app, works offline
```

### 5-Minute Enterprise Tour

```sql
-- 1. Dismiss the welcome splash (it greets you with the builder bio)
-- 2. Click 📦 in the toolbar → load Employees + Departments

-- 3. Write authentic T-SQL — the translation engine handles it
SELECT TOP 10
    e.first_name,
    e.last_name,
    e.department,
    e.salary,
    IIF(e.salary > 700000, 'High', 'Standard') AS band,
    YEAR(e.hire_date) AS year_joined,
    DATEDIFF(day, e.hire_date, GETDATE()) AS days_employed,
    ISNULL(e.city, 'Unknown') AS city
FROM dbo.employees e
WHERE e.department IN ('Engineering', 'Sales')
ORDER BY e.salary DESC;
GO

-- 4. Press F5 — Messages tab shows what got translated
-- 5. Tools menu → Activity Monitor — see the query register live
-- 6. Tools menu → SQL Server Profiler — see the trace event
-- 7. Tools menu → Query Store — pattern aggregation
-- 8. Right-click employees in Object Explorer → SELECT TOP 1000
-- 9. Tools menu → Programmability → Create View → name "vw_top_earners",
--    SELECT first_name, salary FROM employees ORDER BY salary DESC LIMIT 10
-- 10. Tools menu → Backup & Restore Wizard → download a .bak file
-- 11. Tools menu → Maintenance Plan → run all 7 tasks
-- 12. Click the 👤 strip at the bottom → meet the builder
```

---

## 🗄 Sample Databases

13 built-in datasets with realistic Nigerian business and educational context. Multiple datasets can be loaded simultaneously and joined together.

| # | Dataset | Rows | Description | Best For |
|---|---|---|---|---|
| 1 | 👥 Employees | 20 | HR: salaries, departments, performance | `GROUP BY`, `CASE`, window functions |
| 2 | 🏢 Departments | 6 | Dept budgets, heads, locations | JOIN with Employees |
| 3 | 🧑 Customers | 10 | Customer profiles with tiers | LEFT JOIN with Orders |
| 4 | 💰 Orders | 30 | Sales transactions by product, region, status | Aggregates, filtering |
| 5 | 🎓 Students | 60 | Academic scores across subjects and classes | `HAVING`, pass-rate analysis |
| 6 | 📦 Inventory | 12 | Stock levels, costs, reorder levels | `CASE` thresholds |
| 7 | 🏥 Hospital (patients) | 20 | Admissions, diagnoses, billing | Date functions |
| 8 | 📱 Products | 10 | Catalogue with costs and margins | JOIN with Orders |
| 9 | 💳 Transactions | 50 | Financial ledger, credits and debits | Window functions, running totals |
| 10 | 📅 Staff Attendance | 40 | Daily check-in / check-out | JOIN with Employees |
| 11 | 💵 Payroll | 40 | Monthly salary slips | Payroll analysis |
| 12 | 🎯 Sales Targets | 30 | Monthly target vs actual by salesperson | Variance analysis |
| 13 | 📚 Courses + Enrollments | 45 | Students ↔ Courses many-to-many | Multi-table JOIN |

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `F5` / `Ctrl+Enter` | **Execute current query** (or selection) |
| `Ctrl+F5` | Parse / Validate SQL |
| `Ctrl+L` | Display Execution Plan |
| `Ctrl+Alt+A` | **Activity Monitor** (v10) |
| `Ctrl+N` | New Query Window |
| `Ctrl+O` | Open SQL File |
| `Ctrl+S` | Save Query to Library |
| `Ctrl+Shift+S` | Save Query as `.sql` file |
| `Ctrl+W` | Close current tab |
| `Ctrl+P` | Command Palette (every action) |
| `Ctrl+H` | Find & Replace |
| `Ctrl+Space` | IntelliSense Autocomplete |
| `Ctrl+Shift+F` | Format SQL |
| `Ctrl+/` | Toggle Comment |
| `Ctrl+R` | Toggle Results Pane |
| `F1` | Feature Help Guide |
| `F8` | Toggle Object Explorer |
| `F11` | Fullscreen |
| `Esc` | Close modals / autocomplete |
| `Tab` | 4-space indent |
| `Shift+Click header` | Multi-column sort |
| `Double-click cell` | Inline edit (runs UPDATE) |
| `Double-click table` | Generate `SELECT TOP 1000` |
| `Right-click row / column` | Context menu |
| Click `T-SQL: AUTO` badge | Cycle T-SQL translation mode |
| Click 👤 in status bar / strip | Meet the Builder |

---

## 📁 Repository Structure

```text
ms-sql-server-simulator/
│
├── index.html                            ← THE APP (single file, ~360 KB)
├── ms-sql-server-simulator-v10.html      ← Versioned backup (identical)
├── index.v9-backup.html                  ← Previous v9 backup
│
├── README.md                             ← This document
├── CHANGELOG.md                          ← Full version history
├── CONTRIBUTING.md                       ← How to contribute
├── LICENSE                               ← MIT License
├── .gitignore                            ← OS / editor noise to ignore
│
├── .github/
│   └── workflows/
│       └── pages.yml                     ← Auto-deploy to GitHub Pages on push
│
├── docs/
│   ├── FEATURES.md                       ← Long-form feature documentation
│   ├── DEPLOYMENT.md                     ← Detailed deployment steps
│   ├── SSMS_MAPPING.md                   ← SSMS element mapping
│   ├── TSQL_TRANSLATION.md               ← Full T-SQL translation reference
│   └── BUILDER.md                        ← About the builder (markdown bio)
│
└── assets/
    └── (screenshots go here)
```

---

## 🚀 Deployment Guide

The application is a **single static HTML file**. It can be deployed on any platform that serves static files. **Five fully detailed paths below** — pick whichever fits your workflow.

### 📌 Pre-Deployment Checklist

- [ ] You have a GitHub account (for options 1, 2, 4) — sign up free at <https://github.com>
- [ ] You have downloaded `index.html` (and ideally the whole repository)
- [ ] You have a modern browser (Chrome / Edge / Firefox / Safari — desktop or Android)

---

### 1️⃣ GitHub Pages (Recommended — Free, Easy, CI/CD Built In)

**Result:** Your app live at `https://YOUR_USERNAME.github.io/REPO_NAME/`
**Cost:** Free forever for public repositories.
**Time:** ~3 minutes.

#### Step 1 — Create the repository

1. Go to <https://github.com/new>
2. Repository name: `ms-sql-server-simulator`
3. Visibility: **Public** (required for free GitHub Pages on personal accounts)
4. Tick **"Add a README file"**
5. Click **Create repository**

#### Step 2 — Upload the files (via web UI — works from tablet)

1. In the new repo, click **Add file → Upload files**
2. Drag every file from this project:
   - `index.html`
   - `ms-sql-server-simulator-v10.html`
   - `README.md`
   - `CHANGELOG.md`
   - `CONTRIBUTING.md`
   - `LICENSE`
   - `.gitignore`
   - The `docs/` folder (all files inside)
   - The `.github/workflows/pages.yml` file
3. Scroll down → commit message: `Initial commit — MS SQL Server Simulator v10 Enterprise Edition`
4. Click **Commit changes**

#### Step 2 (alternative) — Via Git CLI (desktop)

```bash
git clone https://github.com/YOUR_USERNAME/ms-sql-server-simulator.git
cd ms-sql-server-simulator
# Copy all project files into this folder
git add .
git commit -m "Initial commit — MS SQL Server Simulator v10 Enterprise Edition"
git push origin main
```

#### Step 3 — Enable GitHub Pages

1. In your repo, click **Settings** (top right)
2. In the left sidebar, click **Pages**
3. Under **Build and deployment**:
   - **Source:** select `Deploy from a branch`
   - **Branch:** select `main` and folder `/ (root)`
4. Click **Save**
5. Wait 30–60 seconds. Refresh the page. You will see:
   > ✅ Your site is live at `https://YOUR_USERNAME.github.io/ms-sql-server-simulator/`

#### Step 4 — Visit your site

Open the URL above. The welcome splash greets you (built by Adewale Samson Adeagbo). Click **Get Started →** and you're in.

> **Tip:** Every future `git push` to `main` auto-redeploys via the included `.github/workflows/pages.yml`.

---

### 2️⃣ Cloudflare Pages (Fastest CDN — Matches Your Other Sites)

**Result:** Live at `https://YOUR_PROJECT.pages.dev`
**Cost:** Free.
**Time:** ~2 minutes after repo exists.

1. Push the repo to GitHub (Step 1–2 above)
2. Go to <https://dash.cloudflare.com> → sign up / log in (free)
3. Left sidebar: **Workers & Pages** → **Create application** → **Pages** tab → **Connect to Git**
4. Authorise Cloudflare to read your GitHub
5. Select the `ms-sql-server-simulator` repository → **Begin setup**
6. Configure:
   - **Project name:** `ms-sql-server-simulator`
   - **Production branch:** `main`
   - **Framework preset:** **None**
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
7. Click **Save and Deploy**
8. Wait ~30 seconds. Site live at the printed URL (e.g. `mssqlsim.pages.dev`).

> **Note:** Cloudflare Pages auto-rebuilds on every push to `main` — no extra config needed. This matches your existing `cssadewale.pages.dev`, `hmgacademy.pages.dev`, `hmgconcepts.pages.dev` setup.

---

### 3️⃣ Netlify (Easiest — Drag & Drop, No Git Needed)

**Result:** Live at `https://RANDOM-NAME.netlify.app`
**Cost:** Free.
**Time:** ~30 seconds.

1. Go to <https://app.netlify.com/drop>
2. Sign up free if needed
3. **Drag the entire project folder** onto the drop zone (or just `index.html` if you only want the app)
4. Wait ~10 seconds. Site live.
5. Click **Site settings → Domain management** to choose a custom subdomain like `ms-sql-server-sim.netlify.app`

---

### 4️⃣ Vercel (Production-Grade — From GitHub)

1. Go to <https://vercel.com/new>
2. **Import Git Repository** → authorise → select `ms-sql-server-simulator`
3. **Framework Preset:** Other
4. **Root Directory:** `./`
5. **Build Command:** leave empty
6. **Output Directory:** leave empty (or `.`)
7. Click **Deploy**. Live in ~30 seconds at `https://PROJECT.vercel.app`.

---

### 5️⃣ Local / Offline (No Internet After First Load)

1. Download `index.html`
2. Double-click it — opens in your default browser via `file://`
3. First load fetches the 3 CDN libraries; browser cache keeps them
4. Subsequent opens work fully offline
5. On Android: open in Chrome → menu → **Add to Home screen** — works like a native app

> **Why this matters:** The builder built the entire app on an Android tablet with limited mobile data — proving the project's tablet-first ethos.

---

## ⚙ Continuous Deployment (GitHub Actions)

The bundled `.github/workflows/pages.yml` auto-deploys to GitHub Pages on every push to `main`. **You do not need to edit anything for this to work** — just enable GitHub Pages once as described above.

The workflow:

1. Triggers on push to `main` (and manual dispatch)
2. Uploads the entire repo as a Pages artifact
3. Deploys to your `*.github.io/REPO_NAME/` URL
4. Reports the live URL in the Actions tab

To enable: in your repo → **Settings → Pages → Source = GitHub Actions** (instead of "Deploy from a branch") if you want the workflow to be the source of truth.

---

## 🧱 Architecture Notes

```text
┌──────────────────────────────────────────────────────────────────┐
│                          Browser (Chrome / Edge / Firefox)        │
├──────────────────────────────────────────────────────────────────┤
│                                                                    │
│   ┌────────────────────┐   ┌────────────────┐   ┌──────────────┐   │
│   │   index.html       │   │  sql.js WASM   │   │  Chart.js    │   │
│   │   (UI + JS + CSS)  │◄──┤  SQLite Engine │   │  Visualiser  │   │
│   │                    │   └────────────────┘   └──────────────┘   │
│   │   T-SQL → SQLite   │                                            │
│   │   Translation      │                                            │
│   │   (30+ rules)      │                                            │
│   │                    │                                            │
│   │   Activity Monitor │                                            │
│   │   Profiler         │                                            │
│   │   Query Store      │                                            │
│   │   Programmability  │                                            │
│   │   Security         │                                            │
│   │   Backup/Restore   │                                            │
│   │   Maintenance      │                                            │
│   │   Always On UI     │                                            │
│   └────────────────────┘                                            │
│         ▲                                                          │
│         │                                                          │
│         └──── localStorage ───── PapaParse CSV                     │
│              (history, saved, notebook, logins, stored procs,      │
│               theme, font size, tabs, tsql mode, splash state)     │
│                                                                    │
└──────────────────────────────────────────────────────────────────┘

  NO BACKEND. NO API. NO COOKIES. NO ANALYTICS. NO TRACKING.
  Everything runs in YOUR browser. Your data never leaves YOUR device.
```

- **Storage:** all user state (history, saved queries, notebook, stored objects, logins, theme, font size, tabs, T-SQL mode, splash dismissed state) in `localStorage` under `mssss_*` keys.
- **Database:** sql.js creates a SQLite database in memory; can be exported/imported as a `.sqlite` or `.bak` binary file.
- **Privacy:** zero outbound requests after the initial CDN library fetch. Your queries and data never leave the browser.
- **Performance:** SQLite WASM handles tens of thousands of rows comfortably on a mid-range tablet.

---

## 📋 Version History

### v10.0 — 2026 (Current — Enterprise Edition)

**Major additions:**
- **T-SQL Translation Engine** — 30+ rules
- **Activity Monitor**, **SQL Server Profiler**, **Query Store**, **Performance Dashboard**
- **Programmability** — Stored Procedures, Views, Triggers
- **Security & Logins** — 5 default logins, 9 server roles
- **Backup & Restore Wizard** — Full database `.bak` round-trip
- **Maintenance Plan Wizard** — 7 tasks
- **Import / Export Wizard** — 6 sources, 8 targets
- **Database Diagrams**, **Always On Dashboard (Visual)**
- **Registered Servers**, **Solution Explorer**, **Template Explorer**
- **GO Batch Separator**, **DECLARE/SET/@variables**, **sys.tables/INFORMATION_SCHEMA**
- **JSON Import**
- **Welcome Splash**, **Builder Strip**, status-bar builder credit, Object Explorer builder node, attribution in all exports, console signature

### v9.0 — 2026 (SSMS UI Shell)

- Complete UI rebuild as SSMS-inspired shell
- Object Explorer tree, tabbed query documents, blue status bar
- IntelliSense Ctrl+Space autocomplete
- In-app Deployment Guide
- All v8 features preserved

### v8 — 2025 (QueryForge final)

- Author identity embedded, Table Overview Dashboard, Data Validator
- SQL Hints Analyser (12 checks), Macro Recorder, Markdown Report, Result Set Diff

### v1–v7 — 2024–2025

See [CHANGELOG.md](CHANGELOG.md) for the full detail.

---

## 👤 About the Builder

<div align="center">

### **Adewale Samson Adeagbo**

**Data Scientist · EdTech Builder · Virtual Tutor · AI-Augmented Solutions Developer · DataTech Builder · FaithTech Builder**

</div>

**Based in:** Lagos, Nigeria 🇳🇬
**Founded:** HMG Concepts (His Marvellous Grace Educational Consult) — 2015
**Education:** B.Sc(Ed) Computer Science Education — Lagos State University (2023)
**Currently enrolled in:**

- 🌺 **DeepTech_Ready** — DSN × 3MTT × Google.org — DSML Cohort 3
- 🌺 **WorldQuant University** — Applied Data Science Lab
- 🌺 **Kodecamp Cohort 6** — Machine Learning Core Track

**Teaching experience:** 15+ years in Nigerian classrooms — Nursery, Primary, JSS, SSS — across Mathematics, Further Mathematics, Physics, Chemistry, and Computer Science. Schools include His Marvellous Grace, Fredaks, Anchor Heights, Dave Model, Lifeline, De Glorious College, Chrisville, Angel High School, God of Seed Academy.

> *"I did not wait to become a developer. I used clear thinking and AI leverage to build the tools my students needed. That working method is the real skill — not any specific technology."*

### 🏛 HMG Concepts — Three Pillars

| Subsidiary | Mission | URL |
|---|---|---|
| **HMG Academy** | Full virtual learning institution — all subjects, all levels, Nigerian + international exams (WAEC, NECO, JAMB, IGCSE, IELTS, JUPEB, SAT) | <https://hmgacademy.pages.dev> |
| **HMG Technologies** | EdTech and data-driven solutions — CBT Pro, MS SQL Server Simulator, ML tools | (this project + others) |
| **HMG Media** | Educational content, digital presence, YouTube channel | <https://hmgconcepts.pages.dev> |

### 🛠 Core Skills

- **Data Science / ML:** Python · Pandas · NumPy · scikit-learn · XGBoost · Gradient Boosting · Random Forest · SHAP Explainability · SMOTE · TF-IDF · VADER · Streamlit · Joblib
- **BI / Analytics:** SQL · Power BI · Tableau · Excel (Advanced) · Google Sheets (Advanced) · EDA · Statistical Summaries
- **Web & EdTech:** HTML5 · CSS3 · Vanilla JavaScript · Supabase (PostgreSQL + Row-Level Security) · GitHub Pages · Cloudflare Pages · Acode (mobile IDE)
- **Tools & Workflow:** Git · GitHub · Jupyter · Google Colab · VS Code · Formspree · AI-Augmented Solutions methodology

### 🚀 Live Projects (12 deployed across 7 industries)

| Project | Type | Stack / Result |
|---|---|---|
| 🗄 **MS SQL Server Simulator v10** *(this)* | Enterprise Browser Tool | SSMS-inspired enterprise workbench · 360 KB · SQLite WASM · T-SQL translation |
| ⚡ **QueryForge v8** | Browser Tool | Original engine for this app · 50+ features |
| 📝 **CBT Pro** | EdTech | Browser CBT platform · anti-cheat · scientific calculator · live with real students |
| 🏗 **Insurance Claim Prediction** | ML Classification | Random Forest · SHAP · ROC-AUC 0.6144 |
| 👔 **Staff Promotion Prediction** *(Yakub Trading Group)* | ML Classification | Random Forest · ROC-AUC 0.891 |
| 🏦 **Bank Customer Churn** | ML Classification | Gradient Boosting · ROC-AUC 0.8675 · F1 0.6091 |
| 💰 **Income Level Prediction** *(US Census)* | ML Classification | Random Forest · SMOTE |
| 📰 **TruthLens Fake News Detector** *(3MTT Capstone)* | NLP · ML | XGBoost · TF-IDF · Acc 86.75% · ROC-AUC 0.9393 |
| 🚚 **SwiftChain Delivery Prediction** | ML Multiclass | Gradient Boosting · Weighted F1 0.5791 |
| 🔥 **NeuroWell Burnout Predictor** | ML Regression | Gradient Boosting · R² 0.855 · RMSE 0.072 |

### 📡 Connect

| Platform | Link |
|---|---|
| 🌐 Portfolio | <https://cssadewale.pages.dev> |
| 💼 LinkedIn | <https://linkedin.com/in/adewalesamsonadeagbo> |
| ⌥ GitHub | <https://github.com/cssadewale> |
| 🎓 HMG Academy | <https://hmgacademy.pages.dev> |
| 🏛 HMG Concepts | <https://hmgconcepts.pages.dev> |
| 𝕏 Twitter / X | <https://x.com/cssadewale> |
| 📺 YouTube | <https://youtube.com/@hmgconcepts> |
| 📷 Instagram | <https://instagram.com/cssadewale> |
| ✉ Email | <buildingmyictcareer@gmail.com> |
| 📱 WhatsApp | [+234 810 086 6322](https://wa.me/2348100866322) |
| ☎ Phone (alt) | +234 809 448 1488 |

---

## 📄 License

**MIT License** — Copyright © 2026 Adewale Samson Adeagbo

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: the above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

See [LICENSE](LICENSE) for the full text.

---

<div align="center">

**If MS SQL Server Simulator v10 Enterprise Edition is useful to you, please give it a ⭐ star on GitHub.**

Built with 💚 by [**Adewale Samson Adeagbo**](https://linkedin.com/in/adewalesamsonadeagbo) — *enterprise-grade software built from an Android tablet in Lagos.*

*"I did not wait to become a developer. I used clear thinking and AI leverage to build the tools my students needed."*

</div>
