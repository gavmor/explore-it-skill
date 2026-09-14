---
title: Heuristic Test Execution
category: skills
tags: [testing, heuristics, execution, practical-guide]
aliases: ["Executing with Heuristics", "Heuristic Testing"]
relationships:
  - target: "[[concepts/test-heuristics]]"
    type: implements
  - target: "[[concepts/exploratory-testing]]"
    type: uses
  - target: "[[concepts/software-observability-testing]]"
    type: uses
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Practical guide to applying and combining test heuristics during exploratory testing sessions to provoke and isolate defects.
provenance:
  extracted: 0.93
  inferred: 0.07
  ambiguous: 0.00
base_confidence: 0.57
lifecycle: draft
lifecycle_changed: "2026-09-14"
tier: supporting
created: "2026-09-14T14:31:00Z"
updated: "2026-09-14T14:31:00Z"
---

# Heuristic Test Execution

Applying heuristics effectively requires more than mechanically checking items off a list. In exploratory testing, heuristics function as **generative catalysts**—mental prompts that spark new experiments based on the system's immediate responses.

## The Execution Workflow

```
1. Select Target & Goal (from Charter)
   │
2. Choose Primary Heuristic (e.g., CRUD)
   │
3. Layer Secondary Heuristics (e.g., Goldilocks + Interrupt)
   │
4. Execute Experiment & Observe Deep State (Logs, DB, Network)
   │
5. Steer: Did system flinch? Adapt or move to next heuristic
```

## Heuristic Stacking (Combinatorial Power)

Single heuristics find common bugs; **combining heuristics** exposes critical architectural flaws:

1. **CRUD + Beginning/Middle/End:**
   - *Action:* Create a record at the start of a list. Update the record in the middle. Delete the record at the very end.
2. **CRUD + Goldilocks + Interrupt:**
   - *Action:* Initiate an update with a massive payload (oversized image/file), and sever network connectivity at 50% upload. Observe whether database locks are held or disk temp files leak.
3. **Follow the Data + Violate Format Rules:**
   - *Action:* Inject a malformed UTF-8 sequence or SQL payload into an account name field via API, then view it in the administrative report, export to CSV, and import into the analytics pipeline.

## Active Observation During Execution

Never evaluate test results solely through the front-end user interface:
- **Tail server logs in real time:** `tail -f application.log | grep -iE 'error|exception|warn'`
- **Monitor Network Traffic:** Watch for HTTP 500 status codes, slow responses, duplicate network calls on button clicks, or leaked authentication tokens.
- **Inspect Persistence:** Verify that "successful" UI updates actually persisted in the database without field truncation or silent default fallbacks.

## Steering and Diminishing Returns

- If an application handles a heuristic smoothly across 2–3 diverse variations, **shift focus** to another heuristic.
- If the application shows any sign of distress (a sluggish response, an unformatted error banner, or a log warning), **double down**: vary timing, sequence, and payload size around that specific vulnerability.

## Related Skills & Concepts

- Draws from the catalog of [[concepts/test-heuristics|test heuristics]]
- Executed within the framework of [[concepts/exploratory-testing|exploratory testing]]
- Relies on [[concepts/software-observability-testing|observability in testing]]
- Feeds into [[skills/state-model-exploration|state model exploration]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Part II: Adding Dimensions, Chapters 6–9).
