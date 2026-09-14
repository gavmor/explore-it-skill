---
title: State Model Exploration
category: skills
tags: [testing, state-machines, race-conditions, timing]
aliases: ["State Modeling", "State Tables", "Windows of Vulnerability"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/exploratory-testing]]"
    type: implements
  - target: "[[concepts/test-heuristics]]"
    type: uses
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Method for discovering behavioral states, diagramming transitions, and using state tables to exploit timing race conditions and windows of vulnerability.
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

# State Model Exploration

Intermittent and seemingly unreproducible defects frequently occur within brief **windows of vulnerability**—fleeting periods where a state transition is underway and internal safeguards are momentarily uncoordinated. In *[[references/explore-it|Explore It!]]*, [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]] provides a systematic approach for mapping behavioral states and provoking state-related failures.

## Detecting States

States are distinct behavioral modes of a system. Hendrickson outlines two reliable detection heuristics:

### 1. Alan Jorgensen's Three State Questions
Ask at any point in an interaction:
1. *Are there things I can do now that I could not do before?*
2. *Are there things I cannot do now that I could do before?*
3. *Do my actions produce different results now than before?*
If the answer to any question is yes, the system has entered a new state.

### 2. The "While" Linguistic Test
Listen to the language used to describe the software. Whenever you can naturally frame an explanation starting with *"While..."*, you have isolated a state:
- *"While the file is uploading..."*
- *"While the payment is authenticating..."*
- *"While the account is suspended..."*

## Events That Drive Transitions

States transition only when stimulated by events. Exploratory testers probe beyond obvious user keystrokes to identify all four classes of events:
- **User Actions:** Form submits, button clicks, API calls.
- **Externally Generated Events:** Hardware disconnection, incoming webhooks, external database lock, file system modification.
- **System-Generated Events:** Background queue consumer finishing a job, automated memory compaction, garbage collection pass.
- **Time-Related Events:** Session expiration, heartbeat timeouts, scheduled cron executions.

## Modeling: Diagrams vs State Tables

A powerful heuristic in state exploration is **Change the Model**—converting a visual state graph into a matrix:

### State Diagram (Flow)
Visualizes the happy path and primary error loops:
```
[Logged Out] ──(Enter Credentials)──► [Authenticating] ──(Success)──► [Logged In]
     ▲                                      │
     └────────────────(Failure)─────────────┘
```

### State Table (Completeness Matrix)
Place current states as columns and events as rows. Every cell must define the resulting state:

| Event \ State | Logged Out | Authenticating | Logged In |
|---|---|---|---|
| **Enter Credentials** | Transition → Authenticating | Ignore / Error? | Re-authenticate? |
| **Network Loss** | No change | Hang or Retry? | Disconnect / Reconnect? |
| **Cancel Click** | N/A | Abort & Reset? | N/A |
| **Session Timeout** | No change | Transition → Logged Out? | Transition → Logged Out |

> [!TIP] The Bug-Finding Power of State Tables
> In a state diagram, developers draw only the transitions they thought about. In a state table, **every empty or undefined cell represents a potential crash or unhandled state vulnerability.**

## Attack Vectors on State Models

1. **Provoke Illegal Transitions:** Trigger events in states where they make no sense (e.g., submit order while payment is already authenticating).
2. **Interrupt Transitional States:** Apply the [[concepts/test-heuristics#interrupt|Interrupt]] heuristic right during a "While..." phase (e.g., kill browser tab or sever Wi-Fi while a 50MB PDF upload is at 90%).
3. **Double-Event Race Conditions:** Fire two conflicting events concurrently (e.g., simultaneously click "Approve" and "Cancel" in two browser windows).

## Related Skills & Concepts

- Directly employs [[concepts/test-heuristics|test heuristics]] (Interrupt, Change the Model)
- Uncovers [[concepts/variables-in-testing|subtle timing variables]]
- Applied in [[concepts/exploratory-testing|exploratory testing]] sessions

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 8: Discover States and Transitions).
