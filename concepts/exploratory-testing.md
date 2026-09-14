---
title: Exploratory Testing
category: concepts
tags: [testing, exploratory-testing, methodology, quality]
aliases: ["ET", "Exploration in Testing"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/test-charter]]"
    type: uses
  - target: "[[concepts/test-heuristics]]"
    type: uses
  - target: "[[concepts/exploratory-testing-in-agile]]"
    type: related_to
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Simultaneous learning, test design, and test execution aimed at uncovering unknown risks where pre-scripted checks cannot reach.
provenance:
  extracted: 0.94
  inferred: 0.06
  ambiguous: 0.00
base_confidence: 0.57
lifecycle: draft
lifecycle_changed: "2026-09-14"
tier: core
created: "2026-09-14T14:31:00Z"
updated: "2026-09-14T14:31:00Z"
---

# Exploratory Testing

**Exploratory testing (ET)** is an empirical approach to software evaluation characterized by **simultaneous learning, test design, and test execution**. Rather than executing pre-scripted test steps mechanically, an exploratory tester designs tiny experiments in rapid succession, immediately executes them, observes the actual behavior, and uses the feedback from the last experiment to steer the next.

The term was coined in 1988 by Cem Kaner and extensively refined in [[references/explore-it|Explore It!]] by [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]].

## The Two Sides of Testing: Checking vs Exploring

In *Explore It!*, Hendrickson articulates that any testing effort must address two distinct questions:

$$\text{Tested} = \text{Checked} + \text{Explored}$$

| Dimension | Checking | Exploring |
|---|---|---|
| **Core Question** | Does software behave as intended under expected conditions? | Are there any other risks, side effects, or failure modes? |
| **Timing** | Tests are designed in advance. | Tests are designed, executed, and adapted on the fly. |
| **Primary Value** | Repeatability, regression protection, confidence in known baselines. | Discovery of unknown unknowns, edge-case interactions, emergent bugs. |
| **Mechanism** | Tripwire net catching violations of explicit assertions. | Active scouting into unmapped spaces beyond the net. |
| **Execution** | Ideal for machine automation (CI / unit / integration tests). | Requires human judgment, curiosity, and critical analysis. |

Pre-planned tests provide safety and repeatability, but repeatability does not surface new information. Variation is required to discover new risks.

## Essential Elements of Exploratory Testing

Exploratory testing rests on three continuous activities occurring concurrently:

```
          ┌─────────────┐
          │   Charter   │
          └──────┬──────┘
                 │ (guides)
                 ▼
          ┌─────────────┐
   ┌─────►│ Test Design │──────┐
   │      └─────────────┘      │
   │ (steers)           (executes)
   │                           │
┌──┴──────────┐         ┌──────▼──────┐
│  Learning   │◄────────│ Observation │
└─────────────┘(reveals)└─────────────┘
```

1. **Test Design:** Formulating an experiment or hypothesis based on mental models, risk areas, and [[concepts/test-heuristics|test heuristics]].
2. **Execution & Observation:** Interacting with the system and actively looking behind the scenes via [[concepts/software-observability-testing|observability tools]] (consoles, logs, database state).
3. **Learning & Steering:** Evaluating results against [[concepts/test-oracles|test oracles]], recognizing unexpected behavior, and steering the next test toward suspicious anomalies.

## Structure: Session-Based Test Management (SBTM)

Unstructured exploration risks turning into aimless meandering. To maintain rigor and accountability, exploratory testing relies on:
- **[[concepts/test-charter|Test Charters]]:** Clear, bounded mission statements setting scope without prescribing rigid keystrokes.
- **Time-Boxed Sessions:** Focused periods (typically 45–90 minutes) dedicated to a single charter without interruption.
- **Session Notes:** Lightweight records of test ideas, anomalies found, areas investigated, and questions raised.
- **Debriefs:** Structured conversations with stakeholders (developers, product managers) reviewing discoveries and risks.

## Related Concepts

- Guided by a [[concepts/test-charter|test charter]]
- Uses cognitive [[concepts/test-heuristics|test heuristics]]
- Unpacks multi-dimensional [[concepts/variables-in-testing|variables in testing]]
- Integrated into development via [[concepts/exploratory-testing-in-agile|exploratory testing in agile]]
- Bootstrapped on new systems through [[skills/recon-session|recon sessions]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 1: On Testing and Exploration).
- Kaner, Cem. *Testing Computer Software*. Tab Books, 1988.
- Bach, James and Bach, Jon. *Session-Based Test Management*. Satisfice, 2000.
