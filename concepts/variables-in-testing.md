---
title: Variables in Testing
category: concepts
tags: [testing, variables, edge-cases, system-safety]
aliases: ["Subtle Variables", "Variation in Testing"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/exploratory-testing]]"
    type: uses
  - target: "[[concepts/test-heuristics]]"
    type: related_to
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Exploration of obvious vs subtle variables in software systems, drawing on historical disasters to expose overlooked points of failure.
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

# Variables in Testing

In *[[references/explore-it|Explore It!]]*, [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]] defines a variable as **anything that can vary or be changed**. Because the combination of variables in modern software is mathematically infinite, exhaustive testing is impossible. Skilled exploration lies in identifying and manipulating the *most interesting* variables, particularly the subtle ones that developers take for granted.

## Obvious vs Subtle Variables

Testers and developers readily identify obvious variables, but catastrophic failures almost always stem from subtle, unmonitored variables:

| Category | Obvious Variables | Subtle Variables |
|---|---|---|
| **Inputs** | Form fields, button clicks, query parameters. | Character encoding (UTF-8, UTF-16), whitespace variants, invisible non-breaking spaces. |
| **Time & Sequencing** | System clock date/time. | Operator typing speed, latency between async API requests, race windows during writes. |
| **State** | Logged-in vs logged-out. | Cold cache vs warm cache, stale local storage, dangling session cookies, background sync state. |
| **Environment** | Operating system, browser family. | Locale settings, currency formats, timezone offsets, available file descriptors, subnet firewalls. |

## Lessons from Historical Disasters

Hendrickson highlights three famous engineering catastrophes caused by overlooked subtle variables:

### 1. Therac-25 Medical Accelerator (Timing & Sequence)
In the 1980s, the Therac-25 radiation therapy machine delivered lethal radiation doses to patients. The software contained a race condition: if an experienced operator rapidly edited treatment settings within eight seconds, the machine software armed the full-power 25-MeV electron beam without positioning the protective tungsten target in place. The subtle variable was **operator typing speed and keystroke sequence**.

### 2. Ariane 5 Flight 501 (Environmental Assumption)
In 1996, the Ariane 5 rocket exploded 37 seconds after launch. The inertial reference software was reused without modification from Ariane 4. However, Ariane 5's higher flight trajectory generated higher horizontal velocity values than Ariane 4. This caused a 64-bit floating point value to overflow a 16-bit signed integer conversion. The subtle variable was **acceleration magnitude in a reused component**.

### 3. Mars Exploration Rover Spirit (Accumulation & File System)
In 2004, the Spirit rover on Mars stopped transmitting and continuously rebooted. The flash memory file system was overwhelmed not by active scientific data, but by an accumulation of thousands of deleted file tracking nodes created during boot sequences on the long journey from Earth. The subtle variable was **cumulative file system directory overhead over time**.

## Techniques for Identifying Subtle Variables

To uncover hidden variables during [[concepts/exploratory-testing|exploratory testing]], Hendrickson recommends:
1. **Analyze Dependencies:** Look at what the system touches—filesystems, external APIs, DNS servers, clocks, caches.
2. **Examine Boundaries:** Apply heuristics like [[concepts/test-heuristics#goldilocks|Goldilocks]] and [[concepts/test-heuristics#zero-one-many|Zero, One, Many]] to data structures and counts.
3. **Vary Sequences:** Invert order of operations using the [[concepts/test-heuristics#reverse|Reverse]] and [[concepts/test-heuristics#interrupt|Interrupt]] heuristics.
4. **Inspect State Models:** Map state transitions using [[skills/state-model-exploration|state modeling]] to expose brief transitional states.

## Related Concepts

- Generates test cases for [[concepts/exploratory-testing|exploratory testing]]
- Stimulated by [[concepts/test-heuristics|test heuristics]]
- Surfaced via [[skills/state-model-exploration|state model exploration]]
- Analyzed in [[references/explore-it|Explore It!]] (Chapter 4)

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 4: Find Interesting Variations).
- Leveson, Nancy. *Safeware: System Safety and Computers*. Addison-Wesley, 1995.
