# State Table Architectural Patterns

Standard state table templates for common software workflows, designed to expose unhandled events and race condition windows.

---

## 1. Asynchronous Job Lifecycle

| Event \ State | Idle / Queued | Running (`While...`) | Succeeded | Failed | Retrying |
|---|---|---|---|---|---|
| **Cancel Job** | Drop from queue | Send SIGTERM / cleanup? | Ignore | Ignore | Cancel retry |
| **Worker Crash** | Re-queue | Orphaned? Detection timeout? | N/A | Log error | Backoff |
| **Duplicate Trigger** | Idempotency deduplication | Ignore / Parallel execution? | Re-run? | Re-run? | Ignore |
| **Timeout (Max Wall Clock)** | Purge | Kill & Mark Failed | N/A | N/A | Max retry exceeded |

---

## 2. E-Commerce Checkout Flow

| Event \ State | Cart (Editing) | Awaiting Payment (`While...`) | Authorized | Capture Pending | Completed |
|---|---|---|---|---|---|
| **User Back Button** | No-op | Abort or Double-Auth? | Refund? | Lock screen | Redirect to receipt |
| **Item Out of Stock** | Remove item & warn | Fail transaction cleanly | Void authorization | Critical exception! | N/A |
| **Double-Click "Pay"** | Transition | Ignore duplicate POST | Ignore | Ignore | Ignore |
| **Gateway Timeout (30s)** | No-op | Poll status / Mark Pending | Retry capture? | Alert ops | N/A |
