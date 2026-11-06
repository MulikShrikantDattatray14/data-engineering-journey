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
