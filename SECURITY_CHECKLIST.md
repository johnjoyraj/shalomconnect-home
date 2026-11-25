# SECURITY & PRIVACY CHECKLIST — SHALOM CONNECT

- [x] **No secrets in `shalomconnect-home`**: Master site is pure static HTML/CSS/JS with zero API keys, passwords, or service-role credentials.
- [x] **External link safety**: All 7 outbound subdomain links use `target="_blank" rel="noopener noreferrer"`.
- [x] **Privacy Policy & Terms**: Dedicated `privacy.html` and `terms.html` linked in footer.
- [x] **No database consolidation**: Each app retains its own Firebase or Supabase backend and access rules.
- [ ] **GitHub Verified Domain**: Verify `shalomconnect.in` in GitHub Account Settings → Pages → Verified domains before assigning subdomains (prevents subdomain takeover).
- [ ] **Enforce HTTPS**: Enable "Enforce HTTPS" in GitHub Pages settings for `shalomconnect-home`, `shalom-connecthub-india`, `rajfamily`, `Shalom`, `prayforindia`, `school`, and `billbook` after DNS propagation.
- [ ] **Firebase Authorized Domains**: Add each custom subdomain to its respective Firebase project's Authorized Domains list.
- [ ] **Supabase Redirect URLs**: Add `https://connecthub.shalomconnect.in/**` to `fkjiafpcbgqtnkdonrtb` Redirect URLs.
- [ ] **Private App Protection**: Ensure `billbook.shalomconnect.in` and `whatsapp.shalomconnect.in` require authentication and do not expose invoices, CVs, or customer databases publicly.
