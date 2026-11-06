# Day 1 — Slot 01: SQL Foundations & PNP Practice

**Study date:** November 6, 2026 (Asia/Kolkata)  
**Status:** Interactive session in progress; Q1 correct, Q2 corrected and reviewed (5/5)  
**Actual start/end and verified focus minutes:** Not recorded  
**Goal:** Rebuild accurate foundations, use independent queries to demonstrate fluency, then revisit the existing PNP SQL 205-question bank without duplicating solutions.

## Lesson 1A — How a SELECT query thinks

### Why it matters to Data Engineering
A Data Engineer uses SQL not merely to display rows, but to select clean records for data transformations, validate incoming batches and build reliable aggregations. A simple filtering mistake can silently include cancelled, null or out-of-range records in a production metric.

### Core concepts to demonstrate
- `SELECT`: choose output columns; `FROM`: choose a table or relation.
- `WHERE`: keep rows satisfying a condition. Understand `=`, `<>`, `>`, `>=`, `<`, `<=`.
- Boolean logic: `AND` requires both conditions, `OR` either condition; use parentheses to make mixed conditions explicit.
- SQL `NULL` represents an absent/unknown value, not a normal value you can compare with `=`. `IS NULL` and `IS NOT NULL` are the appropriate checks.
- SQL filtering uses three-valued logic: TRUE, FALSE, UNKNOWN. A `WHERE` clause retains only TRUE.
- `ORDER BY` controls sort order; `LIMIT` (PostgreSQL) limits returned rows. A relational result is not guaranteed to have a particular order without explicit ordering.
- We will revisit joins, aggregation, duplicate amplification and multi-concept SQL after these foundations are validated.

### Dialect for this practice
Use **PostgreSQL** syntax in the interactive lesson, so examples and LIMIT/NULL behavior are unambiguous. We can compare SQL Server TOP and other dialects separately later.

## First independent diagnostic: Q1 — Paid Maharashtra orders

You are given an `orders` table:

| order_id | customer_id | status | amount | state |
|---:|---:|---|---:|---|
| 101 | 1 | paid | 1200 | Maharashtra |
| 102 | 2 | paid | 500 | Karnataka |
| 103 | 3 | cancelled | 2200 | Maharashtra |
| 104 | 1 | paid | NULL | Maharashtra |
| 105 | 4 | paid | 1800 | Maharashtra |
| 106 | 5 | pending | 2600 | Maharashtra |

**Your task:** Write one PostgreSQL query returning only `order_id` and `amount` for rows whose `status` is `'paid'`, `state` is `'Maharashtra'`, and `amount` is strictly greater than `1000`. Sort by `amount` descending. Do not hardcode order IDs or answers. Explain why a missing amount must not be included.

**Student's original first attempt (preserved exactly, no formatting edits):**

```sql
SELECT order_id , amount
FROM orders
WHERE status = 'paid' and  state = 'Maharashtra' and amount > 1000
order by amount desc
```

**Review:** 5/5 explicit query requirements satisfied. Valid PostgreSQL SQL. `WHERE` checks paid orders, Maharashtra, and amount strictly greater than 1000. `ORDER BY amount DESC` yields order 105 (1800), then order 101 (1200). For order 104, comparison `NULL > 1000` is UNKNOWN, and `WHERE` only retains TRUE. Extra `IS NOT NULL` is unnecessary. Keyword capitalization / line breaks are optional style choices only; student's original retained.

**Learner-confirmed new learning (submitted after Q1 review):** The learner identified the following explanation as their new takeaway, not as a separately authored pre-review answer. It is saved verbatim under the learning entry below.

**Completion credit:** One original tutor diagnostic question reviewed correct; this is **not** a new PNP source ID, not a full slot completion, and not a mastered SQL module.

