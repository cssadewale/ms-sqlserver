# Deployment Guide — MS SQL Server Simulator

This document gives step-by-step instructions to deploy **MS SQL Server Simulator** to every major free static-hosting platform, plus offline use.

The app is a single `index.html` file. Any service that serves static files will host it correctly.

> Author: **Adewale Samson Adeagbo** · HMG Concepts · 2026

---

## 📋 Pre-Deployment Checklist

- [ ] Modern browser (Chrome, Edge, Firefox, or Safari)
- [ ] `index.html` downloaded (and ideally the whole project folder)
- [ ] GitHub account if using options 1, 2, or 4 — free at <https://github.com>

---

## 1️⃣ GitHub Pages — Recommended

**Result:** Your app live at `https://YOUR_USERNAME.github.io/REPO_NAME/`
**Cost:** Free forever for public repositories.
**Time:** ~3 minutes.

### Step-by-Step

#### Step 1 — Create the repository

1. Go to <https://github.com/new>
2. Repository name: `ms-sql-server-simulator`
3. Visibility: **Public** (required for free Pages on personal accounts)
4. Tick **"Add a README file"**
5. Click **Create repository**

#### Step 2 — Upload files (web UI — works on tablets)

1. In the new repo, click **Add file → Upload files**
2. Drag every file from the project folder:
   - `index.html`
   - `ms-sql-server-simulator-v9.html`
   - `README.md`
   - `CHANGELOG.md`
   - `CONTRIBUTING.md`
   - `LICENSE`
   - `.gitignore`
   - The `docs/` folder
   - The `.github/workflows/pages.yml` file
3. Scroll down → commit message: `Initial commit — MS SQL Server Simulator v9`
4. Click **Commit changes**

#### Step 2 (alternative) — Upload via Git CLI (desktop)

```bash
git clone https://github.com/YOUR_USERNAME/ms-sql-server-simulator.git
cd ms-sql-server-simulator
# Copy all project files into this folder
git add .
git commit -m "Initial commit — MS SQL Server Simulator v9"
git push origin main
```

#### Step 3 — Enable GitHub Pages

1. In your repo, click **Settings** (top right)
2. In the left sidebar, click **Pages**
3. Under **Build and deployment**:
   - **Source:** select `Deploy from a branch`
   - **Branch:** select `main` and folder `/ (root)`
4. Click **Save**
5. Wait 30–60 seconds, then refresh. You will see:
   > ✅ Your site is live at `https://YOUR_USERNAME.github.io/ms-sql-server-simulator/`

#### Step 4 — Visit your site

Open the URL above. Done.

#### Optional — Use the GitHub Actions workflow

The bundled `.github/workflows/pages.yml` enables automatic redeployment on every push.

To use it as the primary deployment source:

1. **Settings → Pages → Source = "GitHub Actions"**

Future `git push` events to `main` will trigger a redeploy with a live status in the **Actions** tab.

---

## 2️⃣ Cloudflare Pages — Fastest CDN

**Result:** Live at `https://YOUR_PROJECT.pages.dev`
**Cost:** Free.
**Time:** ~2 minutes after repo exists.

### Step-by-Step

1. Push the repo to GitHub (follow Option 1 Steps 1–2)
2. Go to <https://dash.cloudflare.com> → sign up / log in
3. Left sidebar: **Workers & Pages**
4. Click **Create application** → **Pages** tab → **Connect to Git**
5. Authorise Cloudflare to read your GitHub account
6. Select the `ms-sql-server-simulator` repository → **Begin setup**
7. Configure:
   - **Project name:** `ms-sql-server-simulator`
   - **Production branch:** `main`
   - **Framework preset:** **None**
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
8. Click **Save and Deploy**
9. Wait ~30 seconds. Site live at the printed URL.

**Custom domain:** project → **Custom domains → Set up a custom domain** → enter your domain → Cloudflare auto-issues SSL.

> Cloudflare Pages auto-rebuilds on every push to `main` — no extra config.

---

## 3️⃣ Netlify — Drag and Drop, No Git Needed

**Result:** Live at `https://RANDOM-NAME.netlify.app`
**Cost:** Free.
**Time:** ~30 seconds.

### Step-by-Step

1. Go to <https://app.netlify.com/drop>
2. Sign up free if needed
3. **Drag the entire project folder** onto the drop zone (or just `index.html` if you only want the app)
4. Wait ~10 seconds. Site live.
5. Click the site → **Site settings → Domain management → Change site name** for a friendlier subdomain like `ms-sql-server-sim.netlify.app`

