# MASTER PROJECT GUIDE — SHALOM CONNECT

**Platform:** Shalom Connect  
**Tagline:** One Digital Home. Multiple Connected Services.  
**Root Domain:** `https://shalomconnect.in`  
**Owner:** `johnjoyraj`

---

## 1. Architecture Overview

Shalom Connect is a **federated multi-domain digital ecosystem**.

- `https://shalomconnect.in` (repository: `johnjoyraj/shalomconnect-home`) serves as the lightweight, fast-loading central directory.
- Each of the seven applications operates **independently** on its own subdomain (`*.shalomconnect.in`) with its own codebase, database, authentication, and administration.
- No databases or authentication systems were merged. No iframe masking or forwarding hacks are used.

---

## 2. Subdomain Directory

| Subdomain | Application | Repository | Backend |
|---|---|---|---|
| `shalomconnect.in` | Master Homepage | `shalomconnect-home` | Static (GitHub Pages) |
| `connecthub.shalomconnect.in` | Shalom ConnectHub India | `shalom-connecthub-india` | Supabase (`fkjiafpcbgqtnkdonrtb`) |
| `family.shalomconnect.in` | Raj Family / FamilyRoots | `rajfamily` | Firebase (`raj-family-33299`) |
| `store.shalomconnect.in` | Shalom Kerala Stores | `Shalom` | Firebase |
| `pray.shalomconnect.in` | Pray for India | `prayforindia` | Firebase |
| `school.shalomconnect.in` | Multi-School Management SaaS | `school` | Firebase |
| `whatsapp.shalomconnect.in` | WhatsApp Customer Automation | `whatsapp-automation` | Python Flask + SQLite + Firebase |
| `billbook.shalomconnect.in` | BillBook SaaS | `billbook` | Firebase |

---

## 3. Documentation Index

- [PROJECT_INVENTORY.md](./PROJECT_INVENTORY.md) — Full audit of all 7 existing repositories.
- [DOMAIN_MAPPING.md](./DOMAIN_MAPPING.md) — Subdomain-to-repository and hosting mapping.
- [BIGROCK_DNS_CONFIGURATION.md](./BIGROCK_DNS_CONFIGURATION.md) — Exact DNS records for BigRock.
- [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) — Step-by-step GitHub Pages, custom domain, and backend auth setup.
- [SEO_SETUP_GUIDE.md](./SEO_SETUP_GUIDE.md) — Google Search Console, sitemaps, and indexing rules.
- [SECURITY_CHECKLIST.md](./SECURITY_CHECKLIST.md) — HTTPS, secrets, Firebase/Supabase rules, and privacy checks.
- [TESTING_REPORT.md](./TESTING_REPORT.md) — Verified test results for the master site and subdomain readiness.
- [DEVELOPMENT_STATUS.md](./DEVELOPMENT_STATUS.md) — Current completion status and remaining manual actions.
