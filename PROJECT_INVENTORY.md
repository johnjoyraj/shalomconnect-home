# SHALOM CONNECT — PROJECT INVENTORY

**Inspection Date:** 2026-11-25  
**GitHub Owner:** `johnjoyraj`  
**Workspace Root:** `E:\MYWORKSPACE`

---

## Executive Summary

All seven existing projects were inspected locally and checked against GitHub (`https://api.github.com/repos/johnjoyraj/<repo>` and `https://johnjoyraj.github.io/<repo>/`).

- **5 applications are currently LIVE on GitHub Pages** (`rajfamily`, `Shalom`, `prayforindia`, `school`, `shalom-connecthub-india`).
- **1 application (`billbook`)** is on GitHub as a static web app (`has_pages=False`, returns HTTP 404 on GitHub Pages) and requires GitHub Pages activation.
- **1 application (`whatsapp-automation`)** is a **Python Flask + SQLite + Gunicorn server application** (`Procfile`), NOT a static GitHub Pages frontend. Its GitHub repo returned HTTP 404 on the public API (private or not publicly accessible) and it has no cloud hosting URL verified yet.

---

## Detailed Repository Inventory

| # | Local Folder | GitHub Repo | Proposed Subdomain | Framework / Stack | Backend / Database | Current Deployment | Live URL Status | Custom Domain Configured? | Development Status |
|---|---|---|---|---|---|---|---|---|---|
| 1 | `familyroot` | `johnjoyraj/rajfamily` (Public) | `family.shalomconnect.in` | Single-file Static HTML/CSS/JS (`index.html`) | Firebase (`raj-family-33299`) | GitHub Pages (branch `main`) | `https://johnjoyraj.github.io/rajfamily/` (**HTTP 200**) | No | Deployed & Live |
| 2 | `SHALOM` | `johnjoyraj/Shalom` (Public) | `store.shalomconnect.in` | Static HTML/CSS/JS + PWA (`manifest.json`, `sw.js`) + Android Capacitor/APK + `webhook/` | Firebase Realtime DB / Firestore (`database.rules.json`, `firestore.rules`) | GitHub Pages (`.github/workflows/deploy-pages.yml`) | `https://johnjoyraj.github.io/Shalom/` (**HTTP 200**) | No | Deployed & Live (untracked local scripts/xlsx present) |
| 3 | `prayforindia` | `johnjoyraj/prayforindia` (Public) | `pray.shalomconnect.in` | Static HTML/JS (`index.html`, `admin.html`, `login.html`, `prayer-sync.js`) + Python scripts | Firebase Realtime DB (`database.rules.json`) | GitHub Pages (`google.yml` / branch) + `daily-4am-prayer.yml` | `https://johnjoyraj.github.io/prayforindia/` (**HTTP 200**) | No | Deployed & Live (local uncommitted edits present) |
| 4 | `school` | `johnjoyraj/school` (Public) | `school.shalomconnect.in` | Multi-page Static HTML/JS (`index.html`, `signin.html`, `school_admin.html`, `super_admin.html`, `student_parent_app.html`, `teacher_staff_app.html`, `apply_school.html`, `school-sync.js`) + Flutter `mobile_app/` | Firebase Realtime DB (`database.rules.json`) + local `server.py` / `school_database.db` | GitHub Pages | `https://johnjoyraj.github.io/school/` (**HTTP 200**) | No | Deployed & Live |
| 5 | `WHATSAPP-AUTOMATION` | `johnjoyraj/whatsapp-automation` (Private or 404 on public API) | `whatsapp.shalomconnect.in` | Python Flask (`app.py`, `templates/index.html`, `Procfile`: `gunicorn app:app`) | SQLite (`data/customers.db`) + Firebase (`firebase_service.py`) + OpenAI + WhatsApp Cloud API | Local / `Procfile` ready for Python PaaS (Render/Railway/VPS) | Not on GitHub Pages (Backend server required) | No | Under Development / Local (uncommitted cache & db changes) |
| 6 | `BILLBOOK-SAAS` | `johnjoyraj/billbook` (Public) | `billbook.shalomconnect.in` | Static HTML/CSS/JS (`index.html`, `css/`, `js/`, `assets/`, `templates/`) | Firebase Realtime DB (`database.rules.json`) | GitHub repo exists (`has_pages=False`) | `https://johnjoyraj.github.io/billbook/` (**HTTP 404**) | No | Ready locally; GitHub Pages not yet enabled |
| 7 | `SHALOM CONNECTHUB INDIA` | `johnjoyraj/shalom-connecthub-india` (Public) | `connecthub.shalomconnect.in` | React 18 + Vite + TypeScript + Tailwind + PWA (`manifest.webmanifest`, `sw.js`) | Supabase (`fkjiafpcbgqtnkdonrtb`) + 5 Deno Edge Functions | GitHub Pages (`.github/workflows/deploy-pages.yml`) | `https://johnjoyraj.github.io/shalom-connecthub-india/` (**HTTP 200**) | No | Deployed & Live (requires `VITE_BASE_PATH=/` switch for custom domain) |

---

## Key Technical Observations

1. **Relative Asset Paths**:
   - `rajfamily`, `Shalom`, `prayforindia`, `school`, and `billbook` all use relative paths (verified no hardcoded `github.io` or `/repo-name/` subpath references in their entry HTML files). `Shalom`'s `manifest.json` (`start_url: "index.html"`, `scope: "./"`) and `sw.js` (`./`) also use relative paths, so moving to a custom subdomain will not break assets.
2. **Vite Subpath vs Custom Domain (`shalom-connecthub-india`)**:
   - Currently `deploy-pages.yml` sets `VITE_BASE_PATH: /${{ github.event.repository.name }}/` for `https://johnjoyraj.github.io/shalom-connecthub-india/`.
   - When `connecthub.shalomconnect.in` is attached as the custom domain on GitHub Pages, `VITE_BASE_PATH` **must** be switched to `/` (or `vars.VITE_BASE_PATH || '/shalom-connecthub-india/'`) so JS/CSS/manifest/SW assets resolve at root `/`.
3. **WhatsApp Automation Hosting**:
   - Because `WHATSAPP-AUTOMATION` is a Python Flask + Gunicorn application (`Procfile`) with SQLite and background scheduling, **GitHub Pages cannot host it**. It must be deployed to a Python-capable host (e.g., Render, Railway, Fly.io, or a VPS), and `whatsapp.shalomconnect.in` must point to that provider's CNAME/A target—not `johnjoyraj.github.io`.
4. **Master Homepage Repository**:
   - A dedicated repository `johnjoyraj/shalomconnect-home` (`E:\MYWORKSPACE\shalomconnect-home`) has been created for `https://shalomconnect.in` so `shalom-connecthub-india` remains independent at `connecthub.shalomconnect.in`.
