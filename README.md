# Chamber — work allocation and cause list for a Senior Advocate's chamber

A single-file web app (installable on phones) for a chamber's Staff and Colleagues:
the day's cause list, work distribution and workload, the Senior's calendar, briefs,
leave and conferences. Each chamber runs its own copy with its own Firebase project.

**New chamber? Follow `SETUP.md`.** About 30 minutes, no coding.

- `index.html` — the whole app. Personalised from inside the app (Chamber → Chamber
  details); the only code edits are the Firebase keys and the admin's email (SETUP.md).
- `firestore.rules` — the security rules to paste into the Firebase console.
- `fetch_causelist.py` + `.github/workflows/causelist.yml` — fetches the Supreme Court's
  cause lists on a schedule into `court-updates.json` (see CAUSELIST-SETUP.md).
- `sw.js`, `manifest.json`, icons — the installable-app plumbing. `make-icon.py XY`
  regenerates the icons with the Senior's initials.
