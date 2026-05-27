# Changelog

All notable changes to **MS SQL Server Simulator** are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [v10.0] — 2026 (Current — Enterprise Edition)

### 🏢 Major Additions — Enterprise Modules

- **T-SQL Translation Engine** — 30+ deterministic rules that auto-translate Microsoft T-SQL to SQLite at execution time:
  - `SELECT TOP N` → `LIMIT N`
  - `GETDATE()`, `GETUTCDATE()`, `SYSDATETIME()` → `datetime('now',...)`
  - `ISNULL`, `LEN`, `CHARINDEX`, `CONVERT`, `IIF`, `CHOOSE`
  - `YEAR`, `MONTH`, `DAY`, `DATEPART`, `DATEDIFF`, `DATEADD`
  - `NEWID`, `STUFF`, `TRY_CAST`, `TRY_CONVERT`
  - `[bracket]` identifiers → `"quoted"`
  - `DECLARE @var`, `SET @var`, variable substitution
  - `GO` batch separator
  - `PRINT` statements
  - `sys.tables`, `sys.columns`, `sys.databases`, `INFORMATION_SCHEMA.TABLES`, `INFORMATION_SCHEMA.COLUMNS`
  - `sp_help`, `sp_tables`, `sp_columns`
  - `dbo.` schema prefix stripping
  - DDL types: `NVARCHAR(MAX)`, `BIT`, `MONEY`, `DATETIME2`, `UNIQUEIDENTIFIER`, `IDENTITY(1,1)`
  - `OFFSET N ROWS FETCH NEXT M ROWS ONLY` → `LIMIT M OFFSET N`
  - Status-bar badge `T-SQL: AUTO` clickable to cycle modes (AUTO / STRICT / OFF)
  - Translation map documented in Help menu

- **Activity Monitor** — Tools menu / `Ctrl+Alt+A`. Real-time KPI dashboard with 8 cards (queries, avg duration, rows, errors, uptime, tables, connections, engine), sparkline of recent execution times, and top-10 recent queries table. Auto-refresh every 2 seconds.

- **SQL Server Profiler** — Tools menu. Trace table of last 500 query events with time, SPID, event class (DDL/DML/SELECT/error), SQL text, duration, rows, user, db. Pause/resume capture, clear all, export trace as CSV with builder attribution.

- **Query Store** — Tools menu. Aggregates queries by normalized pattern. Heat-coded by avg duration: 🔥 HOT (>100ms) / 🟧 WARM (>30ms) / 🟦 COLD (<30ms). Top 20 patterns by total time.

- **Performance Dashboard** — Tools menu. 4 KPI cards (queries logged, average, p95, slowest), line chart of duration trend over last 50 queries, slowest-10 list.

- **Programmability** — Tools menu and Object Explorer node:
  - **Stored Procedures** — Create with `@param` list and body; execute with parameter prompts; full JS-backed substitution
  - **Views** — Real SQLite `CREATE VIEW`; one-click query
  - **Triggers** — Real SQLite `CREATE TRIGGER` for AFTER INSERT/UPDATE/DELETE
  - All persist in `localStorage`

- **Security & Logins** — Tools menu and Object Explorer node. Manage 5 default logins (`sa`, `adewale` [builder, sysadmin], `BUILTIN\Administrators`, `app_reader`, `app_writer`) and 9 server roles (sysadmin, serveradmin, securityadmin, processadmin, setupadmin, bulkadmin, diskadmin, dbcreator, public). Add / Enable / Disable / Delete.

- **Backup & Restore Wizard** — Tools menu. 4-step wizard for full database backup as `.bak` (binary SQLite). Round-trips schema, data, indexes, views, triggers. Restore-from-file picker with replace-confirm.

- **Maintenance Plan Wizard** — Tools menu. 7 tasks: Reorganize Indexes (REINDEX), Rebuild Indexes (REINDEX), Update Statistics (ANALYZE), Check Integrity (PRAGMA integrity_check), Vacuum (VACUUM), Cleanup History (>30 days), Full Backup. Run individually, selected, or all in sequence.

- **Import / Export Wizard** — Tools menu. Single hub for 6 import sources (CSV, JSON, SQL, SQLite, .bak, Excel-via-CSV) and 8 export targets (CSV, JSON, HTML, Markdown, SQL INSERTs, .sqlite, DDL, .bak).

- **Database Diagrams** — Tools menu. Dedicated 920×580 SSMS-style table relationship modal (uses ERD canvas engine).

- **Always On Dashboard (Visual)** — Tools menu. Simulated availability group `AG_HMG_PROD` with 1 PRIMARY + 2 SECONDARIES (synchronized) + 1 RESOLVING (failover), availability databases table, listener config. Educational visualisation only — SQLite is single-node.

- **Registered Servers** — View menu. Tree of saved server connections (local instance + mock demo servers).

- **Solution Explorer** — View menu. Treats saved queries as project items in an SSMS-style tree.

- **Template Explorer** — View menu. SSMS-style hierarchical template tree with 20+ templates across 5 folders (SQL Server Templates, DML, DDL, Reporting, **Builder Examples**).

- **GO Batch Separator** — Use `GO` on its own line to split scripts into multiple batches that execute sequentially. Each batch reports separately in Messages.

- **DECLARE / SET / @variables** — Write `DECLARE @x INT = 10; SET @x = 20;` — `@x` references in subsequent statements are auto-substituted (strings auto-quoted, numbers passed through).

- **sys.tables / INFORMATION_SCHEMA** — Query system catalogs as in real SQL Server. Translated to SQLite `sqlite_master` + `pragma_table_info`.

- **JSON Import** — File menu / Import wizard. Imports JSON array of objects as a new table; auto-detects column types.

