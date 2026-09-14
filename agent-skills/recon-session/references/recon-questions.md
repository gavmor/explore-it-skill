# Reconnaissance Question Checklist

Comprehensive checklist for executing a 45–60 minute reconnaissance session on an unfamiliar codebase or system.

## 1. Primary Inputs & Outputs
- What is the most basic, happy-path input the system accepts?
- What is the exact corresponding output, and where does it appear?
- Does the system produce silent side effects (e.g., writes to temp files, queue messages, audit logs)?

## 2. Touchpoint Directory Checklist
- [ ] Command line interfaces (flags, help outputs, environment variable overrides)
- [ ] Configuration files (JSON, YAML, .env, defaults)
- [ ] Network endpoints (REST, gRPC, WebSocket, GraphQL)
- [ ] Datastore access (SQL tables, Redis keys, document collections)
- [ ] Log outputs (log file paths, log levels, formatting)
- [ ] Metrics & health endpoints (`/health`, `/metrics`, `/info`)

## 3. Dependency & Ecosystem Audit
- What external network services does the system call?
- How does the system behave if an external dependency is unreachable?
- Does it retry indefinitely, crash immediately, or degrade gracefully?

## 4. Subtle Variable Audit
- What character encodings are assumed?
- How does the software handle timezone shifts or UTC vs local time?
- Are there background cron jobs or cleanup daemons that run periodically?
