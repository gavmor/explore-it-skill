# Explore It! — Exploratory Testing Knowledge Vault & Agent Skills Suite

A persistent, compiled knowledge base and suite of **Agent Skills** codifying the exploratory testing methodologies from Elisabeth Hendrickson's seminal book, *Explore It! Reduce Risk and Increase Confidence with Exploratory Testing*, combined with the agentic workflow architecture pioneered by Addy Osmani.

---

## Author Credits & Acknowledgments

This project is built directly upon the pioneering work of **Elisabeth Hendrickson**:

- **Book**: *Explore It! Reduce Risk and Increase Confidence with Exploratory Testing*  
  Published by The Pragmatic Bookshelf (2013). ISBN-13: 978-1-937785-02-4.  
  Website: [pragprog.com/titles/ehxta/explore-it](https://pragprog.com/titles/ehxta/explore-it/)
- **Core Intellectual Contributions**:
  - The unifying formulation: **$\text{Tested} = \text{Checked} + \text{Explored}$**. Automated checks verify expected behavior; exploratory testing discovers unknown risks.
  - The three-part **Test Charter** template: `Explore [target] with [resources] to discover [information]`.
  - The **Test Heuristics Cheat Sheet** (CRUD, Goldilocks, Zero/One/Many, Beginning/Middle/End, Interrupt, Reverse, Follow the Data, Starve, Violate Data Formats).
  - Techniques for overcoming inattentional blindness through **observability in testing** (making the invisible visible).
  - Systematic **State Modeling** and state tables (*Change the Model*) to isolate transient windows of vulnerability and race conditions.
  - The **Nightmare Headline Game** for reverse-engineering severe failure modes into actionable charters.
  - Continuous exploratory testing in Agile and Extreme Programming (XP) environments.

Special credit also to **Addy Osmani** for the design principles articulated in [*Agent Skills*](https://addyosmani.com/blog/agent-skills/):
- **Process Over Prose**: Converting static testing essays into executable workflows.
- **Anti-Rationalization Tables**: Pre-empting common AI shortcuts with firm rebuttals.
- **Verification as Hard Exit Criteria**: Enforcing evidence (log traces, repro protocols, state matrices) before any task is declared done.

---

## Repository Structure

```
.
├── README.md                          # Project overview & credits
├── index.md                           # Master Obsidian index catalog
├── hot.md                             # Semantic snapshot of recent activity
├── log.md                             # Append-only audit log
├── .manifest.json                     # Ingestion provenance & delta tracking
│
├── concepts/                          # Core testing mental models
│   ├── exploratory-testing.md         # Fundamental theory & checking vs exploring
│   ├── test-charter.md                # 3-part charter mechanics & calibration
│   ├── test-heuristics.md             # Canonical heuristics cheat sheet
│   ├── software-observability-testing.md # Consoles, streaming logs & testability hooks
│   ├── variables-in-testing.md        # Obvious vs subtle variables (Therac-25, Ariane 5)
│   ├── test-oracles.md                # Never/Always invariants & consistency oracles
│   └── exploratory-testing-in-agile.md# TDD, CI, pairing & whole-team quality
│
├── entities/                          # People, tools & historical context
│   └── elisabeth-hendrickson.md       # Biography & contributions
│
├── skills/                            # Knowledge base procedural guides
│   ├── charter-design.md              # Charter drafting & Nightmare Headline Game
│   ├── heuristic-test-execution.md    # Stacking heuristics & steering on anomalies
│   ├── state-model-exploration.md     # Jorgensen's tests, state tables & race windows
│   └── recon-session.md               # 45-min system mapping & touchpoint inventory
│
├── references/                        # Source material deep dives
│   └── explore-it.md                  # Comprehensive book reference
│
└── agent-skills/                      # Actionable Agent Skills (Addy Osmani style)
    ├── README.md                      # Suite installation & harness guide
    ├── evals/                         # Benchmark & eval prompts
    ├── exploratory-testing/           # [Orchestrator] High-level SDLC workflow
    ├── recon-session/                 # [Reconnaissance] Initial territory mapping
    ├── charter-design/                # [Mission Framing] Charter generation & calibration
    ├── heuristic-test-execution/      # [Execution] Tactical heuristic execution
    └── state-model-exploration/       # [Timing] State transition matrices & race attacks
```

---

## Using as an Obsidian Vault

1. Open **Obsidian**.
2. Select **Open folder as vault** and choose this repository directory.
3. Browse interconnected concepts through graph view, [`index.md`](file:///home/user/Documents/explore-it/index.md), and [[wikilinks]].

---

## Using the Agent Skills

The skills located in [`agent-skills/`](file:///home/user/Documents/explore-it/agent-skills) are compatible with Claude Code, Google Antigravity / Gemini CLI, Cursor, and any harness supporting `SKILL.md` workflows.

To install into your global AI environment:
```bash
# Antigravity / Gemini CLI
cp -r agent-skills/* ~/.gemini/config/skills/

# Claude Code
cp -r agent-skills/* ~/.claude/skills/
```

See [`agent-skills/README.md`](file:///home/user/Documents/explore-it/agent-skills/README.md) for full instructions and prompt triggers.

---

## License

The distilled knowledge, notes, and agent skills in this repository are licensed under the [MIT License](LICENSE).  
Original testing methodologies, concepts, and heuristics are copyright © 2013 Elisabeth Hendrickson / The Pragmatic Bookshelf.
