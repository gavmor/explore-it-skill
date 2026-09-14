---
title: Test Heuristics
category: concepts
tags: [testing, heuristics, test-design, cheat-sheet]
aliases: ["Heuristics Cheat Sheet", "Testing Heuristics"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/exploratory-testing]]"
    type: implements
  - target: "[[skills/heuristic-test-execution]]"
    type: related_to
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Cognitive rules of thumb and cheat-sheet patterns for generating high-leverage test variations across data, sequences, states, and ecosystems.
provenance:
  extracted: 0.96
  inferred: 0.04
  ambiguous: 0.00
base_confidence: 0.57
lifecycle: draft
lifecycle_changed: "2026-09-14"
tier: core
created: "2026-09-14T14:31:00Z"
updated: "2026-09-14T14:31:00Z"
---

# Test Heuristics

In software testing, a **heuristic** is a cognitive rule of thumb or mental shortcut that guides problem-solving, test design, and discovery. Rather than guaranteeing a mathematical proof of correctness, heuristics suggest high-probability places where software faults congregate.

In [[references/explore-it|Explore It!]], [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]] cataloged the canonical **Test Heuristics Cheat Sheet** across general software systems and web applications.

---

## General Test Heuristics

### 1. Data & Cardinality Heuristics

- **Zero, One, Many:** Test with zero items (empty set), exactly one item (singular boundary), and many items (collections, pagination, capacity limits).
  - *Bugs caught:* Pluralization errors ("1 items"), divide-by-zero, collection resizing, off-by-one errors.
- **Kaner's Law of Zero:** *"If there is a zero, something will attempt to divide by it."* Software frequently fails when processing empty collections or zero-length payloads.
- **Some, None, All:** For defined finite sets (permissions, checkboxes, roles, tags). Test with none selected, some selected, and all selected.
  - *Bugs caught:* System treating "None" identically to "All" (e.g., granting full admin rights when permissions array is empty).
- **Goldilocks:** Values that are *too small*, *too big*, and *just right*.
  - *Bugs caught:* Silent truncation of strings, buffer overflows, unhandled exception stack traces.
- **Violate Data Format Rules:** Intentionally supply data violating domain constraints (negative prices, malformed IP addresses, dates with 31 days in February, unescaped delimiters).

### 2. Position & Sequence Heuristics

- **Beginning, Middle, End:** Vary the position of elements or actions. Insert, delete, or modify an item at the exact beginning, in the middle, and at the trailing end of a sequence or file.
  - *Bugs caught:* Truncation at boundaries, broken linked lists, string concatenation indexing errors.
- **Reverse:** Execute operations backward. Step through workflows in reverse order, use undo chains extensively, or jump directly to the final state and navigate backward.
- **Interrupt:** Abruptly cancel operations in flight. Terminate processes, pull network cables, force sleep/hibernation, kill browser tabs, or induce session timeouts while transactions are writing.
  - *Bugs caught:* Partial state writes, deadlocks, corrupted files, unreleased locks.

### 3. Structural & Architectural Heuristics

- **CRUD (Create, Read, Update, Delete):** Exercise the full lifecycle of every persistent entity. Combine with other heuristics (e.g., CRUD with *Beginning/Middle/End* or *Zero/One/Many*).
- **Follow the Data:** Trace a single piece of data across its journey through the entire ecosystem—from ingestion/UI entry, through databases and message queues, into batch jobs, search indexes, and export reports.
- **Centralize Everything:** Move all distributed assets into a single location, folder, or owner account.
- **Decentralize Everything:** Scatter centralized data across hundreds of folders, accounts, subnets, or machines.
- **Starve:** Deprive the application of vital resources: saturated CPU, exhausted memory, full disk storage, throttled bandwidth, or missing socket connections.
- **Too Few / Too Many:** Violate concurrency or capacity expectations (too many concurrent sessions, too few records to populate a grid).
- **Abstract & Zoom:**
  - *Abstract:* Strip out implementation details to see high-level conceptual flows.
  - *Zoom:* Expand a seemingly instantaneous event (like clicking "Save") into its internal substates (serialize, validate, send, commit, acknowledge).
- **Change the Model:** Shift representations (e.g., convert a state diagram into a state table to reveal unhandled state-event cells).

---

## Web-Specific Heuristics

- **Back, Forward, History:** Use browser history controls instead of in-app navigation buttons. Look for double-submit warnings on `POST`, duplicated financial transactions, and cache inconsistencies.
- **Bookmark It:** Bookmark intermediate steps in a multi-stage flow (e.g., step 3 of a checkout wizard) and navigate directly to that URL in a fresh browser session.

---

## Heuristic Application Matrix

| Heuristic Target | Primary Heuristics to Apply |
|---|---|
| **Input Fields** | Goldilocks, Violate Data Format Rules, Zero/One/Many |
| **Lists & Grids** | Beginning/Middle/End, Zero/One/Many, Some/None/All |
| **Lifecycle Workflows** | CRUD, Reverse, Interrupt, Follow the Data |
| **System Resiliency** | Starve, Interrupt, Too Many |
| **Web Applications** | Back/Forward/History, Bookmark It |

## Related Concepts & Skills

- Core tool of [[concepts/exploratory-testing|exploratory testing]]
- Applied systematically in [[skills/heuristic-test-execution|heuristic test execution]]
- Helps identify [[concepts/variables-in-testing|variables in testing]]
- Explored in [[references/explore-it|Explore It!]] (Appendix 2)

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Appendix 2: Test Heuristics Cheat Sheet).
