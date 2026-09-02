# IS Career Launchpad

A prototype tool helping incoming BYU Information Systems students explore four IS career
paths and practice interviewing for them.

Built for the **BYU IS Junior Core Case Competition**, Fall 2026.

**Live site:** `https://<your-github-username>.github.io/<repo-name>/`

---

## What it does

**Career Path Discovery** — four paths (Data Analytics, Cybersecurity Analyst, IT Project
Manager, Software Developer). Each covers day-to-day work, technical skills and tools, three
industries that hire for the role and how the job differs between them, what an intern is and
is not expected to know, certifications, salary and growth, and what makes a strong candidate.
Every figure links directly to its source.

**Hands-on activity per path** — a multi-stage exercise showing what the work actually feels
like: auditing a dirty data extract, running an incident investigation, triaging sprint scope
and finding the critical path, and finding a bug then reviewing a pull request.

**Interview Prep** — a five-question mock interview per path (two behavioral, three technical,
interleaved and drawn at random from that path's pools). Free-response answers get automated
feedback plus a model answer side by side.

---

## Running it

Open `index.html` in any browser. That is the whole thing — one self-contained file with no
build step, no server, no dependencies, and no network requests. It works offline.

---

## Deploying to GitHub Pages

The repo is already structured for it. `index.html` is at the root and all paths are relative.

1. Push this folder to a GitHub repository.
2. In the repo, go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**.
4. Set the branch to `main` and the folder to **`/ (root)`**. Save.
5. Wait about a minute, then visit `https://<username>.github.io/<repo-name>/`.

```bash
git init
git add .
git commit -m "IS Career Launchpad"
git branch -M main
git remote add origin https://github.com/<username>/<repo-name>.git
git push -u origin main
```

Notes:

- `.nojekyll` is included so GitHub serves every file as-is rather than running Jekyll over it.
- Navigation uses URL hashes (`#/careers/cybersecurity`), which work on Pages with no server
  configuration and no 404 workaround. Links are shareable and the back button behaves.
- The favicon is embedded as a data URI, so it loads on Pages and from a local file alike.

---

## Repository contents

| File | Purpose |
|---|---|
| `index.html` | The application. Everything is in here. |
| `SPEC.md` | Build specification — architecture, data schemas, scoring design. |
| `DATA-VERIFIED.md` | Every salary and outlook figure with its source, caveats, and the claims not to make from it. |
| `README.md` | This file. |
| `.nojekyll` | Tells GitHub Pages to skip Jekyll processing. |

---

## How the interview scoring works

Free-response answers are scored offline on three signals, combined as a weighted composite:

| Signal | Weight | What it measures |
|---|---|---|
| Keyword coverage | 50% | Whether the answer hits the concepts a strong answer must contain. Each concept is a synonym group, so plain-language phrasing counts. |
| TF-IDF cosine similarity | 30% | How closely the answer resembles the model answer, as vectors over an IDF corpus built from all model answers in the app. |
| Length | 20% | Whether the answer is substantial without rambling. Also acts as a gate, so a short keyword-stuffed answer cannot score well. |

Bands: **Strong** at 0.70 and above, **Developing** at 0.40–0.69, **Needs work** below 0.40.

Feedback is rules-based and names specifics from the candidate's own answer — which concepts
were missed, whether the length was off, and for behavioral questions, which STAR element was
absent.

**A known limitation, stated deliberately:** cosine similarity is noisy on short texts. A
correct answer phrased very differently from the model answer will score lower than it
deserves. That is why it carries only 30% of the composite and never determines the band on
its own.

---

## Sources

Salary, growth, and employment figures come from the U.S. Bureau of Labor Statistics
Occupational Outlook Handbook (May 2025 wages; 2025–2035 projections). Placement figures come
from BYU Marriott School of Business published placement profiles for the Class of 2025.
Internship wage data comes from the NACE 2026 Internship & Co-op Survey. Full citations, access
dates, and the BLS occupation mapping for each role are in `DATA-VERIFIED.md` and on each
career page in the app.

Content was drafted with AI assistance and verified by the team against the primary sources.
