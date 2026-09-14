---
title: Software Observability in Testing
category: concepts
tags: [testing, observability, logs, monitoring, testability]
aliases: ["Observability in Testing", "Making the Invisible Visible"]
relationships:
  - target: "[[references/explore-it]]"
    type: derived_from
  - target: "[[concepts/exploratory-testing]]"
    type: uses
  - target: "[[skills/heuristic-test-execution]]"
    type: related_to
sources: ["/home/user/Downloads/Explore It! _ Reduce Risk and Increase Confidence with -- Hendrickson, Elisabeth.pdf"]
summary: Techniques to overcome inattentional blindness by surfacing hidden system behaviors through logs, consoles, monitors, and testability hooks.
provenance:
  extracted: 0.94
  inferred: 0.06
  ambiguous: 0.00
base_confidence: 0.57
lifecycle: draft
lifecycle_changed: "2026-09-14"
tier: supporting
created: "2026-09-14T14:31:00Z"
updated: "2026-09-14T14:31:00Z"
---

# Software Observability in Testing

In *[[references/explore-it|Explore It!]]*, [[entities/elisabeth-hendrickson|Elisabeth Hendrickson]] emphasizes that software is like an iceberg: the majority of system activity takes place below the waterline. Evaluating a system solely through user-facing graphical screens creates a dangerous illusion of health while critical failures brew behind the scenes.

## The Cognitive Trap: Inattentional Blindness

Hendrickson cites the famous perceptual experiment by Daniel Simons and Christopher Chabris (and the Transport for London "Moonwalking Bear" safety video): when observers are focused intently on counting passes between basketball players, over half fail to notice a person in a gorilla suit walking through the middle of the frame.

In software testing, **inattentional blindness** occurs when a tester focuses exclusively on whether an expected UI element appeared (e.g., "Did the confirmation banner display?"), blinding them to:
- Latency spikes or sluggish responsiveness
- Browser console JavaScript exceptions
- Error logs flooding the background server
- Unintended side-effect mutations in related database tables

## Making the Invisible Visible

To observe what is really happening, exploratory testers build observation loops into their sessions:

```
┌─────────────────────────────────────────────────────────┐
│              User Action / API Invocation               │
└────────────────────────────┬────────────────────────────┘
                             │
       ┌─────────────────────┼─────────────────────┐
       ▼                     ▼                     ▼
┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│ System UI     │     │ Server Logs   │     │ DB & Storage  │
│ (Visible)     │     │ & Consoles    │     │ Mutations     │
└───────────────┘     └───────────────┘     └───────────────┘
```

### 1. Consoles and Streaming Logs
- **Browser Developer Tools:** Watch network payloads, status codes, and the JavaScript console for silent errors and unhandled promise rejections.
- **Server Application Logs:** Stream logs concurrently during exploration using command-line filters:
  ```bash
  tail -f production.log | grep -E 'ERROR|WARN|Exception'
  ```
- *The Paperclip Example:* In *Explore It!*, Hendrickson recalls tailing a Ruby on Rails log during a user search. The search UI functioned perfectly, but the log revealed that the image processing gem (`Paperclip`) was saving user attachments on every search query. The UI gave no indication of a bug, but the log exposed an impending performance catastrophe.

### 2. Process and System Resource Monitors
- Monitor CPU, RAM, open file descriptors, and database connections (e.g., using `htop`, `Activity Monitor`, or `Process Monitor`).
- Look for memory leaks after closing modal dialogs, orphaned worker threads, or temp files left behind after interrupted uploads.

### 3. Testability Hooks
Software is much easier to explore when developers deliberately build in testability hooks:
- Verbose logging modes switchable at runtime
- Hidden diagnostic screens or debug headers
- Private administrative APIs allowing inspectors to query internal state directly
- Configurable clocks / mock time providers to test time-based transitions

## Related Concepts

- Foundation of rigorous [[concepts/exploratory-testing|exploratory testing]]
- Applied during [[skills/heuristic-test-execution|heuristic test execution]]
- Essential for mapping [[skills/recon-session|recon sessions]]

## Sources

- Hendrickson, Elisabeth. *Explore It!*. Pragmatic Bookshelf, 2013 (Chapter 3: Observe the Details).
- Simons, Daniel J., and Chabris, Christopher F. "Gorillas in Our Midst: Sustained Inattentional Blindness for Dynamic Events." *Perception*, 1999.
