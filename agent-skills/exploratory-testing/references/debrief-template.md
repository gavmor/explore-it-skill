# Stakeholder Debrief Template

A concise, narrative structure for debriefing engineering and product stakeholders after an exploratory testing session.

---

## 1. Mission Metadata
- **Charters Explored:** [List charters]
- **Session Duration:** [e.g., 60 minutes]
- **Target Component / Version:** [Commit / release tag]
- **Testers:** [Names / Pair partners]

## 2. Executive Narrative
*A 3–5 sentence summary telling the story of the exploration. Focus on what was learned about the software's capabilities, resilience, and limitations.*

## 3. Discovered Defects (Evidence-Backed)
| ID | Title | Severity / Invariant Violated | Repro Summary | Log / Evidence Link |
|---|---|---|---|---|
| BUG-01 | Silent truncation on 1MB text input | High (Data Loss) | Paste 1MB payload in bio | `app.log:412` |
| BUG-02 | Race condition on double-submit | Critical (Idempotency) | Double-click checkout | Duplicate txn ID |

## 4. Areas of High Confidence & Resilience
- [Features or flows that resisted stress and handled heuristics smoothly]

## 5. Emerging Risks & Recommended Follow-Up Charters
1. *Explore [area] with [resources] to discover [question]*
