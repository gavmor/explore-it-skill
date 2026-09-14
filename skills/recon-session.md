---
title: Recon Session
category: skills
tags: [testing, reconnaissance, legacy-systems, exploration]
aliases: ["Reconnaissance Session", "Product Recon"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/exploratory-testing]]"
    type: uses
  - target: "[[concepts/test-charter]]"
    type: implements
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Initial reconnaissance methodology for quickly mapping an unfamiliar or legacy codebase to identify touchpoints, ecosystem boundaries, and high-priority charters.
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.00
base_confidence: 0.57
lifecycle: draft
lifecycle_changed: "2026-09-14"
tier: supporting
created: "2026-09-14T14:31:00Z"
updated: "2026-09-14T14:31:00Z"
---

# Recon Session

A **recon session** (reconnaissance session) is a specialized, time-boxed exploratory session conducted at the outset of investigating a new product, legacy application, or unfamiliar service. Coined by James and Jon Bach and formalized in *[[references/explore-it|Explore It!]]* by [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]], its mission is not to find every bug, but to **map the territory**.

## The Recon Charter

A standard recon charter is structured as:

> **Explore** `[the target application or system]` **with** `[reconnaissance techniques and observability tools]` **to discover** `[the ecosystem, touchpoints for visibility and control, variables, and emerging risks]`.

## Core Reconnaissance Questions

By the conclusion of a recon session (typically 60–90 minutes), the explorer should be able to answer:

1. **Purpose & Capability:** What does the system actually do? What problem does it solve?
2. **Inputs & Outputs:** What interfaces does it accept (GUI, REST, CLI, files)? Where does it output (logs, queues, DB, displays)?
3. **Touchpoints for Visibility & Control:** Where can an explorer inspect internal state? Are there debug headers, admin consoles, or database tables accessible?
4. **Environment & Dependencies:** What databases, third-party APIs, and OS resources does it touch?
5. **Vulnerabilities & Outliers:** What crashes or hangs when given basic malformed inputs?

## The Staples Easy Button Case Study

In *Explore It!*, Hendrickson cites James and Jon Bach's classic video demonstrating a recon session on the Staples "Easy Button"—a physical toy with only a single button. Even on this trivial device, they demonstrated over a dozen distinct recon techniques:
- **Claims Testing:** Comparing device behavior against packaging claims ("Press it and it says 'That was easy'").
- **Product Analysis:** Inspecting materials, battery compartment, and internal circuit speaker mechanics.
- **Stress & Abuse Testing:** James Bach's famous "shoe test"—resting heavy objects on the button or pressing it repeatedly at high frequency.
- **Environmental Variations:** Operating in extreme cold, moisture, or while dropping from heights.

## Deliverables from a Recon Session

A recon session yields four immediate assets that guide all future testing:

```
┌────────────────────────────────────────────────────────┐
│               RECON SESSION DELIVERABLES               │
├──────────────────────────┬─────────────────────────────┤
│ 1. Ecosystem Map         │ Diagram showing databases,  │
│                          │ APIs, queues, and gateways  │
├──────────────────────────┼─────────────────────────────┤
│ 2. Touchpoint Directory  │ Log files, consoles, admin  │
│                          │ endpoints, and DB schemas   │
├──────────────────────────┼─────────────────────────────┤
│ 3. Variable Catalog      │ Obvious inputs and subtle   │
│                          │ timing/configuration flags  │
├──────────────────────────┼─────────────────────────────┤
│ 4. Backlog of Charters   │ Targeted missions for deep- │
│                          │ dive exploration sessions   │
└──────────────────────────┴─────────────────────────────┘
```

## Related Skills & Concepts

- First step in [[concepts/exploratory-testing|exploratory testing]] of legacy or new code
- Generates [[concepts/test-charter|test charters]] using [[skills/charter-design|charter design]]
- Employs [[concepts/software-observability-testing|observability in testing]]
- Identifies [[concepts/variables-in-testing|variables in testing]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 11: Explore an Existing System).
- Bach, James and Bach, Jon. *Easy Button Reconnaissance Session*. Satisfice, 2008.
