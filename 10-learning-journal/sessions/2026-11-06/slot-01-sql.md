# Day 1 — Slot 01: SQL Foundations & PNP Practice

**Study date:** November 6, 2026 (Asia/Kolkata)  
**Status:** Interactive session in progress; Q1 reviewed correct, Q2 pending  
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

**Student's written explanation of NULL:** Not yet separately submitted (the assistant supplied the explanation during review).

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
- Errors and important insights: No query errors found; distinguish unknown results of NULL comparisons from TRUE; learner's independent NULL explanation still pending
- Next revision: Pending

**Rule:** Log each original student submission before corrections. Lesson documentation does not equal reviewed mastery.

## Question 2 — AND/OR precedence and NULL diagnostics (awaiting learner)

Using the **same orders table** from Q1, write one PostgreSQL query that returns `order_id`, `status`, `state`, and `amount` for:

- **Either** all `'paid'` orders from `'Maharashtra'` **or** all orders with `amount > 2000`, regardless of state or status.
- Exclude any order with a `NULL` amount.
- Sort by `order_id` ascending.

**Requirement:** Use correct parentheses to make the intended logical grouping explicit. Do not hardcode IDs. In your own words, explain which operator would otherwise take precedence between `AND` and `OR`, and why order 104 must be excluded.

**Student first attempt:** Pending.
**Assistant feedback and expected result:** Withheld until attempt.

**Archive rule:** Record next answer exactly before providing corrections.
