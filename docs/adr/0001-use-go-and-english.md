# 1. Use Go for v1.0 and English as the source language of the project

## Status

Accepted (2026-10-09)

## Context

Memento is a personal learning project. It is developed by one person
who has a full-time job, so the available time is 3 to 5 hours per week.
The main goal is to learn how things work internally, not only to ship
a product.

The author already knows Python, JavaScript and some C++. The app will
run as a web service on a free Oracle Cloud server. In v2.0 the core
will be rewritten in Rust/WebAssembly, so the v1.0 design must be easy
to port.

Code and documentation also need a single source language, because
the project will be maintained for a long time across several computers.

## Decision

1. The v1.0 backend will be written in Go.
2. All code, comments, identifiers, commit messages, issues and ADRs
   will be written in English. English is the source language of the
   documentation. Spanish and Italian translations are derived from it
   (see the README convention).

The language of the application interface (i18n) is a separate
decision and will be recorded in its own ADR.

### Alternatives considered

- **Python:** already known, so it teaches less. Dynamic typing hides
  errors that Go catches at compile time, and deployment needs an
  interpreter and dependencies on the server.
- **JavaScript (Node.js):** same dynamic typing issue, and the
  ecosystem pushes towards frameworks, against the goal of building
  things by hand first.
- **Rust from the start:** better fit for the formula engine, but the
  learning curve is too steep for 3 to 5 hours per week.
- **C++:** too much manual complexity for the time available.

## Consequences

### Positive

- A small language with a gentle curve: progress is possible in short
  weekly sessions.
- The standard library covers HTTP, templates, testing and benchmarks,
  so no framework is needed (matches the "build by hand first" goal).
- Static typing and a built-in test tool support the tests-from-day-1
  practice.
- The result compiles to a single binary, which simplifies deployment
  to the Oracle server and cross-compiling for other systems.
- One source language for code removes ambiguity in identifiers and
  history, and English gives access to the widest set of references.

### Negative

- Go has no enums that carry data, so card types and the formula AST
  must be modeled with interfaces. This is less safe than Rust's
  enums and `match`.
- The core will be rewritten in Rust in v2.0, so part of the effort
  in v1.0 will be done twice.
- Every document needs three versions (en, es, it), and translations
  can become outdated. This is mitigated by the version note at the
  top of each translation.
- Writing in English is slower for a non-native speaker.