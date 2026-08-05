# Finalise vetting — interface concept (Objective Build)

Clickable concept for streamlining the vetting-outcome capture in Objective Build.
Static single-page prototype. No build step, no dependencies, no backend.

> **Concept demonstration only. Does not conform to the Objective Design Language.
> Commercial in confidence.**

---

## Before you deploy — read this

A Vercel deployment on the **Hobby** plan is a **public URL**. Anyone who has the link
can open it; there is no login. Vercel's password protection / SSO gating is a
**Pro or Enterprise** feature.

This prototype carries a "Commercial in confidence" marking and mimics a customer-facing
product UI. If that combination is not acceptable, use one of these instead:

| Option | Access control | Notes |
|---|---|---|
| Vercel Hobby | None — public link | Fine if you accept the link may be shared |
| Vercel Pro + Deployment Protection | Password or SSO | The only option that actually restricts access |
| Send the `.html` file directly | Recipient-controlled | No hosting, no URL to leak |

This repo already sets `noindex, nofollow, noarchive` (via `vercel.json` headers, a
`<meta name="robots">` tag, and `robots.txt`). That keeps it out of search results.
**It does not make the URL private.**

---

## Deploy

### Option A — drag and drop (fastest)

1. Zip this folder (or use the zip you were sent).
2. Go to https://vercel.com/new
3. Drag the folder/zip onto the drop zone.
4. Framework preset: **Other**. Build command: leave empty. Output directory: leave empty.
5. Deploy.

### Option B — Vercel CLI

```bash
npm i -g vercel        # once
cd proto-vetting-finalise
vercel                 # preview deployment
vercel --prod          # production
```

When prompted: no build command, output directory `.` (project root).

### Option C — Git

```bash
git init
git add .
git commit -m "Finalise vetting concept prototype"
git remote add origin <your-repo-url>
git push -u origin main
```

Then import the repo at https://vercel.com/new. Vercel detects a static site and
deploys `index.html` as-is.

---

## Turning on password protection (Pro plan)

Vercel dashboard → your project → **Settings → Deployment Protection**
→ **Password Protection** → set a password → Save. Applies to all deployments.

---

## What's in here

| File | Purpose |
|---|---|
| `index.html` | The entire prototype — HTML, CSS and JS inline |
| `favicon.svg` | Browser tab icon |
| `robots.txt` | Blocks crawlers |
| `vercel.json` | `noindex` + security headers, no-cache so reviewers always see the latest |
| `.gitignore` | Excludes `.vercel`, OS cruft |

No `package.json` — deliberately. Adding one would make Vercel attempt a build step
this project doesn't need.

The only external request is the Inter webfont from Google Fonts. If your reviewers
are behind a proxy that blocks it, the page falls back to the system sans-serif;
layout is unaffected.

---

## Demoing it

1. Click **Finalise** (top right).
2. Choose an outcome. `Accepted and lodged` reveals the planning-team selector;
   `Returned` and `Withdrawn` do not.
3. The date defaults to today. Pick an earlier date to see the backdating warning.
4. **Finalise** → step 2 shows a summary of the decision → **Confirm**.

**Demo state controls** (bottom left):

- **Already forwarded: No / Yes** — flips whether the application has already been
  forwarded. With `Yes`, the team selector is replaced by a read-only notice, per the
  acceptance criteria.
- **Reset** — returns the application to *In progress* so you can run the flow again.

Both controls are prototype scaffolding, not proposed UI.

---

## What the concept changes

- Three modals (Finalise → Forward → Confirm) reduced to two: one decision-capture
  step, one confirmation.
- Two separate internal-note fields collapsed into one note recorded against the decision.
- Adds the decision date, defaulted to today, constrained to today or earlier, with an
  explicit warning of the statutory consequence when backdated.
- Planning-team selection appears only when accepting and lodging **and** the
  application has not already been forwarded.
- The confirmation step now summarises what is about to be committed, instead of
  asking "Are you sure?" with nothing on screen.

## Known open questions

- The internal file note is optional for all three outcomes. Arguably it should be
  mandatory for `Returned` and `Withdrawn`, where the reason is what gets contested later.
- Team selection is mandatory when shown. The acceptance criteria say "presented a
  list", not "must choose".
- Outcome labels and date labels are NSW-shaped. For reuse in Victoria, Queensland or
  New Zealand (resource consents) these need to be configuration, not hard-coded values.
