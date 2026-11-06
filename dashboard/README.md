# Data Engineering Progress Dashboard

A responsive, zero-build, browser-based website for the **₹30–40 LPA aspirational Data Engineer/Data Platform Engineer preparation campaign**.

## Website
When GitHub Pages is enabled with **Settings → Pages → Build and deployment → Source: GitHub Actions**, the expected project URL is:

`https://mulikshrikantdattatray14.github.io/data-engineering-journey/`

**This URL is expected, not verified live until GitHub Pages successfully deploys.** The site is served from `dashboard/index.html`, which becomes the Pages root artifact through `.github/workflows/deploy-de-dashboard.yml`.

You can also open `dashboard/index.html` locally in any modern web browser.

## Live data sources

| Information | Where it comes from | Refresh |
|---|---|---|
| 157-date campaign (Nov 6 kickoff + original 156 planned study dates) | Repository 1 `progress/daily-progress.json` | Every five minutes and via Refresh button |
| Completed source SQL IDs | `daily[].sql.completed_ids` in Repository 1 | Same |
| Previously solved 20 SQL questions | `baseline.sql_previously_solved` | Same |
| Python pages actually completed | `daily[].python.completed_pages` | Same |
| Reviewed learning, actual focus time, reflections | Daily progress fields | Same |
| Recent Repository 1 commit | Public GitHub commit API | Same |
| Recent Repository 2 commit | Public GitHub commit API | Same |
| Six-month roadmap & salary evidence gates | Explicitly documented dashboard policy + current plan | On website commit/deploy |

**Important truthfulness rule:** GitHub pushes only update activity telemetry. An edited problem file does not automatically prove that a question was attempted, correct, reviewed or mastered. Real credit requires explicitly reviewed progress records. There is no guesswork based on commit counts, filenames, file sizes, PDF views or code lines.

The GitHub Pages site does not have write access to GitHub. To log progress, review an attempt and commit the real evidence to the designated progress JSON, preferably using the existing progress update process. Do not mark future days complete. Daily source IDs/pages stay grounded in the tracker and the November 22 sprint.

## Why five-minute auto-refresh instead of instant webhooks?

This is a secure, free, static public site with no always-running server or authentication secrets. Fetching public GitHub data on an interval works without any personal access token. GitHub may delay content via caching or temporarily rate-limit API calls, so the dashboard displays partial/stale data warnings instead of inventing freshness. Refresh starts a new fetch; there is no guarantee of sub-second updates.

## What is tracked

- Overview: study wins, SQL/205, Python/80, actual focused hours.
- Daily: selected date, original SQL IDs, Python source pages, 25% × 4 target score, reflection and actual minutes.
- Timeline: all 157 study dates; no false completions.
- Central roadmap: source sprint to Nov 22, SQL+Python mastery by Dec 31, modeling/ETL, Spark/cloud, projects, interview readiness and applications. PNP mentor's sequence has priority when provided.
- Career readiness: skills and interview evidence gates are **not yet verified** until explicit project and mock logs exist.
- Sources: latest main-branch commit messages from both repositories; activity is not equivalent to mastery.

## Dates / source-of-truth nuance

- `progress/daily-progress.json` now begins **November 6, 2026 (Day 1 kickoff)** and contains 157 dated entries. The original 156 planned curriculum entries are retained from November 7 onward as Days 2–157, with the same source tasks and final date. November 6 records seven reviewed tutor-created SQLite questions (Q1–Q7), three independently correct/corrected (Q1, Q2, Q7), and links to the dated session archive. It does **not** invent PNP completions, Python PDF completions, study minutes, or a daily win.
- The aspirational 10h schedule is a stretch. The dashboard deliberately records actual study time separately.
- `SPRINT-NOV-22.md` supersedes the older 100-day SQL and 77-day Python source deadlines.
- Salary ₹30–40 LPA is a target, not a forecast or guarantee.
- The provisional January–May phase descriptions are **execution recommendations**, not a claim to reproduce an unavailable exact PNP mentorship roadmap. Update the roadmap when verified mentor notes arrive.

## Privacy and operations
Both tracked repositories are public. Never commit credentials, personal contact details, paid course notebooks, or real customer information into progress notes. The site contains no API secrets. API reads are public and rate-limited. There is no login or browser-side write-back.

## Developer check
No framework or build step is required. Edit `dashboard/index.html`, open locally, validate the embedded JavaScript, commit to `main` and allow GitHub Pages deployment. The old `PROGRESS-DASHBOARD.md` remains available as a Markdown report; this website is a visual companion, not a destructive replacement.

## First deployment status (checked 6 November 2026)

The deploy workflow was pushed successfully but its initial run **failed during `actions/configure-pages`** with `Get Pages site failed ... Not Found`. This means the repository has not had GitHub Pages enabled yet; the website code was not rejected by a build step.

**One-time owner action:** Visit [Repository Settings → Pages](https://github.com/MulikShrikantDattatray14/data-engineering-journey/settings/pages), choose **GitHub Actions** as the build source. Then visit [Actions → Deploy Data Engineering Progress Dashboard](https://github.com/MulikShrikantDattatray14/data-engineering-journey/actions/workflows/deploy-de-dashboard.yml) and use **Run workflow** if GitHub does not redeploy automatically. Once the workflow succeeds, use the Pages URL GitHub reports. The live site is not asserted active before that succeeds.

No repository secret or PAT is necessary for normal publishing. Do not add an access token to the public static website.


## Nov 6 launch day and separate practice telemetry

The website's **Today's targets** and **Daily targets** now show November 6 as an actual selectable Day 1. Its `practice` object is independent of scored PNP/Python curriculum fields and displays: seven tutor questions reviewed, three independently correct/corrected, and the closing Q7 checkpoint. Study-day wins remain based on reviewed source task requirements, Python progress and reflection; those are not inferred from GitHub commits. November 7 remains available, relabeled Day 2. If your browser still shows an old cached dashboard, reload the site and press **Refresh** in the dashboard.


## Daily revision links and practice progress (November 6 update)

The **Daily targets** view now includes distinct sections for **guided SQL diagnostic progress**, **each reviewed question**, and **concepts studied**. Question links open [the November 6 per-question GitHub revision index](../10-learning-journal/sessions/2026-11-06/PRACTICE-INDEX.md), which points to exact attempted SQL, actual output comparisons and references. Concept links open SQL-R001–SQL-R006 rules and detailed lessons. Future dated records can use the same `daily[].practice.questions` and `daily[].practice.concepts` data fields.

The overview and daily scoring panel display **7/8 guided tutor questions reviewed** and **3/7 independently correct or corrected** on November 6, with an explicit explanation that these are *separate* from official PNP/Python source-completion credits. In the timeline and day list, the date shows guided activity even while its official curriculum score is 0%. **Do not change curriculum mastery flags or source-completed IDs just to make the practice meter move.**
