---
name: state-model-exploration
description: Models behavioral states and state transition matrices to expose brief windows of vulnerability, timing race conditions, and unhandled event transitions, using techniques from Elisabeth Hendrickson's Explore It!. Make sure to use this skill whenever the user asks to "test state transitions", "find race conditions", "test timing bugs", "model states for this workflow", "find intermittent or unreproducible bugs", or test asynchronous multi-step operations.
---

# State Model Exploration

> *"Defects that are hard to reproduce are often triggered during a brief window of vulnerability: a moment when conditions line up just right so something can go very wrong. State modeling gives you a systematic approach to discovering and exploiting these windows of vulnerability."* — Elisabeth Hendrickson, *Explore It!*

This skill models system behavior through states, events, and transitions. By translating visual diagrams into comprehensive state tables (*Change the Model*), it exposes undefined transitions, unhandled events, and concurrency race conditions.

---

## Anti-Rationalization Table

| Common AI Agent Excuse | Senior Engineer Rebuttal |
|---|---|
| *"This bug only happened once in 50 tries, so it is an unreproducible fluke."* | There are no flukes in digital computing. "Intermittent" bugs are deterministic defects triggered during fleeting state transitions. Map the state model to isolate the exact window. |
| *"Drawing a flow diagram is enough; I don't need a full state table."* | Diagrams show only the transitions the author anticipated. State tables force an evaluation of every event against every state, exposing the unhandled cells where bugs thrive. |
| *"The operation takes less than 100ms, so users can't click fast enough to race."* | Automated scripts, double-clicks, network latency spikes, and concurrent browser tabs easily hit 10ms windows. |
| *"State testing only applies to frontend UI forms."* | State machines govern background workers, database transaction isolation, OAuth handshakes, microservice sagas, and connection lifecycles. |

---

## State Detection & Event Classification

### 1. Alan Jorgensen's Three State Questions
At any point during an interaction, ask:
1. *Are there things I can do now that I could not do before?*
2. *Are there things I cannot do now that I could do before?*
3. *Do my actions produce different results now than before?*
If yes, the system has entered a new state.

### 2. The "While" Linguistic Test
Listen for explanations containing the word **"While"**:
- *"While the report is generating..."* → State: `Generating Report`
- *"While the account is suspended..."* → State: `Suspended`
- *"While waiting for payment gateway webhook..."* → State: `Awaiting Webhook`

### 3. The Four Event Classes
Transitions are triggered by:
- **User Actions:** Click, submit, cancel, navigate.
- **Externally Generated Events:** Network disconnect, third-party webhook, file dropped on disk, push notification.
- **System-Generated Events:** Queue task completed, cache invalidation, DB deadlocks.
- **Time-Related Events:** Token expiration, heartbeat timeout, scheduled cron trigger.

---

## The Exploration Workflow

```
1. Detect States & Events  ──►  2. Construct State Table  ──►  3. Attack Undefined Cells  ──►  4. Provoke Race Windows  ──►  5. Deliver Vulnerability Matrix
(Jorgensen test & "While")      (States=Cols, Events=Rows)     (Trigger invalid actions)      (Interrupt & concurrency)        (Markdown state report)
```

### Step 1: Enumerate States and Events
Identify all primary resting states and all transient "while" states. List all possible events across all four event classes.

### Step 2: Build the State Table (Change the Model)
Plot states as columns and events as rows:

| Event \ State | Logged Out | Authenticating (`While...`) | Logged In | Suspended |
|---|---|---|---|---|
| **Submit Login** | → Authenticating | Ignore? Double-auth? | Re-auth? | Error Banner |
| **Network Severed** | Stay Logged Out | Hang or Retry? | Drop session? | Stay Suspended |
| **Timeout (15 min)** | No-op | Abort auth | → Logged Out | Stay Suspended |
| **Cancel Click** | No-op | Abort & Reset? | No-op | No-op |
| **Concurrent Login** | No-op | ? | Invalidate old? | Block |

### Step 3: Attack Undefined & Empty Cells
Examine every cell where behavior is ambiguous, unhandled, or marked with a question mark:
- Fire the event when in that state.
- Does the system throw an unhandled exception?
- Does it leak memory or hold an open transaction lock?

### Step 4: Provoke Race Windows (Timing Attacks)
Target the transitional "While..." states:
- **Mid-Flight Interruption:** Trigger the [[concepts/test-heuristics#interrupt|Interrupt]] heuristic right during an asynchronous transition (e.g., kill process while writing database rows).
- **Double-Action Race:** Issue two conflicting events within milliseconds (e.g., click "Approve" and "Reject" concurrently in two parallel threads).
- **Time-Boundary Collisions:** Trigger an action at the exact millisecond a session token expires.

---

## Deliverable: State Vulnerability Assessment

```markdown
# State Model Exploration: [Workflow/Component Name]

## 1. State Table Matrix
[Complete table mapping all States against all Events, highlighting vulnerabilities in RED/BOLD]

## 2. Identified Windows of Vulnerability
- **Transitional State:** `[e.g., Authenticating / Processing Payment]`
- **Window Duration:** `[e.g., ~400ms network roundtrip]`
- **Exploited Condition:** `[e.g., Concurrent cancel request triggers duplicate credit]`

## 3. Discovered Defects & Unhandled Transitions
- **State:** `[State]`
- **Event:** `[Event]`
- **Actual Behavior:** `[e.g., HTTP 500, Database Deadlock, Silent State Desync]`
- **Remediation Recommendation:** `[e.g., Implement idempotency key, reject cancel event while processing]`
```

## Exit Criteria
- [ ] A complete state table was constructed with both resting and transitional states.
- [ ] Every empty/undefined cell in the table was tested or explicitly characterized.
- [ ] Transient "While..." states were subjected to concurrent or interruption attacks.
