---
name: charter-design
description: Designs, bounds, and calibrates exploratory test charters using the methodology from Elisabeth Hendrickson's Explore It!, including facilitating the Nightmare Headline Game. Make sure to use this skill whenever the user asks to "write a test charter", "plan exploratory tests", "what should we explore", "run the nightmare headline game", "scope testing for this feature", or needs to define focused testing missions.
---

# Charter Design

> *"A good charter offers direction without overspecifying test actions. It is a prompt: it suggests sources of inspiration without dictating precise actions or outcomes."* — Elisabeth Hendrickson, *Explore It!*

This skill structures the creation, calibration, and prioritization of exploratory testing charters. It transforms vague quality concerns or sprawling feature specifications into crisp, actionable testing missions.

---

## Anti-Rationalization Table

| Common AI Agent Excuse | Senior Engineer Rebuttal |
|---|---|
| *"Writing charters is unnecessary overhead; I can just start testing."* | Unchartered exploration drifts into familiar happy paths. A charter establishes accountability, keeps the session focused, and bounds the scope. |
| *"My charter is 'Explore the entire application to find all bugs.'"* | Vague, infinite charters are useless. You will never know when the mission is accomplished or what risks were actually investigated. |
| *"I'll make the charter very thorough by listing every click and input step-by-step."* | That is a scripted test case, not a charter. Over-specifying steps blinds the explorer to peripheral clues and destroys adaptive steering. |
| *"The Nightmare Headline Game is too extreme for our internal tool."* | Production disasters (data loss, race condition corruptions, security leaks) happen in internal tools too. Thinking adversarially surfaces unstated assumptions. |

---

## The Charter Design Workflow

```
1. Gather Raw Risks / Requirements  ──►  2. Run Nightmare Headline Game  ──►  3. Apply 3-Part Template  ──►  4. Calibrate Specificity  ──►  5. Deliver Charter Card
(Specs, user stories, architecture)      (Worst-case disaster modeling)       (Explore / With / To Discover)   (Avoid scripts vs vague goals)    (Markdown artifact)
```

### Step 1: Ingest Context
Review the target feature, pull request, user story, or architecture doc. Identify:
- Core capabilities that *must always function*.
- Integrations with external dependencies or state stores.
- Recent changes, bug histories, or user complaints.

### Step 2: Run the Nightmare Headline Game
When exploring high-stakes systems or ambiguous requirements, brainstorm the worst conceivable production outcome:
1. **The Headline:** What is the most catastrophic headline that could appear on Hacker News or the front page if this feature fails?
   - *Example:* "E-Commerce App Double-Charges 10,000 Customers During Flash Sale."
2. **Contributing Factors:** Reverse-engineer the technical flaws that could cause this:
   - Network timeout during token exchange
   - Rapid double-clicking on submit button
   - Database deadlocks on inventory decrement
   - Browser back button during checkout redirect
3. **Derive Targets:** Each contributing factor becomes a candidate for a dedicated charter.

### Step 3: Apply the Three-Part Template
Every charter must strictly adhere to Hendrickson's formula:

$$\text{\textbf{Explore}}\;[\text{Target}]\;\text{\textbf{with}}\;[\text{Resources}]\;\text{\textbf{to discover}}\;[\text{Information}]$$

- **Target:** A specific feature, API endpoint, workflow, or architectural seam.
- **Resources:** Tools (cURL, DevTools, Charles Proxy), cognitive heuristics (CRUD, Goldilocks, Interrupt), personas, or data sets.
- **Information:** Risks, boundary limits, Never/Always violations, data integrity failures, or recovery behavior.

### Step 4: Calibrate Specificity (The Goldilocks Test)

Assess the drafted charter against the two failure modes:
- **Too Narrow (Test Script):** *"Type `<script>` in the search box, click Search, and verify no alert appears."* → **Broaden** to: *"Explore search input with injection attack heuristics to discover cross-site scripting and query injection vulnerabilities."*
- **Too Broad (Vague Goal):** *"Explore security in the web app."* → **Narrow** to: *"Explore authentication cookie handling with session interruption and concurrent logins to discover session hijacking vulnerabilities."*

---

## Deliverable: Actionable Charter Card

Every charter produced must be formatted as follows:

```markdown
### Charter: [Descriptive Title]
- **Mission:** Explore `[Target]` with `[Resources/Heuristics]` to discover `[Information/Risks]`.
- **Time-Box:** [45 | 60 | 90 minutes]
- **Target Invariants:**
  - ALWAYS: [Inviolate rule, e.g., "Always return transactional receipts"]
  - NEVER: [Inviolate rule, e.g., "Never charge card without persisting order"]
- **Heuristics to Apply:** [e.g., Goldilocks, Interrupt, Reverse, Back/Forward/History]
- **Observability Streams:** [e.g., Application log, Browser console, DB query log]
- **Debrief Questions for Stakeholders:**
  1. [Specific risk question, e.g., "How should the app behave if the payment gateway times out after 15s?"]
```

## Exit Criteria
- [ ] Charter strictly follows the 3-part template.
- [ ] Specificity passes the Goldilocks calibration test.
- [ ] At least 2 Never/Always invariants and relevant heuristics are specified.