### Optional — Connect to GitHub for auto-deploy

1. Netlify dashboard → **Add new site → Import an existing project**
2. Select GitHub → authorise → pick the repo
3. Build command: leave empty. Publish directory: `/`
4. **Deploy site**

---

## 4️⃣ Vercel — Production-Grade

**Result:** Live at `https://PROJECT.vercel.app`
**Cost:** Free.
**Time:** ~1 minute.

### Step-by-Step

1. Go to <https://vercel.com/new>
2. **Import Git Repository** → authorise → select `ms-sql-server-simulator`
3. **Framework Preset:** Other
4. **Root Directory:** `./`
5. **Build Command:** leave empty
6. **Output Directory:** leave empty (or `.`)
7. Click **Deploy**
8. Live in ~30 seconds at `https://PROJECT.vercel.app`

---

## 5️⃣ Local / Offline Use

**Result:** App opens from your file system, no internet after first load.
**Cost:** Free.
**Time:** Immediate.

### Step-by-Step

1. Download `index.html` (right-click → Save As)
2. Double-click it — opens in your default browser via `file://`
3. First load fetches the 3 CDN libraries (~5 seconds; needs internet once)
4. Browser cache keeps them; subsequent opens work fully offline

### On Android (tablet or phone)

1. Open the live URL in Chrome (e.g. <https://cssadewale.github.io/ms-sql-server-simulator/>)
2. Tap the ⋮ menu → **Add to Home screen**
3. Name it **MS SQL Simulator** → tap Add
4. Opens fullscreen like a native app, works offline

### On iOS

1. Open the live URL in Safari
2. Tap the Share icon → **Add to Home Screen**

---

## 🔄 Updating Your Deployment

| Platform | How to update |
|---|---|
| GitHub Pages | `git push` to `main` (auto-deploys via Pages or Actions) |
| Cloudflare Pages | `git push` to `main` (auto-deploys) |
| Netlify (drag-drop) | Drag the new file again, replacing the old |
| Netlify (Git) | `git push` to `main` (auto-deploys) |
| Vercel | `git push` to `main` (auto-deploys) |
| Local | Re-download `index.html` |

---

## 🌍 Custom Domain (Optional)

Once your site is live on any platform, you can attach a custom domain (e.g. `sqlsim.example.com`):

### GitHub Pages

1. Repo → **Settings → Pages → Custom domain** → enter `sqlsim.example.com`
2. In your DNS provider, add a `CNAME` record from `sqlsim` → `YOUR_USERNAME.github.io`
3. Wait ~10 minutes for DNS to propagate
4. Tick **Enforce HTTPS**

### Cloudflare Pages

1. Project → **Custom domains → Set up a custom domain** → enter the domain
2. Cloudflare provides DNS instructions; if your domain is already on Cloudflare DNS, it's automatic
3. SSL certificate auto-issued

### Netlify / Vercel

Similar flow: Domain settings → add domain → follow DNS instructions.

---

## 🐛 Troubleshooting

| Symptom | Fix |
|---|---|
| `404 — Page not found` on GitHub Pages | Confirm the file is literally `index.html` (lowercase) at the repo root. Check Settings → Pages is enabled. |
| Page loads but SQL engine never initialises | Open browser console (F12). The first load needs internet to fetch CDN libraries. Try a different network or check if your firewall blocks `cdnjs.cloudflare.com`. |
| Charts / autocomplete don't appear | Chart.js / PapaParse failed to load. Hard-refresh (`Ctrl+Shift+R`) to force re-fetch. |
| App is blank on Android | Update Chrome to the latest version. WebAssembly requires Chrome ≥ 57 (released 2017). |
| "Add to Home Screen" not appearing | Use Chrome on Android, not other browsers. Visit the URL twice in 5 minutes — Chrome's PWA prompt may take time. |
| GitHub Actions deploy failed | Check **Settings → Pages → Source** is set to "GitHub Actions" (not "Deploy from a branch"). Re-run the workflow from the Actions tab. |

---

## 📞 Support

| Channel | Detail |
|---|---|
| Issues | <https://github.com/cssadewale/ms-sql-server-simulator/issues> |
| Email | <buildingmyictcareer@gmail.com> |
| WhatsApp | [+234 810 086 6322](https://wa.me/2348100866322) |

---

*Built with 💚 by Adewale Samson Adeagbo · HMG Concepts · Lagos, Nigeria · 2026*
