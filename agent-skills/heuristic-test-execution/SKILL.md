---
name: heuristic-test-execution
description: Executes exploratory test sessions by systematically applying and stacking cognitive heuristics from Elisabeth Hendrickson's Explore It! cheat sheet while monitoring deep system observability. Make sure to use this skill whenever the user asks to "run exploratory tests", "apply test heuristics", "find edge cases in this API or UI", "stress test input data", "provoke bugs with heuristics", or test system resilience.
---

# Heuristic Test Execution

> *"Repeatability will not help you find new surprises—variation will. Heuristics are rules of thumb that suggest high-probability places where software faults congregate."* — Elisabeth Hendrickson, *Explore It!*

This skill drives tactical test execution. It translates exploratory charters into rapid, iterative micro-experiments by stacking heuristics across data, sequence, state, and environmental dimensions while verifying behavior behind the scenes.

---

## Anti-Rationalization Table

| Common AI Agent Excuse | Senior Engineer Rebuttal |
|---|---|
| *"I tested one valid and one invalid input; that's sufficient input testing."* | Two data points do not test boundaries. Apply Goldilocks (too small, too big, just right), Zero/One/Many, and character encoding variations. |
| *"The UI showed a green success toast, so the data was saved correctly."* | Frontends lie or silently truncate. Inspect the database directly or execute a follow-up query to verify exact persistence. |
| *"An unhandled 500 Internal Server Error or crash on garbage input is fine."* | Applications must never crash or spew raw stack traces on bad input. Graceful degradation and user feedback are non-negotiable. |
| *"I don't need to check server logs unless a test fails visibly in the UI."* | Inattentional blindness! Memory leaks, database lock contention, and silent failures appear in server logs long before the UI crashes. |

---

## The Heuristic Cheat Sheet Catalog

### 1. Data & Cardinality
- **Zero, One, Many:** Test with empty sets (`[]`, `""`, `0`), single items, and boundary-pushing quantities (10,000 items, page size overflow).
- **Kaner's Law of Zero:** Where there is a zero, something will divide by it. Test zero balances, zero quantities, zero-byte uploads.
- **Some, None, All:** For multiselects, roles, checkboxes, tags. Ensure "None" is not treated as "All" (e.g., zero permissions mistakenly granting admin access).
- **Goldilocks:** Values *too small* (underflow, negative numbers), *too big* (max integer, 10MB text fields, 4K resolution images), and *just right*.
- **Violate Data Format Rules:** Provide invalid UTF-8, malformed UUIDs, invalid IP addresses, emojis, SQL/script injection vectors, and broken JSON schemas.

### 2. Sequence & Workflow
- **Beginning, Middle, End:** Insert, modify, or delete elements at index 0, in the middle, and at the final index of a collection or stream.
- **Reverse:** Execute operations backward, step through wizards in reverse, or trigger undo chains repeatedly.
- **Interrupt:** Abruptly terminate operations in flight: disconnect Wi-Fi mid-upload, kill worker processes, close browser tabs during checkout, induce session timeout.

### 3. Architecture & Environment
- **CRUD (Create, Read, Update, Delete):** Exercise all four operations across the entity lifecycle.
- **Follow the Data:** Trace a data entity from input entry through background jobs, database rows, cache entries, search indexes, and export files.
- **Starve:** Deprive the system of resources (CPU saturation, out-of-disk space, exhausted database connection pools).
- **Web Heuristics:** Navigate using browser `Back`, `Forward`, and `Refresh` buttons; directly bookmark deep intermediate steps in multi-stage workflows.

---

## The Execution Workflow

```
1. Ingest Charter & Baseline State  ──►  2. Open Observability Streams  ──►  3. Stack Heuristics & Execute  ──►  4. Steer on Anomalies  ──►  5. Deliver Test Protocol
(Set scope & target invariants)         (Tail logs, DevTools, DB access)     (Run micro-experiments)             (Double down on flinches)       (Repro steps & evidence)
```

### Step 1: Initialize Observability
Before executing a single test action, open live monitoring streams:
- Stream server logs: `tail -f app.log | grep -iE 'error|warn|exception'`
- Enable browser DevTools (Network tab for status codes; Console for exceptions).
- Prepare a query tool or script to inspect database state directly.

### Step 2: Stack Heuristics
Combine heuristics to test compound dimensions:
- *Example 1:* `CRUD` + `Goldilocks` + `Interrupt` (Create record with huge payload, interrupt transmission at 75%).
- *Example 2:* `Beginning, Middle, End` + `Some, None, All` (Delete permissions from the middle of an existing role).
- *Example 3:* `Follow the Data` + `Violate Format Rules` (Inject emojis and SQL fragments via API, check export reports).

### Step 3: Execute Micro-Experiments & Observe
Run tests iteratively:
1. Fire the test payload.
2. Check the user-facing output.
3. Check background server logs and database storage.
4. Compare against [[concepts/test-oracles|test oracles]] (Never/Always rules).

### Step 4: Steer on Anomalies
If the system flinches—a 2-second lag, a strange warning, an unescaped character, or an unhandled HTTP 500:
- **Do not move on.**
- Narrow the parameters around that specific vulnerability.
- Vary timing, payload size, and concurrency to characterize the boundary of the defect.

---

## Deliverable: Heuristic Execution Protocol & Bug Report

For every discovered issue, format a strict defect report:

```markdown
### Bug Report: [Concise Defect Title]
- **Heuristics Applied:** [e.g., Interrupt + Follow the Data]
- **Severity / Invariant Violated:** [e.g., NEVER: Silent data loss]
- **Environment & Preconditions:** [Starting state, account type]
- **Reproduction Steps:**
  1. Action 1 with exact payload: `...`
  2. Action 2: `...`
- **Expected Behavior:** [What Never/Always rule or standard dictates]
- **Actual Behavior:** [What occurred, including error codes]
- **Evidence:**
  - Log Excerpt:
    ```
    [ERROR] Unhandled NullPointerException at OrderService.java:142
    ```
  - Network Trace: HTTP 500 on POST `/api/v1/orders`
```

## Exit Criteria
- [ ] At least 3 distinct heuristics from the cheat sheet were executed.
- [ ] Observability streams were monitored concurrently with test execution.
- [ ] Any unexpected behavior is accompanied by deterministic reproduction steps and log evidence.
