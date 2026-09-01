# dmless — Hiring Automation MVP

A self-screening hiring tool. Recruiters create links with 5 knockout MCQs. Candidates screen themselves. Only the best reach the inbox.

---

## 🚀 Running Locally

```bash
npm install
npm run dev
```

Visit `http://localhost:3000`

---

## ☁️ Deploying to Vercel

### Step 1: Push to GitHub

```bash
git init
git add .
git commit -m "dmless MVP"
git remote add origin https://github.com/YOUR_USER/dmless.git
git push -u origin main
```

### Step 2: Import on Vercel

1. Go to [vercel.com/new](https://vercel.com/new)
2. Import your GitHub repository
3. Framework: **Next.js** (auto-detected)
4. Click **Deploy**


## 📁 Architecture

```
src/
  app/
    page.tsx                          Landing page
    signup/ login/                    Auth pages
    dashboard/
      page.tsx                        Recruiter dashboard
      job/[id]/candidates/page.tsx    ← NEW: Shortlisted candidates view
    create-job/ edit-job/[id]/        Job management
    job/[id]/                         Candidate screening flow
    api/
      auth/signup|login|me/           Authentication
      jobs/
        route.ts                      List/create jobs
        [id]/route.ts                 Get/edit/toggle job
        [id]/candidates/route.ts      ← NEW: GET shortlisted candidates
      candidates/
        job/[id]/                     Public job info (no auth)
        check/                        Attempt limit check
        submit/                       MCQ submission
        submit-check/                 Per-question knockout check
        upload/                       Resume upload
        [id]/decision/route.ts        ← NEW: PATCH hire/reject decision
  lib/
    db.ts                             File-based JSON persistence
    auth.ts                           Session cookie helpers
data/
  db.json                             Local database (gitignored)
```

---

## ✨ Features

- **Knockout MCQs** — wrong answer = instant rejection, no retries by default
- **Timer** — recruiter can set time limit per test
- **Attempt limits** — recruiter controls max attempts per candidate
- **Analytics** — funnel chart, MCQ failure rates, pass rate
- **Edit jobs** — change MCQs, description, timer, attempt limit
- **Candidates view** — review shortlisted candidates, hire or reject
- **Persistent DB** — JSON file survives dev server restarts

