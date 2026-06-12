---
name: testing-mebelpro
description: Test the MebelPro furniture-management single-file SPA (index.html) end-to-end — registration/auth validation, password UX, and role dashboards. Use when verifying UI/UX or auth changes in this repo.
---

# Testing MebelPro

MebelPro is a **single-file SPA** (`index.html`) with no backend. State persists in `localStorage`. There are three roles: buyer (oluvchi), seller (sotuvchi), admin.

## Running it
- Open directly in Chrome: `file:///<abs-path>/index.html`. No build/server needed.
- To reset state between runs: log out (Chiqish), or clear the page's localStorage. A fresh session shows the auth screen.

## What to test (auth/registration is the high-value area)
Register tab ("Ro'yxatdan o'tish"):
- Password strength meter updates live: short/simple → red "Zaif parol"; long+mixed → green "Kuchli parol".
- Eye toggle reveals/hides password (icon 👁️↔🙈).
- Invalid phone (e.g. `+123`, <7 digits) → toast "Telefon raqam noto'g'ri!" + red field; registration blocked.
- Mismatched confirm password → toast "Parollar mos kelmadi!" + red field; registration blocked.
- Valid input → success toast + lands on "Mebel Katalogi" as the new buyer.

Regression:
- Login tab: the newly registered username/password logs in (proves persistence).
- Admin: click "⚙️ Admin kirish", enter demo password `admin123`, Enter → Admin Dashboard.

## Gotchas / tips
- **CDP vs recorded window mismatch:** `browser_console` (CDP at localhost:29229) may attach to a DIFFERENT Chrome target than the one the `computer`/screenshot tool records (e.g. innerWidth 1600 vs a 1024-wide recorded window). Symptom: DOM changes you make via console (or modal `display:flex`) don't appear in screenshots. Do NOT conclude the app is broken from this. Verify flows via clicks + screenshots in the recorded window and judge by the resulting page state.
- The admin modal markup is always present in the stripped DOM dump regardless of whether it's visible; don't infer "open" from the DOM dump. If a modal doesn't visibly appear in a screenshot, test it functionally (click trigger, type, submit) and check the outcome page.
- The app is Uzbek-language; assert on the literal Uzbek toast/label strings above.
- Passwords are stored in plaintext in localStorage (demo app) — expected, not a defect.

## Devin Secrets Needed
- None. Fully local, no external services. Admin demo password is `admin123` (in-app, not a secret).
