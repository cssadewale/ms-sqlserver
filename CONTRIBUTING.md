# Contributing to MS SQL Server Simulator

Thank you for considering a contribution! This document explains how to contribute effectively.

---

## 🧭 Project Philosophy

**MS SQL Server Simulator** is a **single HTML file** with:

- No build system
- No npm
- No framework (no React, no Vue, no Svelte)
- No backend
- No AI API
- No paid services

Every feature is plain HTML, CSS, and Vanilla JavaScript. This is deliberate — the project must be **openable, editable, and testable on any device, including Android tablets without a development environment**. The author built the entire project on an Android tablet using [Acode](https://acode.app/) — and you should be able to fix bugs or add features the same way.

---

## ✅ Ground Rules

1. **All changes go in `index.html`.** Do not introduce a build step.
2. **CDN libraries from [cdnjs.cloudflare.com](https://cdnjs.cloudflare.com) only.** No paid services.
3. **No AI API.** Adding one would break the "free forever, no cost per query" guarantee.
4. **No backend.** Everything must run in the browser.
5. **Test on Android Chrome at 360 px width.** Many users are on tablets / phones.
6. **All new features must be added to the `HELP_DATA` array** in JavaScript so they show up in <kbd>F1</kbd> help.
7. **Preserve every existing feature.** Additions only — no removals without prior discussion via Issue.
8. **Keep the SSMS look.** Major UI changes that depart from SSMS conventions need an Issue first.

---

## 🐛 Reporting Bugs

1. Open a [GitHub Issue](https://github.com/cssadewale/ms-sql-server-simulator/issues/new)
2. Title format: `[BUG] Brief description`
3. Include:
   - Exact steps to reproduce
   - Expected behaviour
   - Actual behaviour
   - Your browser and OS (and tablet model if relevant)
   - Whether it reproduces on the live demo at <https://cssadewale.github.io/ms-sql-server-simulator/>
   - Screenshot if visual

---

## 💡 Suggesting a Feature

1. Open a [GitHub Issue](https://github.com/cssadewale/ms-sql-server-simulator/issues/new)
2. Title format: `[FEATURE] Brief description`
3. Explain:
   - What problem it solves
   - How you envision it working (rough UI sketch helps)
   - Whether it requires any new CDN library (if so, which and why)
   - Whether it preserves the single-file, no-backend, no-AI-API architecture

---

## 🚀 Submitting a Pull Request

1. **Fork** the repository
2. **Create a branch:** `git checkout -b feature/your-feature-name`
3. **Edit `index.html` only**
4. **Test thoroughly:**
   - Desktop Chrome — dark mode + light mode
   - Desktop Firefox
   - Android Chrome at narrow width (360 px)
   - Browser console — no JavaScript errors
5. **Add the feature to `HELP_DATA`** so users discover it via <kbd>F1</kbd>
6. **Add a command-palette entry** in `PALETTE_ITEMS` if applicable
7. **Update `CHANGELOG.md`** under the current version's "Added/Changed/Fixed" section
8. **Commit with a clear message:** `feat: add column hide button to results toolbar`
9. **Push and open a Pull Request** with a clear description

---

## 📏 Code Style

- Use `var`, `let`, or `const` consistently with the surrounding code
- Single quotes for JavaScript strings (`'foo'`, not `"foo"`)
- CSS class names: lowercase with hyphens (`results-grid`, not `resultsGrid`)
- New modal panels: follow the existing `.modal` / `.modal-head` / `.modal-body` / `.modal-foot` structure
- New toolbar buttons: must include a descriptive `title` attribute (becomes the SSMS-style tooltip)
- New menu items: follow the `mi` / `mi-icon` / `mi-kb` HTML pattern
- New features: must add entries to the `HELP_DATA` array in JavaScript

---

## ✅ New Feature Checklist

Before submitting your PR, tick every box:

- [ ] Works offline — no new external API calls
- [ ] Free — no paid service, no AI API
- [ ] Every button / tab has a descriptive `title` attribute
- [ ] Added to `HELP_DATA` array so it appears in the F1 Help Guide
- [ ] Added to `PALETTE_ITEMS` if it's a discoverable action
- [ ] Dark mode AND light mode both look correct
- [ ] Tested at 360 px mobile width
- [ ] Browser console shows zero errors
- [ ] Single-file architecture preserved
- [ ] CHANGELOG.md updated
- [ ] No existing features were removed

---

## 📞 Contact

| Channel | Detail |
|---|---|
| GitHub Issues | <https://github.com/cssadewale/ms-sql-server-simulator/issues> |
| LinkedIn | <https://linkedin.com/in/adewalesamsonadeagbo> |
| Email | <buildingmyictcareer@gmail.com> |
| WhatsApp | [+234 810 086 6322](https://wa.me/2348100866322) |

Thank you for helping make MS SQL Server Simulator better for learners everywhere.
