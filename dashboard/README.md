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
| 156-day SQL/Python targets | Repository 1 `progress/daily-progress.json` | Every five minutes and via Refresh button |
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
- Timeline: all 156 study dates; no false completions.
- Central roadmap: source sprint to Nov 22, SQL+Python mastery by Dec 31, modeling/ETL, Spark/cloud, projects, interview readiness and applications. PNP mentor's sequence has priority when provided.
- Career readiness: skills and interview evidence gates are **not yet verified** until explicit project and mock logs exist.
- Sources: latest main-branch commit messages from both repositories; activity is not equivalent to mastery.

## Dates / source-of-truth nuance

- `progress/daily-progress.json` starts on **November 7, 2026**, with Friday rest days (156 study entries). The **Nov 6 holiday target** appears as a separate overlay drawn from `DIWALI-HOLIDAY-SPRINT-NOV-6-9.md`; it currently has no verified completion record.
- The aspirational 10h schedule is a stretch. The dashboard deliberately records actual study time separately.
- `SPRINT-NOV-22.md` supersedes the older 100-day SQL and 77-day Python source deadlines.
- Salary ₹30–40 LPA is a target, not a forecast or guarantee.
- The provisional January–May phase descriptions are **execution recommendations**, not a claim to reproduce an unavailable exact PNP mentorship roadmap. Update the roadmap when verified mentor notes arrive.

## Privacy and operations
Both tracked repositories are public. Never commit credentials, personal contact details, paid course notebooks, or real customer information into progress notes. The site contains no API secrets. API reads are public and rate-limited. There is no login or browser-side write-back.

## Developer check
No framework or build step is required. Edit `dashboard/index.html`, open locally, validate the embedded JavaScript, commit to `main` and allow GitHub Pages deployment. The old `PROGRESS-DASHBOARD.md` remains available as a Markdown report; this website is a visual companion, not a destructive replacement.
