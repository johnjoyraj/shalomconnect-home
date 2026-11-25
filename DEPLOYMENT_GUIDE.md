# DEPLOYMENT GUIDE — SHALOM CONNECT

## 1. Master Homepage (`shalomconnect-home`)

1. Create GitHub repository `johnjoyraj/shalomconnect-home` (public).
2. Push `main` branch. `.github/workflows/deploy-pages.yml` automatically deploys to GitHub Pages.
3. In **Settings → Pages**:
   - Source: **GitHub Actions**
   - Once BigRock DNS records (`A` on `@` + `CNAME` on `www`) are active, set **Custom domain** to `shalomconnect.in` and enable **Enforce HTTPS**.

---

## 2. Subdomain Applications on GitHub Pages

### A. `rajfamily` → `family.shalomconnect.in`
- Uses relative paths; no code changes required.
- In `johnjoyraj/rajfamily` **Settings → Pages → Custom domain**, set `family.shalomconnect.in` and check **Enforce HTTPS** after DNS propagation.
- **Firebase Auth (`raj-family-33299`)**: Add `family.shalomconnect.in` to **Firebase Console → Authentication → Settings → Authorized domains**.

### B. `Shalom` → `store.shalomconnect.in`
- Uses relative paths including `manifest.json` and `sw.js`.
- In `johnjoyraj/Shalom` **Settings → Pages → Custom domain**, set `store.shalomconnect.in` and check **Enforce HTTPS**.
- **Firebase Auth**: Add `store.shalomconnect.in` to Firebase **Authorized domains**.

### C. `prayforindia` → `pray.shalomconnect.in`
- Uses relative paths. (Note: commit or review local uncommitted edits before pushing.)
- In `johnjoyraj/prayforindia` **Settings → Pages → Custom domain**, set `pray.shalomconnect.in` and check **Enforce HTTPS**.
- **Firebase Auth**: Add `pray.shalomconnect.in` to Firebase **Authorized domains**.

### D. `school` → `school.shalomconnect.in`
- Uses relative paths across `index.html`, `signin.html`, `school_admin.html`, `super_admin.html`, `student_parent_app.html`, `teacher_staff_app.html`, `apply_school.html`.
- In `johnjoyraj/school` **Settings → Pages → Custom domain**, set `school.shalomconnect.in` and check **Enforce HTTPS**.
- **Firebase Auth**: Add `school.shalomconnect.in` to Firebase **Authorized domains**.

### E. `billbook` → `billbook.shalomconnect.in`
- **Prerequisite:** GitHub Pages is currently **disabled** (`404`).
- In `johnjoyraj/billbook` **Settings → Pages**, enable Pages from branch `main` (root `/`).
- Once live, set **Custom domain** to `billbook.shalomconnect.in` and check **Enforce HTTPS**.
- **Firebase Auth**: Add `billbook.shalomconnect.in` to Firebase **Authorized domains**.

### F. `shalom-connecthub-india` → `connecthub.shalomconnect.in`
- **Important Vite Base Path Switch:** Currently `.github/workflows/deploy-pages.yml` builds with `VITE_BASE_PATH: /shalom-connecthub-india/`. When switching to custom domain `connecthub.shalomconnect.in`, update `VITE_BASE_PATH` to `/` (or `${{ vars.VITE_BASE_PATH || '/' }}` with repo variable `VITE_BASE_PATH=/`) so `/assets/*`, `/manifest.webmanifest`, and `/sw.js` resolve at root.
- **Supabase Auth (`fkjiafpcbgqtnkdonrtb`):**
  - Add `https://connecthub.shalomconnect.in/**` to **Authentication → URL Configuration → Redirect URLs**.
  - Update **Site URL** to `https://connecthub.shalomconnect.in/` once DNS is live.

---

## 3. Non-GitHub-Pages Application: `whatsapp-automation`

- `WHATSAPP-AUTOMATION` is a **Python Flask + Gunicorn** app (`Procfile`: `web: gunicorn app:app --workers 2 --threads 4 --timeout 120`).
- **Cannot run on GitHub Pages.**
- Deploy to Render, Railway, Fly.io, or a VPS with Python 3.11+, attach `whatsapp.shalomconnect.in` as a custom domain in that host's dashboard, and point the `whatsapp` DNS record in BigRock to that host's target.
