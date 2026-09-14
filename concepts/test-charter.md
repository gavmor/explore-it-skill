---
title: Test Charter
category: concepts
tags: [testing, exploratory-testing, charter, planning]
aliases: ["Charters", "Exploration Charter"]
relationships:
  - target: "[[concepts/exploratory-testing]]"
    type: implements
  - target: "[[skills/charter-design]]"
    type: related_to
  - target: "[[references/explore-it]]"
    type: derived_from
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: A concise, mission-focused statement that establishes the scope, resources, and target discoveries of an exploratory testing session without prescribing rigid steps.
provenance:
  extracted: 0.93
  inferred: 0.07
  ambiguous: 0.00
base_confidence: 0.57
lifecycle: draft
lifecycle_changed: "2026-09-14"
tier: core
created: "2026-09-14T14:31:00Z"
updated: "2026-09-14T14:31:00Z"
---

# Test Charter

A **test charter** is a concise statement of purpose that guides an exploratory testing session. It frames what the explorer is setting out to learn, preventing unfocused drifting while leaving the tester complete freedom to design and vary tests dynamically.

In [[references/explore-it|Explore It!]], [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]] models software test charters on historical expedition charters, such as Thomas Jefferson's 1803 instructions to Lewis and Clark (specifying the territory to explore, the resources provided, and the specific intelligence sought).

## The Three-Part Charter Template

A standard charter follows the pattern:

> **Explore** `[target]` **with** `[resources]` **to discover** `[information]`

```
┌──────────────────────────────────────────────────────────┐
│ Explore: [TARGET]                                        │
│          A feature, module, API, workflow, or boundary   │
├──────────────────────────────────────────────────────────┤
│ With:    [RESOURCES]                                     │
│          Tools, heuristics, data sets, personas, configs │
├──────────────────────────────────────────────────────────┤
│ To:      [DISCOVER]                                      │
│          Risks, quality criteria, limits, vulnerabilities│
└──────────────────────────────────────────────────────────┘
```

### Examples of the Template in Practice

1. **Security Focus:**
   > *Explore* the user profile update form *with* inputs containing JavaScript and SQL injection patterns *to discover* vulnerabilities to script execution or unauthorized database mutations.
2. **Integration / Authentication Focus:**
   > *Explore* profile editing *with* third-party authentication mechanisms (OAuth, single sign-on, session timeouts) *to discover* session handling and state synchronization defects.
3. **Boundary / Ecosystem Focus:**
   > *Explore* shopping cart checkout *with* network throttling and server interruption *to discover* how the system preserves transaction integrity and handles idempotency.

## Spectrum: Good Charters vs Over- and Under-Specification

Hendrickson cautions against two common failure modes:

| Degree of Specificity | Example | Analysis |
|---|---|---|
| **Too Specific (Scripted Test Case)** | *"Type `<script>` in the First Name field, click Submit, and check for an alert dialog."* | Not a charter. Over-prescribes mechanical steps; stifles exploration and peripheral observation. |
| **Just Right (Actionable Charter)** | *"Explore user profile inputs with injection attack heuristics to discover vulnerabilities to stored and reflected attacks."* | Provides clear direction and boundaries, but prompts the tester to improvise variations and adapt to findings. |
| **Too Broad (Vague Goal)** | *"Explore the system to find security vulnerabilities."* | Infinite scope. You will never know when the session is complete or if adequate coverage was achieved. |

## Sources of Charters

Charters are generated dynamically from multiple inputs:
- **Requirements & User Stories:** Derived during planning conversations using active reading and "What If?" questions.
- **Risk Analysis:** Brainstormed using exercises like the [[skills/charter-design#the-nightmare-headline-game|Nightmare Headline Game]].
- **Emergent Findings:** Identified during an active exploration session when a side discovery prompts a new charter rather than derailing the current one.
- **Defect Clusters & Support Issues:** In response to recurring customer incidents or legacy code vulnerabilities.

## Related Concepts & Skills

- Core mechanism of [[concepts/exploratory-testing|exploratory testing]]
- Practical creation techniques in [[skills/charter-design|charter design]]
- Paired with [[concepts/test-heuristics|test heuristics]] to seed variations
- Executed during [[skills/recon-session|recon sessions]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 2: Charter Your Explorations).
