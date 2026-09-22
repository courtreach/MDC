# Setting up this chamber app — one-time, about 30 minutes

No terminal, no code editor. Everything is done in three websites: **GitHub** (where the
app lives), **Firebase** (where the chamber's data lives) and the app itself.

Each chamber has its **own** copy of this app and its **own** Firebase project, so its
matters, day sheets and members are never in the same database as any other chamber's.

## 1. Firebase project (the database)

1. Go to https://console.firebase.google.com → **Add project** → name it after the chamber
   → Continue (Google Analytics can be off) → Create.
2. Left menu **Build → Authentication → Get started → Email/Password → Enable → Save**.
3. Left menu **Build → Firestore Database → Create database → Start in production mode**,
   location **asia-south1 (Mumbai)** → Create.

## 2. Security rules (what each member may see and change)

Firestore Database → **Rules** tab. Delete what is there, paste the whole contents of
`firestore.rules` from this repository, and **change one line first**: near the top,
`isAdminEmail()` has `'admin-email@example.com'` — put the chamber admin's email there,
**all lower-case**, inside the quotes. Then **Publish**.

## 3. Connect the app to the project

Firebase console → gear icon → **Project settings** → scroll to **Your apps** → the `</>`
(web) icon → nickname "Chamber" → Register app. It shows `firebaseConfig` with six values.

In GitHub, open `index.html` → pencil (Edit) → find the block near the top that says
`PASTE-apiKey-HERE` and paste each of the six values over its placeholder (keep the
quotes). **Commit changes.**

## 4. The admin's email

In the same `index.html`, a few lines above, `adminEmail: "ADMIN-EMAIL@example.com"` — put
the same email as in step 2. **Commit changes.** (The admin is recognised by this email
the very first time they sign in, so nobody has to approve them.)

## 5. Publish the app

GitHub → the repository's **Settings → Pages** → Source: *Deploy from a branch* → Branch:
**main**, folder **/ (root)** → Save. A minute later the site address appears at the top
of that page (`https://<account>.github.io/<repository>/`). That is the app.

## 6. First sign-in and the chamber's details

Open the app on a phone or computer → **Set your password** → the admin's email → choose a
password. The app opens as admin and asks for the **Chamber details** (Senior's name,
designation, court). These are shown on the sign-in card, the sidebar and every printout,
and can be changed any time from **Chamber → Chamber details**.

Then **Chamber → Add member** for the staff and colleagues: name, email, role. Each of
them signs in with that email and "Set your password" — no approval step.

## 7. The Supreme Court cause list (automatic bench and case lookup)

GitHub → **Settings → Actions → General → Workflow permissions → Read and write
permissions → Save.** Then the **Actions** tab → *Fetch SC cause list* → **Run workflow**
once. From then on it runs itself every hour on court days (see CAUSELIST-SETUP.md).

## 8. App icon (optional)

The icons show "SA". To use the Senior's initials, run on any Mac:
`python3 make-icon.py XY` (XY = the initials) and commit the three PNG files. An installed
phone shortcut keeps its old icon until removed and re-added.

---

**Keeping the app up to date:** improvements are made in the shell repository and copied
into each chamber's copy by the person who maintains it; the chamber's data is untouched
by an update.
