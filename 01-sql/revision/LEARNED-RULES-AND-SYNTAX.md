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
