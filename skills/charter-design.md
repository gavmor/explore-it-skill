---
title: Charter Design
category: skills
tags: [testing, charter, practical-guide, risk-analysis]
aliases: ["Drafting Charters", "Nightmare Headline Game"]
relationships:
  - target: "[[concepts/test-charter]]"
    type: implements
  - target: "[[concepts/exploratory-testing]]"
    type: uses
  - target: "[[references/explore-it]]"
    type: derived_from
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Step-by-step methodology for crafting, calibrating, and generating focused exploratory test charters, including the Nightmare Headline Game.
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

# Charter Design

**Charter design** is the discipline of framing effective exploratory testing missions. A well-designed charter provides clear direction and focus while leaving the explorer free to adapt and improvise test execution.

## The Design Workflow

```
1. Identify Target & Stakeholder Risk
   │
2. Apply Template: Explore [Target] With [Resources] To Discover [Info]
   │
3. Calibrate Specificity (Avoid Scripted Tests & Vague Goals)
   │
4. Review & Validate with Stakeholders
```

### Step 1: Draft with the Three-Part Template

Fill in the core prompt:
- **Target:** A specific feature, workflow, API endpoint, or data store.
- **Resources:** Tools (e.g., Charles Proxy, cURL), heuristics (e.g., [[concepts/test-heuristics#crud|CRUD]], [[concepts/test-heuristics#goldilocks|Goldilocks]]), data sets, or personas.
- **Information:** Quality criteria, vulnerabilities, compliance risks, or resource limits.

### Step 2: Calibrate Scope

Test the draft against two boundary tests:
- *Can this be completed in a single test script?* If yes, the charter is **too specific**—broaden it to cover variations.
- *Could this take weeks with no clear finish line?* If yes, the charter is **too broad**—split it into distinct architectural sub-areas or specific risk categories.

## The Nightmare Headline Game

When a team needs to discover the most urgent risks to explore, Hendrickson recommends the **Nightmare Headline Game**:

1. **Step 1: Imagine the Catastrophe**
   Ask developers, testers, and business stakeholders: *"What is the worst headline our company could see on Hacker News or the front page of the news tomorrow because of this release?"*
   - *Example:* "E-Commerce Giant Charges 50,000 Customers Three Times on Black Friday."
2. **Step 2: Prioritize via Multivoting**
   List all generated headlines on a shared board. Give every participant 3 votes (dots/marks) to distribute across the risks they believe are most catastrophic or plausible.
3. **Step 3: Reverse-Engineer Contributing Factors**
   Take the top-voted headlines and brainstorm potential root causes:
   - Double-clicking the "Place Order" button
   - Network timeouts between the checkout service and the payment gateway
   - Browser back button during processing
   - Concurrency race conditions in message queues
4. **Step 4: Refine into Actionable Charters**
   Transform each contributing factor into a charter:
   > *"Explore payment processing with rapid duplicate clicks and browser navigation actions to discover transaction idempotency failures."*

## Calibrating Charters with Stakeholders

To ensure testing effort matches business value, calibrate charters directly with product owners and engineers using direct risk validation:
- *"I've captured this concern as a charter: `[Charter]`. Is this something we should invest a 60-minute session exploring before release?"*
- *"If this feature failed when interacting with background data synchronization, would you want to know before launch?"*

## Handling Tangents During Sessions

A common challenge in exploratory testing is getting distracted by incidental discoveries.
- **The Rule:** If an unexpected bug or fascinating rabbit hole appears during a session that does *not* directly serve the active charter, log a brief note, create a **new candidate charter** on the backlog, and return immediately to the original mission.

## Related Skills & Concepts

- Guided by the [[concepts/test-charter|test charter]] concept
- Drives [[concepts/exploratory-testing|exploratory testing]] execution
- Leveraged during [[skills/recon-session|recon sessions]]
- Enriched by [[concepts/test-heuristics|test heuristics]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 2: Charter Your Explorations).
