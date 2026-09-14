---
name: exploratory-testing
description: Orchestrates structured exploratory testing sessions using the "Tested = Checked + Explored" paradigm from Elisabeth Hendrickson's Explore It!. Make sure to use this skill whenever the user asks to "test this app", "do exploratory testing", "find bugs in this feature", "QA this system", "hunt for edge cases", "verify system resilience", or assess software quality, even if they don't explicitly mention "exploratory testing".
---

# Exploratory Testing (Orchestrator)

> *"Tested = Checked + Explored. Pre-planned automated checks ensure software behaves as intended under expected conditions; exploratory testing actively discovers unmapped risks, side effects, and emergent failure modes."* — Elisabeth Hendrickson, *Explore It!*

This skill orchestrates end-to-end exploratory testing as a disciplined, evidence-driven engineering workflow. It coordinates reconnaissance, chartering, heuristic execution, state exploration, and stakeholder debriefing.

---

## Anti-Rationalization Table

| Common AI Agent Excuse | Senior Engineer Rebuttal |
|---|---|
| *"All unit and integration tests passed, so testing is complete."* | Passing checks verify only what someone already thought to assert. Exploratory testing uncovers the unknown risks lurking in unmapped seams. |
| *"I don't need a charter; I'll just click around and try random inputs."* | Wandering without a charter is aimless meandering. A charter provides explicit mission boundaries while preserving tactical execution freedom. |
| *"There is no GUI or web frontend, so I cannot perform exploratory testing."* | APIs, CLI tools, databases, background daemons, and microservices are first-class targets for headless exploratory testing. |
| *"The task didn't ask for a full test report, so I'll just summarize in text."* | Testing without concrete evidence (log traces, repro steps, state matrices) is speculation. Every session must produce tangible artifacts. |
| *"I saw an unexpected error in the log, but the UI said 'Success', so it's fine."* | The UI is the tip of the iceberg. Background exceptions, silent truncations, and resource leaks are critical defect signals. |

---

## The Exploratory Testing Lifecycle

```
Phase 1: Recon & Scope  ──►  Phase 2: Charter Mission  ──►  Phase 3: Active Exploration  ──►  Phase 4: Debrief & Evidence
(Map ecosystem & state)      (Draft 3-part charter)         (Stack heuristics & oracles)       (Log traces & repro steps)
```

### Phase 1: Recon & Scoping
1. If the target system or codebase is new, legacy, or unfamiliar, execute the `recon-session` skill.
2. Establish observability touchpoints:
   - Identify application log paths (e.g., `tail -f app.log`)
   - Check database or persistence access
   - Verify network inspection mechanisms (browser DevTools, proxies, cURL)

### Phase 2: Charter Definition
1. Execute the `charter-design` skill to establish 1–3 focused charters.
2. Structure each mission using Hendrickson's template:
   `Explore [target] with [resources] to discover [information]`
3. Allocate a strict time-box (typically 45–90 minutes per charter).

### Phase 3: Active Exploration
1. Execute tests using `heuristic-test-execution` (combining data, sequence, and environment heuristics).
2. If the feature involves multi-step workflows, asynchronous jobs, or timeouts, execute `state-model-exploration` to target transient windows of vulnerability.
3. Observe behind the scenes:
   - Check server logs for stack traces or silent warnings
   - Verify that UI updates actually persisted accurately in the database
   - Monitor resource usage (memory growth, dangling open handles)
4. **Dynamic Steering**: When the software flinches (sluggish response, unexpected warning, odd formatting), pause the broad sweep and double down on that specific anomaly.

### Phase 4: Verification & Debrief
1. Document every suspected defect with a deterministic reproduction protocol:
   - Preconditions & starting state
   - Exact input payload or action sequence
   - Expected behavior (citing Never/Always rules or standards)
   - Actual behavior (including console errors or log excerpts)
2. Summarize session findings for stakeholders:
   - Charters explored and time spent
   - Areas characterized as resilient
   - Uncovered vulnerabilities, edge-case risks, and open questions

---

## Non-Negotiable Exit Criteria

A testing mission is **not done** until:
- [ ] At least one concrete charter was documented before test execution began.
- [ ] Runtime observability (logs, network, or data layer) was actively checked during testing.
- [ ] Every reported defect includes exact reproduction steps and captured evidence.
- [ ] A final session debrief artifact is produced.
