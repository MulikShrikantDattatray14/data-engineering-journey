# SQL — General Rules, Syntax & Lessons Learned

A living, cross-day revision reference for **new insights explicitly identified by the learner during independent SQL practice**. Keep source links and question IDs. Do not confuse a newly learned rule with an entire topic being mastered.

## SQL-R001 — NULL comparisons and WHERE filtering

**First learned:** 2026-11-06 · Day 1 · Slot 1 · Q1 (paid Maharashtra orders)  
**Category:** SQL filtering · NULL · three-valued logic  
**Type:** General SQL rule  
**Source:** [Original Q1, first attempt, and review](../../10-learning-journal/sessions/2026-11-06/slot-01-sql.md)

### Learner's recorded takeaway (verbatim)

```text
Your condition amount > 1000 evaluates to UNKNOWN when amount is NULL. Since WHERE retains only rows whose condition is TRUE, order 104 is excluded automatically.

You do not need an additional amount IS NOT NULL condition for this query.
```

### Reusable rule / syntax

For a regular SQL comparison such as `amount > 1000`, a `NULL` input produces **UNKNOWN**, not TRUE. A `WHERE` clause filters out both FALSE and UNKNOWN. Therefore, **the predicate alone excludes NULL values** in this situation; adding `AND amount IS NOT NULL` would be redundant.

```sql
SELECT order_id, amount
FROM orders
WHERE amount > 1000;
```

If instead the goal is to **explicitly find missing amounts**, use:

```sql
SELECT order_id
FROM orders
WHERE amount IS NULL;
```

**Boundary:** This applies to ordinary comparison predicates; do not generalize that *every* SQL expression automatically excludes NULL, because `IS NULL` and other operators/functions have different behavior.

**Practice outcome:** Q1 independently solved and reviewed; rule noted for spaced revision. No PNP question or topic mastery automatically credited.

---

## Future entries

Add each new student-submitted learning point here with a stable rule ID, date, slot, question, original wording, validated general rule, representative syntax, a caveat if needed, and a link to the exact question archive. Optional: student may explicitly say **No new learning** and continue without creating an entry.


## SQL-R002 — Mandatory conditions across OR branches

**Date:** 2026-11-06 | **Day 1 Slot 1 Q2** | **Category:** SQL Boolean logic / NULL / WHERE
**Learner explicitly confirmed after review:** Q2's explanation is important new learning.
**Question:** [Q2 session and both learner attempts](../../10-learning-journal/sessions/2026-11-06/slot-01-sql.md)

### Rule
SQL evaluates the **entire WHERE expression**. AND needs both conditions TRUE; OR needs at least one TRUE. AND has higher precedence than OR unless parentheses specify another grouping.

For this expression:

```sql
WHERE (status = 'paid' AND state = 'Maharashtra')
   OR amount > 2000
```

A paid Maharashtra row with NULL amount passes: the first branch is TRUE, the second is UNKNOWN, and TRUE OR UNKNOWN is TRUE.

**If a requirement must apply to every OR branch, group the OR alternatives and place the mandatory condition outside with AND:**

```sql
WHERE ((status = 'paid' AND state = 'Maharashtra') OR amount > 2000)
  AND amount IS NOT NULL
```

This syntax works in SQLite and SQL Server. The student originally repeated IS NOT NULL within both branches; that correction was valid, while this grouped version is shorter. WHERE only retains TRUE, not FALSE or UNKNOWN.

**Recall:** Would a paid row with NULL amount pass `status = 'paid' OR amount > 2000`?

**Source:** [Verified expected vs actual Q2](../practice/verified-results/2026-11-06-q01-q02.md). Learner requested this new learning **after** previously choosing No for Q2; this later explicit request overrides No. No extra course problem completion is credited.


## SQL-R003 — Check syntax and requirements before submitting

**Date:** 2026-11-06 · Day 1 · Slot 1 · Q3  
**Classification:** Practice habit / submission checklist, with related syntax reminder  
**Source:** [Q3 original attempted query and review](../../10-learning-journal/sessions/2026-11-06/slot-01-sql.md)

### Learner's exact reflection (verbatim)

```text
yeah i know it should not be sort by but its should be order by ..i did this mistake bcz i didnt recheck question before submitting . i hurried while submitting , so my learning is i should not hurry.
```

### Reusable reminder

The learner **knew** the correct SQL keyword but rushed and wrote `SORT BY`. In both SQLite and SQL Server, the sorting clause is `ORDER BY`, not `SORT BY`.

**20-second pre-submit check:**
1. Reread the required columns, filters, joins, sorting, and unmatched-row behavior.
2. Scan the query for invalid syntax, especially `ORDER BY` and aliases.
3. Run the query when possible and compare its actual output to the expected rows before submitting.

This records a learner-identified process mistake, **not** a new JOIN misconception or a PNP completion.

---

### Q4 reinforcement — same learner-identified habit (2026-11-06)

**Original Q4 reflection, verbatim:**

```text
same learning as previous question, i hurried up without rechecking,
```

The Q4 original query mistakenly used the digit `0` in `0.status` rather than the letter `o` from the orders alias. The learner explicitly connected this to rushing, the same preventable behavior identified in Q3. This is an additional **Q4 occurrence of SQL-R003**, not a new rule.

**Q4 source:** [Day 1 Slot 1 Q4](../../10-learning-journal/sessions/2026-11-06/slot-01-sql.md).


## SQL-R004 — LEFT JOIN: ON versus WHERE filtering

**Date:** 2026-11-06 · Day 1 · Slot 1 · Q5  
**Category:** Join semantics / filtering / NULL  
**Related attempt:** [Q5 original query, expected vs actual, and corrections](../../10-learning-journal/sessions/2026-11-06/slot-01-sql.md)

### Exact learner-chosen takeaway (verbatim)

```text
filters the joined result after the JOIN.

For Ravi, the matching order is cancelled, so it is removed. For Kabir, there is no matching order, so o.status is NULL, and the condition evaluates to UNKNOWN. That row is removed too.

The crucial distinction:
- ON controls which orders match each customer during the JOIN.
- WHERE filters the rows that remain after the JOIN.
```

### Generalized rule (assistant explanation)

**With an outer join, choose WHERE a right-table filter is placed based on whether unmatched left-table rows must survive.**

- A right-table predicate in the `ON` clause controls **which right rows match**, while `LEFT JOIN` still preserves every left row by supplying NULLs when no match qualifies.
- A right-table predicate in the `WHERE` clause filters **the completed joined rows**. A condition such as `WHERE o.status = 'paid'` rejects NULL-extended rows (`UNKNOWN`) and non-paid matches (`FALSE`), so customers without paid orders disappear.
- **If you need every customer but only paid order details**, place `o.status = 'paid'` in `ON`. **If you need only customers with paid orders**, put that condition in `WHERE` (or use INNER JOIN appropriately).

```sql
-- Preserve all customers; attach only paid orders
SELECT c.customer_id, c.customer_name, o.order_id
FROM customers AS c
LEFT JOIN orders AS o
  ON c.customer_id = o.customer_id
 AND o.status = 'paid';
```

**Nuance:** This is not a universal claim that `WHERE` always turns a LEFT JOIN into INNER JOIN. It applies to NULL-rejecting right-table conditions such as `o.status = 'paid'`. Conditions like `WHERE o.order_id IS NULL` deliberately select unmatched rows instead. SQL logical processing considers JOIN/ON before WHERE.

**SQLite and SQL Server:** The demonstrated syntax and behavior apply to both. This is a new confirmed learning entry, not a new PNP question completion.