### 👤 Builder Identity — Maximum Visibility (NEW)

- **Welcome Splash** — One-time first-load presentation with bio, roles, story, "Don't show again" checkbox.
- **Builder Strip** — Permanent blue strip above status bar with name, role, quick links (Portfolio, LinkedIn, GitHub, WhatsApp, Meet Builder). Hide via View menu.
- **Object Explorer Builder Node** — Permanent node "Builder: Adewale Adeagbo" at bottom of tree.
- **Status Bar Builder Credit** — Bottom-right clickable 👤 Adewale Adeagbo.
- **Title Bar Builder Link** — "by Adewale Samson Adeagbo 👤" clickable to bio.
- **Help Menu** — "Meet the Builder" as the first item with full bio modal.
- **Console Signature** — Browser console (F12) shows builder credit + all 7 contact links on startup.
- **New Query Tab Header** — Every new query tab pre-seeded with builder-attribution comment block.
- **Attribution in Exports** — CSV, JSON, HTML, Markdown, SQL, DDL exports include builder attribution headers with portfolio + LinkedIn + GitHub links.

### 📋 Help & Documentation

- New menu item: **Help → Meet the Builder** (first item)
- New menu item: **Help → T-SQL ↔ SQLite Translation Map** (with 30+ rule reference)
- New menu item: **Help → Full Feature Documentation** (long-form, every feature)
- Help links: GitHub (cssadewale), Builder Portfolio, Builder LinkedIn, HMG Academy, HMG Concepts, Contact Builder (WhatsApp)
- Expanded `HELP_DATA` with two new sections: "Meet the Builder" (7 entries) and "V10 Enterprise Features" (20 entries)
- Expanded `PALETTE_ITEMS` with 23 new commands

### ⌨ Keyboard Shortcuts

- `Ctrl+Alt+A` — Activity Monitor
- Click `T-SQL: AUTO` badge — cycle T-SQL translation mode

### 🔧 Internal

- `BUILDER` constant object with full builder contact data
- `withBuilderAttribution()` helper for exports
- `recordTrace()` function for Profiler
- `storedObjects` localStorage key for Procedures/Views/Triggers
- `logins` localStorage key for Security
- `traceEvents` array (max 500)
- 7 new modal HTML blocks dynamically injected after init
- Override pattern: `_originalExecuteQuery`, `_origNewQuery`, `_origExportResults`, `_origExportSchemaDDL`, `_origRenderOE`, `_origOpenModal` — every override preserves original behaviour

### 📦 File Stats

- Single HTML file: ~360 KB (up from v9 ~230 KB)
- 5 inline `<script>` blocks
- Builds clean (Node.js parse OK)

---

## [v9.0] — 2026 (SSMS UI Shell — renamed from QueryForge)

### Renamed
- Project renamed from **QueryForge** to **MS SQL Server Simulator** to make the SSMS-inspired intent explicit
- All references, localStorage keys (`qf8_*` → `mssss_*`), page title, About modal, and documentation updated

### Added — SSMS UI Shell
- Title bar with SSMS-style cylinder icon, document title, database name, builder attribution
- Menu bar with 7 menus: File · Edit · View · Query · Tools · Window · Help
- Standard toolbar with grouped icon buttons including green **▶ Execute** and red **■ Stop**
- Object Explorer tree (Server → Databases → master → Tables → Columns/Keys/Indexes/Triggers)
- Right-click table context menu (Script as / Design / Rename / DROP / SELECT TOP 1000)
- Filter box at top of Object Explorer
- Tabbed query documents with modified indicator and close button
- 7 results tabs: Results · Messages · Chart · Statistics · ER Diagram · Exec Plan · Hints
- SSMS-style results grid with row-number column, sticky headers
- Blue status bar with connection state, server, user, database, line/column, row count, live clock
- SELECT TOP 1000 generator on table double-click
- Resizable splitters (vertical + horizontal, mouse + touch)
- Authentic SSMS dark theme (default) + light theme

### Added — New Features
- IntelliSense Ctrl+Space autocomplete
- In-app Deployment Guide modal
- Settings & Options modal
- All 50+ features from v8 preserved

---

## [v8] — 2025 (QueryForge final)

- Author identity embedded across UI
- Table Overview Dashboard
- Data Validator (NOT NULL, UNIQUE, Min, Max, LIKE rules)
- SQL Hints Analyser (12 rule-based checks with click-to-apply fixes)
- Query Macro Recorder
- Markdown Report Builder
- Result Set Diff (Snapshot A vs B)

---

## [v7] — 2025

- Multi-column sort, regex filter, conditional formatting
- JOIN Helper, column visibility, right-click context menu
- Copy to clipboard, scratchpad, colour tags
- Search saved, auto-save draft, keyboard row navigation

---

## [v6] — 2025

- Feature Help, SQL Reference, Query Templates
- Aggregator, Insert Form, NULL Heatmap, Timer Badge
- Font Size, Favourites, DDL Export, Duplicate Detector
- 60 dark mode contrast fixes (WCAG AA)

---

## [v5] — 2025

- Command Palette, Fullscreen Editor, ERD
- Create Table Wizard, SQL Script Import
- 9-format Export, Row Bookmarking, Pivot, Perf Dashboard, Query Diff

---

## [v4] — 2025

- Visual Query Builder, 20 SQL Snippets
- Column Statistics, Data Summary, Inline cell edit, schema search

---

## [v3] — 2025

- Autocomplete, Find/Replace, EXPLAIN, Run All
- .sqlite persistence, 10 Practice Challenges

---

## [v2] — 2024

- Multi-tab editor, syntax highlighting, formatter, Chart.js
- Saved Queries, History, Notebook

---

## [v1] — 2024

- Initial release: SQLite WASM, CSV upload, sample datasets
