# Exploratory Testing Agent Skills Suite

A production-grade collection of **Agent Skills** codifying the exploratory testing methodologies of Elisabeth Hendrickson (*Explore It!*) and the agentic engineering principles articulated by Addy Osmani (*Agent Skills*).

---

## The Core Philosophy: Tested = Checked + Explored

Automated tests check that software behaves as intended under conditions developers anticipated. Exploratory testing actively discovers what happens when conditions deviate, finding unknown risks, side-effect bugs, and timing vulnerabilities.

### Design Principles (The Addy Osmani Standard)
1. **Process Over Prose:** Concrete workflows with step-by-step actions, not essays.
2. **Anti-Rationalization Tables:** Pre-written rebuttals to common AI agent excuses and shortcuts.
3. **Verification as Hard Exit Criteria:** Every skill terminates in tangible evidence (logs, reproduction protocols, state matrices).
4. **Progressive Disclosure:** Lean `SKILL.md` files backed by on-demand `references/`.
5. **Scope Discipline:** Non-destructive, bounded missions.

---

## Skills in This Suite

| Skill | Directory | Primary Role |
|---|---|---|
| **`exploratory-testing`** | [`exploratory-testing/`](file:///home/user/Documents/explore-it/agent-skills/exploratory-testing/SKILL.md) | High-level orchestrator & router. Coordinates recon, chartering, heuristic execution, and debriefs. |
| **`recon-session`** | [`recon-session/`](file:///home/user/Documents/explore-it/agent-skills/recon-session/SKILL.md) | Rapid reconnaissance for mapping unfamiliar codebases, touchpoints, ecosystem boundaries, and variables. |
| **`charter-design`** | [`charter-design/`](file:///home/user/Documents/explore-it/agent-skills/charter-design/SKILL.md) | Framing, bounding, and calibrating charters via the 3-part template and the Nightmare Headline Game. |
| **`heuristic-test-execution`** | [`heuristic-test-execution/`](file:///home/user/Documents/explore-it/agent-skills/heuristic-test-execution/SKILL.md) | Tactical test execution by stacking cognitive heuristics while monitoring server logs and background observability. |
| **`state-model-exploration`** | [`state-model-exploration/`](file:///home/user/Documents/explore-it/agent-skills/state-model-exploration/SKILL.md) | State modeling, state tables (*Change the Model*), and targeting fleeting race windows during state transitions. |

---

## Installation & Harness Integration

### Claude Code / Antigravity / Gemini CLI
Symlink or copy individual skill folders into your skills path:
```bash
# For user-global skills
cp -r agent-skills/* ~/.gemini/config/skills/
# or in Claude Code
cp -r agent-skills/* ~/.claude/skills/
```

### Cursor / Windsurf / Codex
Add to your project rules or system prompt configuration (e.g., in `.cursor/rules/`).
