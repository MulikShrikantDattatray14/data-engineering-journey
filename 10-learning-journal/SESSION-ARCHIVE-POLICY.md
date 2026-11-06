# Full-Fidelity Study Session Archive — Operating Rules

**Purpose:** Preserve the actual material learned, attempted, reviewed, and discussed in every study slot across the entire Data Engineering journey. This is not merely a summary journal.

## One date → multiple slots → full evidence

Every study date gets its own folder: `10-learning-journal/sessions/YYYY-MM-DD/`.

Each slot is saved as a Markdown session document, for example:

- `slot-01-sql.md`
- `slot-02-python.md`
- `slot-03-sql.md`
- `slot-04-python.md`
- `day-review.md`

Use `slot-NN-topic.md` to accommodate any additional or reordered slots. Each slot document contains:

1. **Actual start and end time** (Asia/Kolkata), target and source links.
2. **Study content as delivered**: original explanations, definitions, analogies, why/how, examples, code snippets, tables and key explanations; preserve wording and order as closely as practical.
3. **Exact original practice prompts from ChatGPT** and input/output constraints (where authored by us), **no answer spoiler** before the attempt.
4. **Learner's original answers and code**, copied exactly as submitted in the learning session. Never silently replace the first attempt.
5. **Feedback as actually given**, including incorrect assumptions, review, edge cases, testing, time/space complexity and subsequent improved code, explicitly versioned.
6. **Active recall and revision notes**: what was hard, what will recur, mixed-concept links and next task.
7. **Outcome metadata**: status planned / in-progress / attempted / reviewed / mastery-verified, evidence links, completed PNP IDs/pages, Bosscoder question IDs, actual focus time.

If a session was interrupted, save the partial material as partial, with open questions carried over. Do not invent content for slots that haven't occurred. Keep corrections distinct from the original explanation if we changed our understanding.

## Original lessons vs third-party course notes

- Save *our own* lesson text and original questions in full. Save the learner's original submitted work, not rewritten as though it was originally correct.
- For PNP/Bosscoder proprietary/paid course questions and classroom notes: retain source link, topic/ID, original independent summary, and the student's solution and review. Do **not** reproduce lengthy copyrighted source text or entire paid class notebooks in the public repository without permission.
- For MCQs, keep four options if provided and authorized for public use, but never reveal correct choices or explanations before the student has attempted the question.
- Do not publish real customer information, internal company code, confidential job details, account numbers, credentials or secret keys. Scrub sensitive details before committing.
- Source Repository 2 stays unchanged unless the learner separately requests an edit. Repository 1 is the central session archive and progress authority.

## Synchronization and dashboard truth

GitHub does **not** automatically ingest ChatGPT conversations. During the study session, the assistant can commit the completed, reviewed material using the connected GitHub integration. If a long verbatim record is required, collect it from the current conversation while it is accessible, confirm completeness and preserve it alongside the structured notes. Do not claim automatic continuous syncing or work after the chat ends.

Only after verifying actual learning update `progress/daily-progress.json`; GitHub commit activity is separate from source exercise completion, reasoning quality and mastery evidence. The website dashboard can then read the new records on refresh.

**Rule: plan ≠ attended; attended ≠ attempted; attempted ≠ reviewed; reviewed ≠ mastered.**

## Optional "What did I learn?" after every question

**After each practice submission is reviewed**, offer an optional prompt: **“Did you learn anything new from this question?”** The learner may choose **No** and move on without explanation, or choose **Yes** and submit their takeaway in their own words. Do not force this step or delay the next challenge if the learner opts out.

When **Yes**: preserve the exact text in the dated slot under that question, tag it as rule/syntax/formula, misconception, strategy, or engineering insight, then create/update a linked entry in the subject's cumulative revision notes (e.g., [SQL learned rules](../01-sql/revision/LEARNED-RULES-AND-SYNTAX.md)). Include question, date, source and any important caveat. Distinguish the student's new takeaway from a response they independently authored *before* seeing feedback.

**No** = record no new rule; it must not reduce question credit or prevent moving forward.

## SQL dialect policy (student choice)

The student's **primary coding dialect is SQLite**. For every SQL question, retain the original SQLite query **exactly as submitted** in a clearly labeled code block. After the first attempt and review, add an independently validated **SQL Server / T-SQL translation** with differences explained when relevant. Label any translation written by the assistant as *assistant-converted*; do not attribute it to the learner.