## Remaining Slot 1 sequence (not yet studied)
1. Q1 complete; Q2/Q3 variants to check `AND`/`OR`, operator precedence, `IS NULL`, and sorting.
2. Short diagnostic on joins and multiplicative duplicates.
3. Reattempt 6–10 selected previously solved PNP SQL questions. Original source questions stay in [Repository 2](https://github.com/MulikShrikantDattatray14/Data-Engineering-Mastry).
4. If rapid and accurate, begin pending PNP IDs `A016`, `P009`, `P013`, `P014`. No new IDs are credited before actual review.

## Progress and revision log
- Actual focused minutes: Unverified
- First attempted query: Q1 submitted and reviewed correct (5/5 requirements)
- SQL source IDs verified today: None
- Errors and important insights: No query errors found; distinguish unknown results of NULL comparisons from TRUE; learner-confirmed NULL/WHERE takeaway recorded separately after feedback
- Next revision: Pending

**Rule:** Log each original student submission before corrections. Lesson documentation does not equal reviewed mastery.

## Question 2 — AND/OR precedence and NULL diagnostics (awaiting learner)

Using the **same orders table** from Q1, write one PostgreSQL query that returns `order_id`, `status`, `state`, and `amount` for:

- **Either** all `'paid'` orders from `'Maharashtra'` **or** all orders with `amount > 2000`, regardless of state or status.
- Exclude any order with a `NULL` amount.
- Sort by `order_id` ascending.

**Requirement:** Use correct parentheses to make the intended logical grouping explicit. Do not hardcode IDs. In your own words, explain which operator would otherwise take precedence between `AND` and `OR`, and why order 104 must be excluded.

**Student's original first attempt (preserved verbatim, including spaces):**

```sql
SELECT order_id, status, state, amount
FROM orders
WHERE  (status ='paid' and state='Maharashtra') or  amount > 2000 
order by order_id
```

**Student's original reasoning (verbatim):**

> Excludes all orders where amount is NULL need not to be handled seperately as where handles that properly where is excludes this automatically .. this thing i learned from question-1

**Review:** 4 of 5 requirements satisfied. The query's `(status='paid' AND state='Maharashtra') OR amount > 2000` admits order 104: the first group is TRUE despite `amount > 2000` being UNKNOWN. The separate universal exclusion of NULL amounts is missing. `ORDER BY order_id` correctly sorts ascending by default. Expected qualifying IDs after fixing the predicate: 101, 103, 105, 106. This is a **reviewed unsuccessful first attempt**, with independent revision pending.

### SQL Server (T-SQL) — assistant translation of the ORIGINAL attempt (same unresolved logic error)

```sql
SELECT order_id, status, state, amount
FROM orders
WHERE (status = 'paid' AND state = 'Maharashtra')
   OR amount > 2000
ORDER BY order_id;
```

**Important:** This is a dialect-equivalent translation of the learner's *original attempt* and **does not fix the NULL problem**. The corrected SQLite and T-SQL solutions will be saved only after the student independently revises the SQLite query. Do not attribute T-SQL to the student.

**Expected-result explanation:** The first Boolean branch can be TRUE even when amount is NULL; WHERE keeps rows whose entire predicate is TRUE, not all rows with a non-NULL amount.

**Optional post-question new-learning prompt:** Ask Yes/No after the revised query is reviewed; if Yes, capture the exact learner text and link to revision bank.

**Archive rule:** Record next answer exactly before providing corrections.

## Optional post-question learning capture — Q1 (learner-submitted)

**Asked-for workflow:** After every future practice submission and its review, ask **“Any new learning from this question?”** with a Yes/No choice. No is valid, optional, and requires no further response. If Yes, collect learner-authored text and save it both in the session archive and the relevant subject-level rule/syntax revision reference; avoid rewriting the learner's text. Any new insight must remain associated with its date, slot, question and source.

**Q1 — Learner's exact reported takeaway:**

> Your condition `amount > 1000` evaluates to `UNKNOWN` when `amount` is `NULL`. Since `WHERE` retains only rows whose condition is `TRUE`, order 104 is excluded automatically.
>
> You do not need an additional `amount IS NOT NULL` condition for this query.

**Classification:** General rule / SQL syntax / three-valued logic.  
**Cross-topic revision reference:** [SQL-R001 — NULL comparisons and WHERE](../../../01-sql/revision/LEARNED-RULES-AND-SYNTAX.md).  
**Q1 review:** Correct query; explanation originally supplied in feedback, subsequently explicitly selected by learner as a new learning.

**Tracking:** Rule recorded, no change to PNP SQL question totals or mastery counts.


### Q1 learning — resubmitted exact wording

```text
Your condition amount > 1000 evaluates to UNKNOWN when amount is NULL. Since WHERE retains only rows whose condition is TRUE, order 104 is excluded automatically.

You do not need an additional amount IS NOT NULL condition for this query.
```

This entry reproduces the learner's subsequent submission exactly; the original formatted entry above is retained for history.

## SQL dialect correction — user preference

From this point onward the student solves every SQL problem **in SQLite**. Following an independent attempt and review, save the original SQLite solution *unchanged* and an assistant-created **SQL Server (T-SQL)** translation. The earlier references to PostgreSQL describe the initial plan and are **superseded**. Do not create PostgreSQL solution versions.

### Q1 SQLite: original student solution (verbatim)

```sql
SELECT order_id , amount
FROM orders
WHERE status = 'paid' and  state = 'Maharashtra' and amount > 1000
order by amount desc
```

### Q1 SQL Server (T-SQL): assistant-converted after student review

```sql
SELECT order_id, amount
FROM orders
WHERE status = 'paid'
  AND state = 'Maharashtra'
  AND amount > 1000
ORDER BY amount DESC;
```

This particular original query is syntactically valid in both dialects; the second version is a readability formatting of the same logic, **not a second learner-authored attempt**. Q2 first and revised SQLite attempts have been preserved, with its reviewed SQL Server translation below.

## Q2 — Learner's revised SQLite solution (verbatim)

```sql
SELECT order_id, status, state, amount
FROM orders
WHERE  (status ='paid' and state='Maharashtra' and amount is not null ) or  (amount > 2000 and amount is not null)
order by order_id
```

**Review:** 5/5 requirements. Both branches reject NULL amounts, logical grouping is explicit, and `ORDER BY order_id` sorts ascending. Correct rows: 101, 103, 105, 106. The `amount IS NOT NULL` check in the second OR branch is redundant given `amount > 2000`, but not incorrect. Original first attempt and its 4/5 review remain preserved above.

### SQL Server / T-SQL — assistant-converted after successful learner revision

```sql
SELECT order_id, status, state, amount
FROM orders
WHERE
    (status = 'paid'
     AND state = 'Maharashtra'
     AND amount IS NOT NULL)
    OR
    (amount > 2000
     AND amount IS NOT NULL)
ORDER BY order_id ASC;
```

**Learning-capture response:** `No new learning to record.` No new rule is added to the centralized SQL revision bank. The correction is retained in this session review.

**Source completion credit:** Q2 is an original tutor diagnostic, not an additional PNP SQL ID. Focus time and complete slot mastery have not been verified.

## Question 3 — LEFT JOIN and missing records (unattempted)

### Tables

`customers`:

| customer_id | customer_name |
|---:|---|
| 1 | Asha |
| 2 | Ravi |
| 3 | Neha |
| 4 | Kabir |

`orders`:

| order_id | customer_id | status |
|---:|---:|---|
| 201 | 1 | paid |
| 202 | 1 | pending |
| 203 | 2 | cancelled |
| 204 | 3 | paid |

**Task:** Write a SQLite query returning `customer_id`, `customer_name`, and `order_id` for **every customer, including customers with no orders**. For each customer, return their matching orders as separate rows, sorted by `customer_id` and then `order_id` ascending. Do not filter by order status.

**Student SQLite attempt:** Submitted and reviewed below; original SQL hit a syntax error at `sort`. Reference query and expected versus actual output documented below.

## Verified SQLite execution and reference-solution archive (Q1 and Q2)

Actual SQLite output, required expected output, comparison tables, and separately labeled SQLite + SQL Server reference solutions are documented in [the Q1–Q2 verification file](../../../01-sql/practice/verified-results/2026-11-06-q01-q02.md). Q1 matched immediately; Q2 initial query had an extra NULL-amount order 104, and Q2 corrected query matched. Original attempts above remain unchanged. Q3 was subsequently attempted and reviewed; see its detailed execution evidence and reference query below.


## Q2 — Learner-confirmed new learning (subsequent update)

After reviewing the Q2 explanation, the learner explicitly requested that its lesson be saved as important **new learning from Q2**, superseding the earlier optional response of "No new learning to record."

**Saved concept:** SQL evaluates the complete WHERE expression; AND takes precedence over OR; TRUE OR UNKNOWN evaluates TRUE; therefore an amount-NULL row may pass via another OR branch. To enforce NULL exclusion for all alternatives, group the OR clauses and append AND amount IS NOT NULL to the whole group. Avoid repeating mandatory filters unnecessarily.

**Permanent learning reference:** [SQL-R002 — Mandatory conditions across OR branches](../../../01-sql/revision/LEARNED-RULES-AND-SYNTAX.md).

This is a learner-approved takeaway from the prior tutor explanation, not a student-authored solution or a new PNP question completion.

## Q3 — Student submission, executed result, reference solutions

**Question status:** First attempt reviewed; syntax error identified; student independent revised submission not yet received.

### Original learner SQLite submission (exactly preserved)

```sql
SELECT c.customer_id, c.customer_name, o.order_id
FROM customers as c
left join  orders as o on   c.customer_id = o.customer_id
sort by c.customer_id,  o.order_id asc 
```

**Original explanation (verbatim):**

> as it asks for every customer, i kept customer table on left

### Execution test

Ran the original query against an actual in-memory SQLite database containing the exact four customers and four orders from Q3. The attempted SQLite query returned:

```text
OperationalError: near "sort": syntax error
```

**Expected output:**

| customer_id | customer_name | order_id |
|---:|---|---:|
| 1 | Asha | 201 |
| 1 | Asha | 202 |
| 2 | Ravi | 203 |
| 3 | Neha | 204 |
| 4 | Kabir | NULL |

**Actual original-query output:** No rows returned (SQLite refused to execute the query). This is an execution error, not an empty result set. Cause: SQL sorting keyword is `ORDER BY`, not `SORT BY`. Join type and ON condition are correct.

### Assistant-verified SQLite reference query (executed)

```sql
SELECT c.customer_id, c.customer_name, o.order_id
FROM customers AS c
LEFT JOIN orders AS o
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id, o.order_id ASC;
```

**Actual output from executing reference:** (1,Asha,201), (1,Asha,202), (2,Ravi,203), (3,Neha,204), (4,Kabir,NULL). Matches expected output.

### Assistant-converted SQL Server (T-SQL) reference query (not SQL Server executed)

```sql
SELECT c.customer_id, c.customer_name, o.order_id
FROM customers AS c
LEFT JOIN orders AS o
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id, o.order_id ASC;
```

**Review:** Correct JOIN design, one syntax mistake; not scored as first-attempt execution success. Preserve a future learner revised attempt separately if submitted.

**Optional post-question new learning:** Await learner Yes/No. No new rule entered without explicit learner confirmation.

**Course tracking:** Q3 is original tutor-created practice, not a new PNP question ID or module mastery.
