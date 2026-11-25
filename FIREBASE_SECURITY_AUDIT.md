# FIREBASE SECURITY AUDIT REPORT — SHALOM CONNECT

**Audit Date:** 2026-11-25  
**Firebase Projects Audited:** `adonaibroadcast-11095` (`Shalom`, `prayforindia`, `school`, `billbook`), `raj-family-33299` (`rajfamily`)

---

## 1. Executive Summary

- **No production Firebase rules were overwritten** during this audit, because `prayforindia` (`prayer-sync.js`), `school` (`school-sync.js`), `Shalom` (`cloud-sync.js`), and `rajfamily` (`index.html`) currently perform client-side writes without Firebase Auth ID tokens on one or more public/admin flows.
- Applying `auth != null` to those paths before updating the frontend clients would immediately break customer ordering, public prayer submissions, and school portals (`401 Permission denied` — already observed on `school/schools.json?shallow=true` and `billbook.json` before BillBook's Firebase Auth fix).

---

## 2. Vulnerability & Dependency Findings

| Project / File | Finding | Risk | Client Dependency Preventing Immediate Lock |
|---|---|---|---|
| `SHALOM/firestore.rules` | `customers/{phone}` allows `read, write: if true;`; `orders/{orderId}` allows `read, create, update: if true;` | **Critical** | `SHALOM` storefront (`app.js`, `cloud-sync.js`) writes orders/customers before/without Firebase Auth in guest checkout |
| `SHALOM/database.rules.json` | Multiple nodes use `".read": true` and `".write": true` (including `otps`, `orders`, `bills`, `customers`) | **Critical** | `cloud-sync.js` reads/writes `orders/`, `bills/`, `customers/`, `otps/` directly from client |
| `prayforindia/database.rules.json` | Public `.read: true` and `.write: true` on prayer nodes | **High** | `prayer-sync.js` uses unauthenticated REST `fetch(FIREBASE_BASE_URL + ... + '.json')` (`PUT`, `PATCH`, `DELETE`) |
| `school/database.rules.json` | Multiple nodes have `.read: true` / `.write: true` in repo file, while live `adonaibroadcast-11095` currently denies `school/schools.json?shallow=true` (`401`) | **High** | `school-sync.js` uses unauthenticated REST `fetch` without Firebase Auth ID tokens |
| `BILLBOOK-SAAS/database.rules.json` | Properly enforces `".read": "auth != null"`, `".write": "auth != null"` on `billbook` | **Low (Good)** | Fixed in `267961c` / `6b5562f` by adding Firebase Auth (`Email/Password`) + `?auth=<idToken>` |
| `familyroot/index.html` (`raj-family-33299`) | Firebase Auth not initialized; `handleLogin()` checks `email + mobile` against Firestore `familyTree` | **High** | Requires migrating `familyroot/index.html` to Firebase Auth + Firestore Security Rules (`request.auth != null`) |

---

## 3. Recommended Safe Rollout Plan (Per App)

1. **`Shalom` (`store.shalomconnect.in`)**:
   - Move OTP generation/verification out of client-readable RTDB `otps/{phone}` into a Cloud Function or Firebase Phone/WhatsApp Custom Token flow (already partially present in `whatsapp-auth.js`).
   - Restrict `customers/{phone}` and `orders/{orderId}` reads to `request.auth != null && (request.auth.uid == ... || request.auth.token.admin == true)`; allow `create` on `orders` with schema validation, disallow public `read`/`list` of all customers.
2. **`prayforindia` (`pray.shalomconnect.in`)**:
   - Keep public `GET` on approved prayers (`prayers`).
   - Require Firebase Auth (`auth != null` + admin claim) for `admin.html` (`PATCH`/`DELETE` moderation), and validate public prayer submissions (`newData.hasChildren(['text', 'createdAt'])`, disallow `DELETE`/overwrite of existing keys).
3. **`school` (`school.shalomconnect.in`)**:
   - Wire `school-sync.js` to Firebase Auth ID tokens (`?auth=<idToken>`) for `school_admin.html`, `super_admin.html`, `teacher_staff_app.html`, and `student_parent_app.html`, then enforce `auth != null` + role claims in `database.rules.json`.
4. **`rajfamily` (`family.shalomconnect.in`)**:
   - Initialize Firebase Auth on `raj-family-33299` (Email/Password or Phone), replace the hardcoded client admin check in `familyroot/index.html`, and lock Firestore `familyTree` to `request.auth != null`.

---

## 4. Testing Procedure Before Production Rule Deployment

1. Back up current live rules from Firebase Console (`adonaibroadcast-11095` & `raj-family-33299`).
2. Test updated rules + frontend auth changes in **Firebase Emulator Suite** (`firebase emulators:start --only database,firestore,auth`).
3. Verify public storefront/prayer flows succeed and unauthorized `GET`/`PUT`/`DELETE` on customer/order/student nodes return `401/403`.
4. Obtain owner approval before publishing rules to production.
