---
name: recon-session
description: Conducts structured reconnaissance sessions to map unfamiliar, legacy, or newly introduced systems, inspired by James/Jon Bach and Elisabeth Hendrickson. Make sure to use this skill whenever the user asks to "recon this system", "explore this new codebase", "map this app", "investigate legacy service", "take a first look at this project", or needs to discover touchpoints, dependencies, and variables before deeper testing.
---

# Recon Session (Reconnaissance)

> *"In exploring an existing system, your goal first and foremost is to find out what it does, what it interfaces with, and how the pieces connect together. A recon session sets the stage for all future missions by mapping the territory."* — Elisabeth Hendrickson, *Explore It!*

A **recon session** is a disciplined, time-boxed scouting mission (typically 45–60 minutes) aimed at rapidly characterizing an unfamiliar software system, service, or codebase.

---

## Anti-Rationalization Table

| Common AI Agent Excuse | Senior Engineer Rebuttal |
|---|---|
| *"I found a bug within two minutes, so I should stop and fix it now."* | Recon is scouting, not repairing. Note the defect, capture the reproduction context, and continue mapping. If you get sucked into fixing, you leave the rest of the territory unmapped. |
| *"There are no docs or README, so I can't understand what it does."* | The code and the running system are the ground truth. Test the executable, inspect interfaces, trace network traffic, and read database schemas. |
| *"This tool only has a few endpoints/flags; a recon session is overkill."* | The Staples Easy Button had only one button, yet revealed over a dozen distinct testing angles (claims, stress, timing, packaging). Simple surfaces conceal subtle dependencies. |
| *"I can just read the source code; I don't need to run it."* | Reading code is static analysis; recon is empirical observation. Runtime behaviors, environment quirks, and latency only reveal themselves when executed. |

---

## The Reconnaissance Workflow

```
1. Frame Recon Charter  ──►  2. Identify Touchpoints  ──►  3. Map Ecosystem  ──►  4. Catalog Variables  ──►  5. Deliver Map & Backlog
(Time-box & boundary)        (CLI, APIs, logs, DB)         (Services & stores)     (Obvious & subtle)          (Markdown artifact)
```

### Step 1: Establish the Recon Charter
Frame a clear charter:
> **Explore** `[target system or module]` **with** `[recon techniques, observability tools, and basic inputs]` **to discover** `[its ecosystem, touchpoints for visibility/control, key variables, and emerging risks]`.

Set a strict time-box (e.g., 45 minutes).

### Step 2: Discover Touchpoints for Visibility and Control
Inspect all mechanisms available to interact with and observe the application:
1. **Public Interfaces:** CLI flags, web forms, REST/GraphQL endpoints, public queue consumers.
2. **Private & Diagnostic Interfaces:** Debug HTTP headers, admin endpoints (`/health`, `/metrics`, `/debug/pprof`), hidden configuration files, private socket paths.
3. **Observation Streams:** Application logs (`tail -f`), system journal (`journalctl`), database tables, browser consoles, network inspection proxies.

### Step 3: Map the Ecosystem and Trust Boundaries
Document what the system touches:
- What datastores does it read/write?
- What third-party external services or APIs does it call?
- Where are the trust boundaries (where unvalidated user input enters the system)?

### Step 4: Catalog Variables
Build an initial table of variables:
- **Obvious Variables:** Supported file types, input fields, URL parameters, configuration options.
- **Subtle Variables:** Locale/character encodings, network latency tolerance, memory constraints, process concurrency, background daemon interactions.

### Step 5: Execute the Baseline Stress Probe
Run a quick, high-impact sanity probe:
- Feed empty payloads (`Zero` heuristic).
- Feed massive inputs (`Goldilocks` heuristic).
- Check how it behaves when a required resource (file, port, database) is missing (`Starve` heuristic).

---

## Required Deliverable: Reconnaissance Summary

At the conclusion of the session, generate a markdown artifact containing:

```markdown
# Reconnaissance Report: [System Name]

## 1. System Overview
- **Core Purpose:** What the software does and why it exists.
- **Primary Interfaces:** CLI, API, GUI, or Daemon.

## 2. Touchpoint Directory
- **Control Points:** How to provoke behavior (e.g., endpoints, commands).
- **Observability Streams:** Log paths, consoles, monitoring metrics.

## 3. Ecosystem & Dependency Map
- Datastores: [e.g., PostgreSQL, Redis]
- External APIs: [e.g., Stripe, SendGrid]
- Trust Boundaries: [Where external data is ingested]

## 4. Key Variables Identified
- Data Variables: [Formats, boundaries]
- Environmental Variables: [OS, network, latency]

## 5. Candidate Charter Backlog
1. Explore [target] with [resources] to discover [risk A]
2. Explore [target] with [resources] to discover [risk B]
```

## Exit Criteria
- [ ] All touchpoints for control and observation are documented.
- [ ] At least one baseline stress probe was executed with runtime log observation.
- [ ] A prioritized backlog of at least 3 deep-dive charters is ready for subsequent testing.
