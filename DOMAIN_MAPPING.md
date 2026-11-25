# SHALOM CONNECT — DOMAIN MAPPING

**Root Domain:** `https://shalomconnect.in`  
**Architecture:** Independent applications on dedicated subdomains; central directory on the root domain. No iframe masking; no cross-forwarding to a single app.

| Domain | Application Name | Repository | Hosting Provider | Base Path Requirement | Status |
|---|---|---|---|---|---|
| `shalomconnect.in` | Shalom Connect (Master Homepage) | `johnjoyraj/shalomconnect-home` | GitHub Pages | `/` | Ready to deploy |
| `www.shalomconnect.in` | Redirect to `shalomconnect.in` | `johnjoyraj/shalomconnect-home` | GitHub Pages (automatic apex/www redirect) | `/` | Pending DNS |
| `connecthub.shalomconnect.in` | Shalom ConnectHub India | `johnjoyraj/shalom-connecthub-india` | GitHub Pages | `/` (`VITE_BASE_PATH=/` when custom domain active) | Live at `johnjoyraj.github.io/shalom-connecthub-india/` |
| `family.shalomconnect.in` | Raj Family / FamilyRoots | `johnjoyraj/rajfamily` | GitHub Pages | Relative (`./`) | Live at `johnjoyraj.github.io/rajfamily/` |
| `store.shalomconnect.in` | Shalom Kerala Stores | `johnjoyraj/Shalom` | GitHub Pages | Relative (`./`) | Live at `johnjoyraj.github.io/Shalom/` |
| `pray.shalomconnect.in` | Pray for India | `johnjoyraj/prayforindia` | GitHub Pages | Relative (`./`) | Live at `johnjoyraj.github.io/prayforindia/` |
| `school.shalomconnect.in` | Multi-School Management SaaS | `johnjoyraj/school` | GitHub Pages | Relative (`./`) | Live at `johnjoyraj.github.io/school/` |
| `billbook.shalomconnect.in` | BillBook SaaS | `johnjoyraj/billbook` | GitHub Pages (needs Pages enabled) | Relative (`./`) | Repo ready; Pages disabled (`404`) |
| `whatsapp.shalomconnect.in` | WhatsApp Customer Automation | `johnjoyraj/whatsapp-automation` | **Python PaaS / VPS (NOT GitHub Pages)** | `/` (Flask app) | Local / Not yet cloud-deployed |
