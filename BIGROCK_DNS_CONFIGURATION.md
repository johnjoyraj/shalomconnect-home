# BIGROCK DNS CONFIGURATION — SHALOM CONNECT (`shalomconnect.in`)

> **IMPORTANT:** Do NOT apply DNS records blindly. Review the verification status of each row below before entering records in BigRock's DNS Management panel.
> Specifically, `whatsapp.shalomconnect.in` is a **Python Flask server** (not GitHub Pages), and `billbook.shalomconnect.in` needs GitHub Pages enabled in `johnjoyraj/billbook` before custom-domain verification.

---

## 1. Pre-Check for Conflicting Records in BigRock

Before adding new records, inspect your existing BigRock DNS zone for `shalomconnect.in` and **remove or replace** any conflicting default records:
- Default BigRock **parking `A` records** on `@` (Host: `@` or blank).
- Default BigRock **parking `CNAME`** on `www`.
- Any existing `A`, `AAAA`, or `CNAME` record sharing the same host name (`@`, `www`, `connecthub`, `family`, `store`, `pray`, `school`, `billbook`, `whatsapp`).
- **Keep** any existing `MX`, `TXT` (SPF/DKIM/DMARC/Google verification) records untouched unless intentionally migrating email.

---

## 2. DNS Records Table for Manual Entry in BigRock

| Record Type | Host / Name | Value / Target | TTL | Purpose | Repository | Verification Status |
|---|---|---|---|---|---|---|
| `A` | `@` | `185.199.108.153` | `3600` (1 hr) | GitHub Pages Apex IP 1 | `shalomconnect-home` | Ready (add after GitHub Pages custom domain setup) |
| `A` | `@` | `185.199.109.153` | `3600` (1 hr) | GitHub Pages Apex IP 2 | `shalomconnect-home` | Ready |
| `A` | `@` | `185.199.110.153` | `3600` (1 hr) | GitHub Pages Apex IP 3 | `shalomconnect-home` | Ready |
| `A` | `@` | `185.199.111.153` | `3600` (1 hr) | GitHub Pages Apex IP 4 | `shalomconnect-home` | Ready |
| `CNAME` | `www` | `johnjoyraj.github.io` | `3600` (1 hr) | Redirect `www.shalomconnect.in` → `shalomconnect.in` | `shalomconnect-home` | Ready |
| `CNAME` | `connecthub` | `johnjoyraj.github.io` | `3600` (1 hr) | Shalom ConnectHub India | `shalom-connecthub-india` | Ready (Pages live; switch `VITE_BASE_PATH` to `/`) |
| `CNAME` | `family` | `johnjoyraj.github.io` | `3600` (1 hr) | Raj Family / FamilyRoots | `rajfamily` | Ready (Pages live) |
| `CNAME` | `store` | `johnjoyraj.github.io` | `3600` (1 hr) | Shalom Kerala Stores | `Shalom` | Ready (Pages live) |
| `CNAME` | `pray` | `johnjoyraj.github.io` | `3600` (1 hr) | Pray for India | `prayforindia` | Ready (Pages live) |
| `CNAME` | `school` | `johnjoyraj.github.io` | `3600` (1 hr) | Multi-School Management SaaS | `school` | Ready (Pages live) |
| `CNAME` | `billbook` | `johnjoyraj.github.io` | `3600` (1 hr) | BillBook SaaS | `billbook` | **Pending:** Enable GitHub Pages in `johnjoyraj/billbook` first |
| `CNAME` or `A` | `whatsapp` | `<YOUR_PYTHON_HOST_TARGET>` *(e.g. Render/Railway CNAME or VPS IP)* | `3600` (1 hr) | WhatsApp Customer Automation (Flask/Gunicorn) | `whatsapp-automation` | **HOLD / DO NOT POINT TO GITHUB PAGES:** App is Python Flask, not static HTML |

---

## 3. Recommended Domain Verification (GitHub Security Best Practice)

Before setting custom domains on GitHub Pages, verify `shalomconnect.in` at the **GitHub Account level**:
1. Go to **GitHub → Settings → Pages → Verified domains → Add a domain** (`shalomconnect.in`).
2. Add the `TXT` record GitHub gives you (e.g., `_github-pages-challenge-johnjoyraj.shalomconnect.in`) in BigRock DNS.
3. Click **Verify** in GitHub. This prevents anyone else from claiming subdomains of `shalomconnect.in` on GitHub Pages.

---

## 4. Recommended Order of Activation

1. Verify `shalomconnect.in` in GitHub Account Settings (TXT record).
2. Add the 4 `A` records (`@`) + `CNAME` (`www`, `connecthub`, `family`, `store`, `pray`, `school`) in BigRock.
3. Enable GitHub Pages on `johnjoyraj/billbook`, then add the `billbook` CNAME record.
4. Deploy `whatsapp-automation` to a Python PaaS (Render/Railway/VPS), then add the `whatsapp` CNAME/`A` record from that provider.
5. In each GitHub repository's **Settings → Pages → Custom domain**, enter the corresponding domain and check **Enforce HTTPS** once DNS propagates and TLS certificates are issued.
