---
title: Test Oracles
category: concepts
tags: [testing, test-oracles, quality-criteria, verification]
aliases: ["Oracles", "Never and Always Rules"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/exploratory-testing]]"
    type: uses
  - target: "[[concepts/test-heuristics]]"
    type: related_to
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Principles and heuristics for evaluating software correctness when precise expected outcomes are unscripted or complex, centered on Never/Always invariants.
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

# Test Oracles

A **test oracle** is the principle, mechanism, or standard by which a tester determines whether an observed software behavior is acceptable or defective. In exploratory testing, where tests explore uncharted territory beyond pre-written specifications, solving the **oracle problem** is critical: *How do you know if what you are seeing is right when no one has exercised the software this way before?*

In *[[references/explore-it|Explore It!]]*, [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]] outlines three practical frameworks for evaluating results.

## 1. Never and Always Invariants

Every system is governed by inviolate rules that must never be broken, regardless of configuration, input error, or network chaos. Even when you do not know the exact numerical output, you know what the system must *never* or *always* do:

```
┌────────────────────────────────────────────────────────────┐
│                    NEVER / ALWAYS RULES                    │
├──────────────────────────────┬─────────────────────────────┤
│ ALWAYS                       │ NEVER                       │
├──────────────────────────────┼─────────────────────────────┤
│ Accounts must balance        │ Corrupt or silently lose    │
│ Double-entry journals sum 0  │ persistent user data        │
├──────────────────────────────┼─────────────────────────────┤
│ Always give user feedback    │ Expose private user data    │
│ on the outcome of an action  │ to unauthorized tenants     │
├──────────────────────────────┼─────────────────────────────┤
│ Always recover to a usable   │ Crash server or terminate   │
│ state after malformed input  │ daemon on unhandled payload │
└──────────────────────────────┴─────────────────────────────┘
```

To extract Never and Always rules, interview stakeholders with targeted questions:
- *"What is the elevator pitch for this product—what core capability must function if everything else fails?"*
- *"What is the single most unforgivable error this system could make?"*

## 2. Consistency Oracles (Comparative References)

When specifications are incomplete or ambiguous, evaluate behavior by comparing against trusted external benchmarks:
- **Comparable Products:** How do industry-leading tools solve this workflow? If competitor products handle an edge case cleanly and your system crashes, that signals an unhandled vulnerability.
- **Standards & Specifications:** Compare behavior against public RFCs, W3C standards, accessibility guidelines (WCAG), or regulatory compliance standards (OWASP, HIPAA, Sarbanes-Oxley).
- **Internal Consistency:** Does the API endpoint validate email addresses with the exact same rules as the frontend web form?
- **Historical Consistency:** Does the new version behave compatibly with previous releases unless an explicit breaking change was planned?

## 3. Useful Approximations

When calculating exact outcomes requires complex mathematical models (e.g., pricing algorithms, search ranking, machine learning scoring), use heuristic approximations:
- **Range & Plausibility Checks:** Does the computed value fall within a sensible physical or domain range (e.g., flight transit time between two cities)?
- **Monotonicity & Trends:** If input $A$ increases while holding other factors constant, does output $B$ strictly increase? (e.g., adding items to a cart should never decrease the subtotal).
- **Conservation Laws:** Does total input equal total output plus retained state? (e.g., items entering a queue must match items processed plus items remaining).
- **Inverse Operations:** Does applying an inverse operation return the original state? (e.g., `decrypt(encrypt(m)) == m`, `deserialize(serialize(obj)) == obj`, `undo(do(action)) == original_state`).

## Related Concepts

- Used to evaluate experiments in [[concepts/exploratory-testing|exploratory testing]]
- Anchored by the [[concepts/test-heuristics#never-and-always|Never and Always heuristic]]
- Tested against [[concepts/variables-in-testing|subtle variables]]
- Applied during [[skills/recon-session|recon sessions]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 5: Evaluate Results).
