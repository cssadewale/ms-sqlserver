# SSMS Mapping — How Every SSMS Element Maps to This Simulator

This is a side-by-side reference for users coming from real Microsoft SQL Server Management Studio. Every SSMS UI element is implemented here; some with adaptations noted.

> Author: **Adewale Samson Adeagbo** · MS SQL Server Simulator v9 · 2026

---

## Top Chrome

| Real SSMS | This Simulator | Implementation |
|---|---|---|
| Title bar with file path | Top title bar | Shows `SQLQueryN.sql (database)` plus author attribution |
| Database cylinder icon | SVG cylinder favicon + title icon | Three stacked ellipses in SSMS blue (`#0078d4`) |
| Window controls (min/max/close) | Light/Dark + About + Fullscreen | Browser handles window chrome |

---

## Menu Bar

Real SSMS has many menus; this simulator includes the 7 most-used.

| Real SSMS Menu | This Simulator | Notes |
|---|---|---|
| **File** | ✅ File | New / Open / Save / Import CSV / Load Sample DB / Export DDL / Print / Exit |
| **Edit** | ✅ Edit | Undo / Redo / Cut / Copy / Paste / Find & Replace / Toggle Comment / Format / Font Size |
| **View** | ✅ View | Object Explorer / Results / Messages / Chart / ERD / Theme / Fullscreen |
| **Query** | ✅ Query | Execute / Execute All / Display Plan / Parse / Cancel / Hints / Visual Builder / JOIN Helper |
| **Project** | (omitted) | Single-file editor — no multi-file project concept |
| **Debug** | (omitted) | SQLite stored procedures not implemented |
| **Tools** | ✅ Tools | Create Table / Insert Row / Find Duplicates / Validator / Macro / Report / Diff / Templates / Snippets / Challenges / Palette / Settings |
| **Window** | ✅ Window | New / Close / Close Others / Saved / History / Notebook |
| **Help** | ✅ Help | Feature Help / T-SQL Reference / Shortcuts / Deployment Guide / GitHub / Portfolio / About |

---

## Standard Toolbar

| Real SSMS Button | This Simulator | Behaviour |
|---|---|---|
| New Query | ✅ 📄 | Opens a new query tab |
| Open File | ✅ 📂 | Opens `.sql` file |
| Save | ✅ 💾 | Saves current query as `.sql` |
| Database dropdown | ✅ dropdown | `master` (single SQLite DB) |
| **Execute (green)** | ✅ ▶ Execute | F5 — runs current query |
| **Stop (red)** | ✅ ■ Stop | Visible while query runs |
| Parse | ✅ ✓ | Ctrl+F5 — syntax check |
| Display Estimated Execution Plan | ✅ 🔍 | Ctrl+L |
| Comment / Uncomment selected lines | ✅ ⌐ | Ctrl+/ |
| Format SQL | ✅ ⚡ | Ctrl+Shift+F |
| Find | ✅ 🔍 | Ctrl+H |
| (additions) | 📦 Samples · 📊 CSV · 🏗 Wizard · 💡 Hints · ⚙ Builder · 🔗 JOIN · ⌕ Palette · ⌨ Shortcuts · ❓ Help | |

---

## Object Explorer

| Real SSMS | This Simulator |
|---|---|
| Server connection node | ✅ Server root (`localhost\SQLEXPRESS (SQLite WASM 3.43)`) |
| Databases folder | ✅ Databases folder |
| System Databases | (omitted) |
| Database Snapshots | (omitted) |
| Database (master, msdb…) | ✅ Single `master` database (SQLite WASM limit) |
| Database Diagrams | ✅ Via Results pane → ER Diagram tab |
| **Tables** folder | ✅ Tables folder with live count |
| Individual table (e.g. `dbo.Employees`) | ✅ Shown as `dbo.tablename` with live row count |
| → Columns folder | ✅ Columns folder showing type and nullable |
| → Keys folder | ✅ Keys folder showing PKs |
| → Constraints folder | (folded into Columns — NOT NULL shown inline) |
| → Triggers folder | ✅ Placeholder (SQLite triggers not exposed here) |
| → Indexes folder | ✅ Indexes folder via `PRAGMA index_list` |
| → Statistics folder | (omitted — no query optimizer stats in SQLite WASM) |
| Views folder | ✅ Views folder |
| Stored Procedures | ✅ Placeholder (not natively supported in SQLite) |
| Functions | ✅ Placeholder (built-in functions only) |
| Security folder | ✅ Placeholder showing single user `adewale` |

