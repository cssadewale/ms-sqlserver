# Features — Long-Form Documentation (v10 Enterprise Edition)

Every feature in **MS SQL Server Simulator v10**, with **what it does**, **why it exists**, and **how to use it**.

> Press <kbd>F1</kbd> inside the app for a searchable version. Press <kbd>Ctrl+P</kbd> for the Command Palette listing every action.
>
> **Built by:** Adewale Samson Adeagbo · HMG Concepts · 2026

---

## 0. Meet the Builder (NEW in v10 — 7 touchpoints)

The builder's identity is intentionally embedded in 7 places so users can always credit, contact, or learn about the developer.

| # | Touchpoint | What |
|---|---|---|
| 1 | **Welcome Splash** | First-load presentation modal — bio, roles, story, "Don't show again" tickbox. Click 👤 Meet the Builder for full bio. |
| 2 | **Builder Strip** | Persistent blue strip above status bar — avatar, name, role, quick links (Portfolio · LinkedIn · GitHub · WhatsApp · Meet Builder). Hide via View menu. |
| 3 | **Status Bar Credit** | Bottom-right of status bar — clickable `👤 Adewale Adeagbo`. |
| 4 | **Object Explorer Node** | Permanent `Builder: Adewale Adeagbo` node at bottom of the tree. |
| 5 | **Title Bar Link** | "by Adewale Samson Adeagbo 👤" link in the top title bar. |
| 6 | **Help Menu — First Item** | `Help → Meet the Builder` shows the full bio modal with all 11 contact links. |
| 7 | **Console Signature** | Browser console (F12) prints builder credit + all 7 contact links on startup. |
| 8 | **New Query Tabs** | Every new query window opens with builder-attribution header comment. |
| 9 | **All Exports** | CSV/JSON/HTML/Markdown/SQL/DDL exports include builder attribution. |

---

## 1. SSMS UI Shell

### Title Bar
- Top bar with SSMS database-cylinder icon, current document, builder link, theme toggle, fullscreen.

### Menu Bar (7 menus)
**File / Edit / View / Query / Tools / Window / Help** — every item mirrors real SSMS where possible.

### Standard Toolbar
Grouped icon buttons — New / Open / Save / DB selector / **green ▶ Execute** / **red ■ Stop** / ✓ Parse / 🔍 Plan / Format / Comment / Find / Samples / CSV / Wizard / Hints / Builder / JOIN / Palette / Shortcuts / Help.

### Object Explorer (Server → Databases → master → Tables → Programmability → Security → Always On → Builder)
- Click ▶/▼ to expand/collapse
- Double-click table → `SELECT TOP 1000`
- Right-click table → Script as / Design / Rename / DROP / SELECT TOP 1000
- Filter box at the top
- v10 nodes: Programmability folder, Security folder, Always On, Activity Monitor, Builder

### Tabbed Query Documents
- `SQLQuery1.sql`, `SQLQuery2.sql`, …
- Modified dot (●) indicator
- Close × per tab
- Click + to add a new tab

### Results Pane Tabs
**📋 Results · 💬 Messages · 📈 Chart · 📉 Statistics · 🗺 ER Diagram · 🔍 Exec Plan · 💡 Hints**

### Status Bar
Bottom blue bar (SSMS classic `#0078d4`): connection · server · user · database · **T-SQL: AUTO badge** · line/column · row count · live clock · 👤 builder credit.

### SELECT TOP 1000 Generator
Double-click any table in Object Explorer to generate the SSMS-familiar `SELECT * FROM table LIMIT 1000` query.

### Command Palette (Ctrl+P)
Searchable list of every action in the app. Arrow keys + Enter to execute.

### Resizable Splitters
- Vertical splitter (Object Explorer width) — mouse + touch
- Horizontal splitter (editor / results)

---

## 2. SQL Editor

| Feature | How |
|---|---|
| Syntax highlighting | Real-time SSMS palette |
| Line numbers | Always visible |
| **IntelliSense (Ctrl+Space)** | Keyword / function / type / table autocomplete |
| Format SQL (Ctrl+Shift+F) | Uppercase keywords, indent clauses, split SELECT columns |
| Find & Replace (Ctrl+H) | Match count, next/prev, replace, replace-all |
| Toggle Comment (Ctrl+/) | Add/remove `--` on selected lines |
| Multi-Tab Editor | Each tab independent |
| Tab indent | 4 spaces |
| Font Size | A+/A− 9px to 22px, persistent |
| Auto-save | Every keystroke to localStorage |
| Cursor position | Live in status bar |

---

## 3. Query Execution

| Action | Shortcut | What |
|---|---|---|
| Execute | F5 / Ctrl+Enter | Run current query (or selection) |
| Execute All Statements | (menu) | Split on `;`, run each |
| **GO Batch Separator** (NEW v10) | `GO` on own line | Splits scripts into batches |
| **DECLARE / SET / @vars** (NEW v10) | (write in editor) | Variable substitution |
| Parse / Validate | Ctrl+F5 | Syntax check without execution |
| Display Execution Plan | Ctrl+L | EXPLAIN QUERY PLAN with ✓ SEARCH / ⚠ SCAN |
| Cancel Query | (red ■ Stop button) | |

