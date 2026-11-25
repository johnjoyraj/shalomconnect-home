# SEO SETUP GUIDE — SHALOM CONNECT (`shalomconnect.in`)

## 1. Master Homepage SEO (Implemented)

`shalomconnect-home` includes:
- Descriptive `<title>` and `<meta name="description">`.
- `<link rel="canonical" href="https://shalomconnect.in/">`.
- Open Graph (`og:*`) and Twitter Card metadata.
- JSON-LD `Organization` and `WebSite` structured data.
- `robots.txt` (`Allow: /`, `Sitemap: https://shalomconnect.in/sitemap.xml`).
- `sitemap.xml` listing `/`, `/privacy.html`, and `/terms.html`.
- Clean semantic links to all seven subdomains.

---

## 2. Google Search Console Verification (Recommended)

Use a **Domain Property** in Google Search Console so one verification covers `shalomconnect.in` and all subdomains (`*.shalomconnect.in`):

1. Open [Google Search Console](https://search.google.com/search-console).
2. Choose **Add Property → Domain** and enter `shalomconnect.in`.
3. Copy the `TXT` verification record provided by Google.
4. Add that `TXT` record in BigRock DNS (`Host: @`, `Value: google-site-verification=...`).
5. Click **Verify** in Google Search Console.
6. Submit `https://shalomconnect.in/sitemap.xml` under **Sitemaps**.

> Note: Search indexing and rankings depend on Google's crawl schedule and content signals; immediate indexing is never guaranteed.

---

## 3. Per-Subdomain SEO & Indexing Policy

| Subdomain | Should Be Indexed? | Recommendation |
|---|---|---|
| `shalomconnect.in` | **Yes** | Public central homepage; submit `sitemap.xml`. |
| `connecthub.shalomconnect.in` | **Yes (public pages only)** | Index public listings (`/jobs`, `/properties`, `/schools`); keep `/dashboard/*` and `/admin/*` behind auth / `noindex`. |
| `store.shalomconnect.in` | **Yes (storefront)** | Index `index.html`; keep `billing.html`, `inventory.html`, `dashboard.html` private / `noindex`. |
| `pray.shalomconnect.in` | **Yes (public prayer book)** | Index `index.html`; add `noindex` to `admin.html` and `login.html`. |
| `school.shalomconnect.in` | **Public landing only** | Keep `school_admin.html`, `super_admin.html`, `student_parent_app.html`, `teacher_staff_app.html` private / `noindex`. |
| `family.shalomconnect.in` | **Optional / Private** | Family portals typically should use `<meta name="robots" content="noindex, nofollow">` if member data is private. |
| `billbook.shalomconnect.in` | **No (private SaaS)** | Add `robots.txt` `Disallow: /` or `noindex` so invoices/business records are never indexed. |
| `whatsapp.shalomconnect.in` | **No (private tool)** | Add `X-Robots-Tag: noindex, nofollow` or auth wall so customer messaging workflows are never indexed. |