### Object Explorer Context Menus (right-click table)

| Real SSMS Action | This Simulator |
|---|---|
| **SELECT TOP 1000 Rows** | ✅ Generates `SELECT * FROM table LIMIT 1000;` |
| Script Table as → CREATE → New Query Editor Window | ✅ Loads `CREATE TABLE …;` into editor |
| Design | ✅ Shows column schema in Results pane |
| Rename | ✅ Inline prompt → `ALTER TABLE … RENAME TO …` |
| Delete (DROP) | ✅ Confirm prompt → `DROP TABLE` |
| Refresh | ✅ Refresh button in Object Explorer toolbar |
| Edit Top 200 Rows | (use double-click cell to edit in results) |

---

## Query Editor

| Real SSMS Feature | This Simulator |
|---|---|
| Syntax colouring | ✅ Matches SSMS palette |
| Line numbers | ✅ Always on |
| IntelliSense (Ctrl+Space) | ✅ Keywords + functions + types + tables |
| Auto-complete on `.` | (not yet — manual Ctrl+Space) |
| Bracket matching | ✅ Brackets in gold |
| Find & Replace (Ctrl+H) | ✅ |
| Go To Line | (use scroll + line numbers) |
| Comment block (Ctrl+K, Ctrl+C) | ✅ Ctrl+/ |
| Format Document | ✅ Ctrl+Shift+F |
| Selection-only execute | ✅ If text is selected, F5 runs only the selection |
| Save with `.sql` extension | ✅ |
| Tabbed query windows | ✅ |
| Code regions / collapse | (not implemented) |

---

## Results Pane

| Real SSMS Tab | This Simulator |
|---|---|
| **Results** (Grid) | ✅ |
| **Results to Text** | (use Export → CSV/TSV) |
| **Results to File** | ✅ Export menu |
| **Messages** | ✅ With timestamped colour-coded entries |
| (additions) | 📈 Chart · 📉 Statistics · 🗺 ER Diagram · 🔍 Exec Plan · 💡 Hints |

### Results Grid Behaviour

| Real SSMS | This Simulator |
|---|---|
| Row number column on the left | ✅ |
| Sticky header row | ✅ |
| Click header to select column | ✅ + sorts |
| Drag column edge to resize | (auto-sized; manual resize not implemented) |
| Right-click row → Copy / Copy with Headers / Save Results As | ✅ Copy / Copy as JSON / Bookmark |
| Edit cell inline | ✅ Double-click to edit (runs UPDATE) |
| Save Results to file | ✅ Export menu |
| Open in Excel | ✅ Copy as TSV → paste in Excel |

---

## Status Bar

| Real SSMS Element | This Simulator |
|---|---|
| Connection status (Connected) | ✅ Green dot + "Connected" |
| Server name | ✅ `localhost\SQLEXPRESS (SQLite WASM 3.43)` |
| Login | ✅ `adewale` |
| Database | ✅ `master` |
| Query status (Executing/Completed) | ✅ |
| Row count | ✅ `N rows` (right side) |
| Execution time | ✅ Live clock + last query ms |
| Line/Column | ✅ `Ln 1, Col 1` |

---

## Keyboard Shortcuts (1:1 with SSMS where possible)

See [the keyboard shortcuts section in README.md](../README.md#%EF%B8%8F-keyboard-shortcuts).

---

## What's Different (and Why)

| Difference | Why |
|---|---|
| Engine is SQLite, not SQL Server | Only WASM SQL engine that runs in browser. |
| `SELECT TOP N` → `SELECT … LIMIT N` | SQLite doesn't support `TOP`. We translate automatically. |
| `GETDATE()` → `DATETIME('now')` | Use the T-SQL Reference Card for translations. |
| Multiple databases | One in-memory database (`master`) at a time; import/export `.sqlite` files for "switching". |
| Stored Procedures & Functions | Not natively supported in SQLite — placeholders shown. |
| Login/Security | Single user `adewale`; no role-based access. |
| Query optimizer statistics | SQLite uses a simpler planner; `EXPLAIN QUERY PLAN` is shown instead. |

---

*The goal is faithful **UI/UX** reproduction. The **engine** is intentionally lightweight SQLite-WASM so the entire experience runs free, offline, and on any device.*

— Adewale Samson Adeagbo · 2026
