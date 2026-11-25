# TESTING REPORT — SHALOM CONNECT

**Test Date:** 2026-11-25  
**Environment:** Local HTTP server (`http://127.0.0.1:4180`) + Headless Edge via Playwright

---

## 1. Master Homepage (`shalomconnect-home`) Verification

| Check | Result | Details |
|---|---|---|
| Desktop (`1280x800`) | **PASS** | `overflow=false`, `cards=7`, 0 console errors, 0 failed local requests |
| Tablet (`768x1024`) | **PASS** | `overflow=false`, `cards=7`, 0 console errors, 0 failed local requests |
| Mobile (`390x844`) | **PASS** | `overflow=false`, `cards=7`, mobile menu toggle (`#menu-toggle` -> `#mobile-nav.is-open`) verified |
| Service Links | **PASS** | All 7 links verified: `connecthub.shalomconnect.in`, `family.shalomconnect.in`, `store.shalomconnect.in`, `pray.shalomconnect.in`, `school.shalomconnect.in`, `whatsapp.shalomconnect.in`, `billbook.shalomconnect.in` |
| SEO Metadata | **PASS** | Title, meta description, canonical (`https://shalomconnect.in/`), Open Graph title, JSON-LD `Organization` + `WebSite` verified |
| Static & PWA Assets | **PASS** | `/privacy.html`, `/terms.html`, `/robots.txt`, `/sitemap.xml`, `/manifest.webmanifest`, `/assets/favicon.svg` all returned `HTTP 200` |

---

## 2. Existing Subdomain Pre-Checks (Current `github.io` Endpoints)

| Repository | Current Endpoint | HTTP Check | Notes |
|---|---|---|---|
| `rajfamily` | `https://johnjoyraj.github.io/rajfamily/` | **HTTP 200** | Ready for custom domain `family.shalomconnect.in` |
| `Shalom` | `https://johnjoyraj.github.io/Shalom/` | **HTTP 200** | Ready for custom domain `store.shalomconnect.in` |
| `prayforindia` | `https://johnjoyraj.github.io/prayforindia/` | **HTTP 200** | Ready for custom domain `pray.shalomconnect.in` |
| `school` | `https://johnjoyraj.github.io/school/` | **HTTP 200** | Ready for custom domain `school.shalomconnect.in` |
| `shalom-connecthub-india` | `https://johnjoyraj.github.io/shalom-connecthub-india/` | **HTTP 200** | Ready; switch `VITE_BASE_PATH` to `/` when `connecthub.shalomconnect.in` is attached |
| `billbook` | `https://johnjoyraj.github.io/billbook/` | **HTTP 404** | GitHub Pages not enabled yet in repo settings |
| `whatsapp-automation` | N/A | **Not Deployed** | Python Flask backend (`Procfile`); requires PaaS/VPS hosting |

---

## 3. Live Custom-Domain HTTPS Verification (Post-DNS)

| Custom Domain | Repository | Live HTTPS Check | Notes |
|---|---|---|---|
| `https://shalomconnect.in/` | `shalomconnect-home` | **HTTP 200** | Apex A records + Enforce HTTPS active |
| `https://connecthub.shalomconnect.in/` | `shalom-connecthub-india` | **HTTP 200** | CNAME + `VITE_BASE_PATH=/` + Enforce HTTPS active |
| `https://family.shalomconnect.in/` | `rajfamily` | **HTTP 200** | CNAME + Enforce HTTPS active |
| `https://store.shalomconnect.in/` | `Shalom` | **HTTP 200** | CNAME + Enforce HTTPS active |
| `https://pray.shalomconnect.in/` | `prayforindia` | **HTTP 200** | CNAME + Enforce HTTPS active |
| `https://school.shalomconnect.in/` | `school` | **HTTP 200** | CNAME + Enforce HTTPS active |
| `https://billbook.shalomconnect.in/` | `billbook` | **HTTP 200** | GitHub Pages enabled + CNAME + Enforce HTTPS active |
| `https://whatsapp.shalomconnect.in/` | `whatsapp-automation` | **Verified on Render (TLS Pending)** | Deployed on Render (`https://shalom-whatsapp-automation.onrender.com`); `CNAME` added in BigRock & Verified on Render |