Only **SQLite and SQL Server** versions should be saved as solutions. Do not create PostgreSQL solution variants. Differences to watch include `LIMIT` versus `TOP`/`OFFSET … FETCH`, date functions, string operations, boolean semantics, null handling, and features not implemented identically. A dialect-independent query can be written identically under both headings, without pretending the student submitted it twice.

Do not generate a SQL Server solution or reveal an answer to an **unattempted** assessment question. Save the prompt and await the student's SQLite attempt first. Study notes may explain syntax without pre-solving assessment questions.

## Expected vs actual SQL results — mandatory after every submission

For each **submitted** SQLite SQL question, record the original query verbatim before making corrections. With a provided schema and fixture, **execute that exact query in SQLite** and show two labeled result tables: **Expected output** (from the question's requirements) and **Actual output** (from the submitted query). Highlight extra, missing, incorrectly valued, duplicated, or misordered rows. State any runtime/syntax errors and distinguish actual execution from inferred output. Preserve the first execution and all revisions, do not silently replace evidence.

Compare columns, values, duplicate multiplicity and required ordering; if row order is not specified, compare unordered rows with duplicates preserved. Prefer representative edge cases (NULL, no match, duplicate keys, ties). If executable schema/sample data are missing, say **Not executed — fixture unavailable**; do not pretend to have actual output. SQL Server translations are labeled **assistant-converted, not executed** unless genuinely tested against SQL Server.

After a student's attempt (or corrected retry) has been reviewed, archive an **assistant-verified reference solution** separately in both SQLite and SQL Server (T-SQL), without replacing the student's code. Use **official platform solution** only when the platform's own answer key has actually been supplied and is authorized to be stored; do not call a generated reference solution official. Never pre-reveal the reference solution for an unattempted problem.

After review, retain the optional Yes/No **New learning?** prompt. Store Yes submissions verbatim in the slot and shared rulebank; No creates no new rule. A submitted question's output comparison is evidence for an attempt, **not automatically a mastered topic or an extra PNP question credit**.

## Progressive teaching of every reviewed reference solution

For every practice problem **after the learner submits an attempt**, create a detailed solution walkthrough, not merely a final query: (1) explain why this technique solves the business requirement and the learner's mistake, (2) use one consistent sample dataset, (3) build the query in small logical steps (start table, JOIN, ON qualification, WHERE, sorting or aggregation as applicable), (4) show the **actual executed SQLite output of each intermediate step**, with row counts and what changed, (5) explain correctness, NULL behavior, duplicates, edge cases and a generalizable pattern, (6) include the original student's unchanged attempt, expected-versus-actual comparison, the assistant-verified SQLite reference and separately labeled SQL Server/T-SQL equivalent, (7) link the optional learner-confirmed insights into the reusable rules bank. If a step is not executable, mark it as illustrated/inferred rather than executed. Never expose answer keys for unattempted questions or label assistant-authored references official platform keys. Full example: [Q6 progressive walkthrough](../01-sql/practice/verified-results/2026-11-06-q06-walkthrough.md).

## Guided, student-led step-by-step SQL workflow (starting Q7)

Starting Day 1 Slot 1 Q7 and for subsequent SQL problems, **do not begin with a final-solution submission form**. Present the problem and full sample data, then invite the learner to choose and explain **one next reasoning/coding step** in their own words and submit its **partial SQLite query**. For each step:

1. Preserve the learner's exact reasoning and incremental SQLite query separately, labeled Step 1, Step 2, etc., with question/date and no retrospective rewriting.
2. Execute **that submitted intermediate query** in SQLite against a consistent, reproducible sample fixture and display its **actual output or actual execution error**; explain what the output means relative to the learner's intended step and the question.
3. Ask the learner what step they want to do next; offer a small, answer-neutral prompt if they're stuck. Do **not** complete the remaining steps or leak the final solution.
4. Only after the learner decides their steps form a complete answer, present a **separate final solution submission**. Execute their final query, compare full expected vs actual, then explain the official-key-versus-assistant-reference distinction, archive detailed SQLite and separately labeled SQL Server reference solutions, and offer optional new-learning capture.
5. Record step output as **executed** only when it was really run; otherwise explicitly mark it not executed. SQLite is the primary dialect, not PostgreSQL. Include duplicate and NULL behavior in output reviews.

The goal is visible reasoning development and learner autonomy, **not** giving a complete reference answer before final submission.