---

## 4. T-SQL Translation Engine (NEW in v10)

See [TSQL_TRANSLATION.md](TSQL_TRANSLATION.md) for the full 30+ rule reference.

**Modes** (click `T-SQL: AUTO` badge in status bar to cycle):
- **AUTO** — translate everything, log to Messages
- **STRICT** — translate but flag prominently
- **OFF** — pass query straight to SQLite

---

## 5. Results Grid

Sort columns · Multi-column sort (Shift+Click) · Filter rows · Regex filter (`.*` toggle) · Inline cell edit (double-click) · Right-click context menus · Bookmark rows · Pivot/Transpose · Copy whole table (TSV for Excel) · Export 6 formats (CSV, TSV, JSON, HTML, Markdown, SQL INSERTs).

---

## 6. Analysis & Visualisation

- **Chart Visualiser** (📈) — Bar, Line, Pie, Doughnut, Polar, Scatter. PNG download.
- **ER Diagram** (🗺) — Auto-drawn relationships
- **Aggregator** (∑) — COUNT, SUM, AVG, MIN, MAX, MEDIAN, STDDEV for numeric columns
- **NULL Heatmap** (🔥) — Red/green grid of data completeness
- **Column Statistics** — Right-click column header

---

## 7. Query Tools

- **SQL Hints Analyser** — 12 deterministic rule-based checks with click-to-apply fixes
- **JOIN Helper** — Auto-detects shared columns
- **Visual Query Builder** — Form-based SELECT with live SQL preview
- **Find Duplicates** — GROUP BY HAVING COUNT(*)>1 on every table
- **Snapshot A / B + Diff** — Side-by-side result comparison

---

## 8. Data Management

- 13 Sample Databases (one-click load)
- Import CSV (auto type detection)
- **Import JSON** (NEW v10) — array of objects becomes a table
- Import SQL script
- Export `.sqlite` / Import `.sqlite`
- Export Schema DDL (with builder attribution)
- Create Table Wizard (form-based, live preview)
- Insert Row Form (per-table dynamic fields)
- Data Quality Validator (NOT NULL, UNIQUE, Min, Max, LIKE rules)

---

## 9. V10 Enterprise Modules (NEW)

### Activity Monitor
Tools menu / `Ctrl+Alt+A`. Real-time 8-card dashboard + sparkline + top-10 recent queries table. Auto-refresh 2 sec.

### SQL Server Profiler
Tools menu. Trace last 500 events with time, SPID, event class, SQL, duration, rows, user, db. Pause/Clear/Export CSV.

### Query Store
Tools menu. Normalized pattern aggregation with HOT/WARM/COLD heat coding.

### Performance Dashboard
Tools menu. Line chart of duration over time + p95 + slowest-10.

### Programmability
Tools menu / Object Explorer node. Tabs for **Stored Procedures**, **Views**, **Triggers**. Full CRUD; Stored Procs run with parameter prompts; Views are real SQLite VIEWs; Triggers are real SQLite TRIGGERs.

### Security & Logins
Tools menu / Object Explorer node. 5 default logins + 9 server roles. Add/Enable/Disable/Delete.

### Backup & Restore Wizard
Tools menu. 4-step wizard. Download as `.bak` (binary SQLite); restore replaces current DB.

### Maintenance Plan Wizard
Tools menu. 7 tasks (REINDEX, REINDEX, ANALYZE, integrity_check, VACUUM, history cleanup, full backup). Run individually, selected, or all.

### Import / Export Wizard
Tools menu. Single hub for 6 import sources + 8 export targets.

### Database Diagrams
Tools menu. Dedicated 920×580 SSMS-style relationship modal.

### Always On Dashboard (Visual)
Tools menu. AG_HMG_PROD cluster with PRIMARY + 3 SECONDARIES, availability databases, listener config.

### Registered Servers
View menu. Tree of saved server connections.

### Solution Explorer
View menu. Saved queries as project items.

### Template Explorer
View menu. SSMS-style hierarchical template tree with 20+ templates including Builder Examples.

---

## 10. Productivity

- **Command Palette** (Ctrl+P)
- **Query Macro Recorder**
- **Markdown Report Builder**
- **Query History** (last 100)
- **Saved Queries** (Ctrl+S) with favourites
- **SQL Notebook**
- **Query Templates** (10 real-world)
- **SQL Snippets** (15 patterns)
- **Practice Challenges** (10 graded)
- **T-SQL Reference Card**
- **Settings & Options**

---

## 11. Author Identity

See section 0 above. 9 distinct touchpoints throughout the UI.

---

*Adewale Samson Adeagbo · HMG Concepts · 2026 · Built on an Android tablet in Lagos · MIT Licence*
