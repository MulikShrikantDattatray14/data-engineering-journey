# PNP P004 — Customer emails that cannot be delivered (independent SQL reattempt 4)

**Date:** 2026-11-06 · **Status:** Not attempted in this session.  
**Source:** PNP Q004; previously solved 2026-10-27, so this is a reattempt, **not a new PNP completion**.  
**Original source file (contains solutions; do not open until after the attempt):** [P004 original in Mastry](https://github.com/MulikShrikantDattatray14/Data-Engineering-Mastry/blob/main/1.%20SQL%20Mastery/1.%20SQL%20Mastry/2.PNP-%20foundations%20and%20practice/8.%20Advance%20string%20functions%2C%20regex%20and%20clause/P004.%20Customer%20emails%20that%20cannot%20be%20delivered.md).

## Problem — independently worded summary

A marketing team wants to remove customer email addresses that may cause failed deliveries. Return customers whose email address:
1. Is **missing** (`NULL` or blank/only spaces), or
2. **Contains a literal space**, or
3. Fails a simple required `name@domain.tld` structure (at least one character before @, at least one after @ before a dot, and at least one after the dot).

Produce exactly these columns in order: `CustomerID`, `FirstName`, `LastName`, `Email` (unchanged), `issue`.

**Issue labels and precedence:** `Missing` for absent or blank addresses; `Contains a space` for nonblank addresses containing a literal space; otherwise `Not in name@domain.tld form` for entries failing the simple shape test. Return invalid records only; sort by `CustomerID` ascending.

This is an **illustrative format check**, not a production-grade email validator. Preserve the source's simple matching contract.

## Sample input — Customers

| CustomerID | FirstName | LastName | Email |
|---:|---|---|---|
| 1 | Asha | Rao | NULL |
| 2 | Ben | Das | `ben das@example.com` |
| 3 | Cia | Sen | `cia.example.com` |
| 4 | Dev | Roy | `dev@example.com` |

## Expected output

| CustomerID | FirstName | LastName | Email | issue |
|---:|---|---|---|---|
| 1 | Asha | Rao | NULL | Missing |
| 2 | Ben | Das | `ben das@example.com` | Contains a space |
| 3 | Cia | Sen | `cia.example.com` | Not in name@domain.tld form |

### Why each row appears (no solution spoilers)

- **Asha (1):** NULL email means absent contact information, hence `Missing`.
- **Ben (2):** His address contains a literal space between `ben` and `das`, hence `Contains a space`.
- **Cia (3):** No @ symbol, so the address fails the required structure, hence `Not in name@domain.tld form`.
- **Dev (4) excluded:** `dev@example.com` satisfies the simplified shape and has no space; therefore no issue needs reporting.

**Expected:** Exactly 3 rows, the 5 specified columns and ascending CustomerID.

## Learner-led practice (pending)

**Step 1 reasoning:** Not submitted.  
**First independently authored SQLite query:** Withheld pending student's attempt.  
**Actual intermediate SQL output:** Not executed yet.  
**Independent revisions:** Not submitted.  
**Assistant SQLite reference:** Withheld until review.  
**Assistant SQL Server/T-SQL reference:** Withheld until review; execution not claimed.  
**Source-labeled official answer:** Available within the original source record, not shown before the student's own attempt.  
**New learning Yes/No:** Pending.  
**Question closing commit:** Pending in both repositories.

## Cross-repository records

- [Journey P004](https://github.com/MulikShrikantDattatray14/data-engineering-journey/blob/main/study-records/2026-11-06/PNP-P004-invalid-customer-emails-reattempt.md)
- [Mastry P004](https://github.com/MulikShrikantDattatray14/Data-Engineering-Mastry/blob/main/study-records/2026-11-06/PNP-P004-invalid-customer-emails-reattempt.md)


## Student first independent SQLite submission and execution

**Learner's submitted SQL (composer HTML spaces normalized, text otherwise preserved):**

```sql
select `CustomerID`, `FirstName`, `LastName`, `Email`, 
( case
when Email is null then 'Missing'
when Email like '% %@%.com' then 'Contains a space'
when Email not like '%@%.com' then 'Not in name@domain.tld form'
end) as 
`issue`
from Customers
where Email is null or Email like '% %@%.com' or Email not like '%@%.com'
order by CustomerID asc
```

**Execution environment:** SQLite 3.46.1; exact 4-row illustrative Customers fixture.

**Actual output (3 rows, 5 columns):**

| CustomerID | FirstName | LastName | Email | issue |
|---:|---|---|---|---|
| 1 | Asha | Rao | NULL | Missing |
| 2 | Ben | Das | `ben das@example.com` | Contains a space |
| 3 | Cia | Sen | `cia.example.com` | Not in name@domain.tld form |

**Comparison:** All 3 expected sample rows, 5 expected output columns, labels and sorting match. The query executes successfully; it is not yet fully correct for the stated general problem because additional requirements fail on edge-case data.

**Actual additional SQLite test (six added records on top of original fixture):**

| ID | Email | Expected interpretation | Student query result |
|---:|---|---|---|
| 5 | empty string | Missing | Not in name@domain.tld form |
| 6 | three spaces | Missing | Not in name@domain.tld form |
| 7 | `a@b.org` | valid simple email | Not in name@domain.tld form (wrong inclusion) |
| 8 | `a@exa mple.com` | Contains a space | omitted (wrong exclusion) |
| 9 | `a@b.` | invalid format | Not in name@domain.tld form |
| 10 | `a@ ex.com` | Contains a space | omitted (wrong exclusion) |

**Diagnosis without solution spoiler:** `'% %@%.com'` recognizes only certain space placements, not every literal space. `'%@%.com'` hardcodes `.com`, incorrectly rejecting valid other-domain suffixes. The Missing branch tests NULL but not blank/whitespace-only values. Label precedence and basic CASE/WHERE design are promising. **Status:** Correct for the four-row example, but independent correction required for the broader stated task; do not credit a verified P004 reattempt or reveal a full reference solution yet.


## Latest combined query attempt — syntax review

The student submitted a combined CASE query with corrected Missing (`IS NULL OR LENGTH(TRIM(Email)) = 0`) and literal-space (`LIKE '% %'`) conditions. The pasted SQL became malformed around the third WHEN and CASE END: the `THEN 'Not in name@domain.tld form'` appeared after ORDER BY. Its LIKE pattern also included literal asterisks and backslashes instead of the previously tested pattern. A reconstruction produced SQLite 3.46.1 `OperationalError: near "end": syntax error`. The original paste contains formatting artifacts, so it was not executed byte-for-byte. No output rows, no completion credit, and no solution was supplied. Ask student to resubmit clean final SQL.


## Current full-query submission — malformed paste and incomplete CASE

Learner's new attempt correctly included the Missing condition (`Email IS NULL OR LENGTH(TRIM(Email)) = 0`) and the space condition (`Email LIKE '% %'`) in CASE, with corresponding WHERE checks. The third `WHEN Email NOT LIKE ...` was corrupted by composer formatting, included stray wildcard/escape characters and was missing a `THEN` label before `END`. The pasted text also contained formatting marks around `END` / `FROM`.

**Execution of readable SQL preserving the missing THEN:** Python sqlite3 returned `OperationalError: near "end": syntax error`. No result rows were produced. This is a parsing failure, not a negative sample-result comparison. Prior individual-format tests had succeeded; the full query remains independently unverified. Student needs to resubmit a clean SQLite code block and supply the third CASE branch with a valid THEN label. No reference solution has been revealed or P004 credited.
