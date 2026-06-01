<!--
Sync Impact Report
- Version change: unversioned template -> 1.0.0
- Modified principles:
	- Principle 1 placeholder -> I. Training-First Boundaries
	- Principle 2 placeholder -> II. Offline-First Architecture
	- Principle 3 placeholder -> III. Defense in Depth for Access Control
	- Principle 4 placeholder -> IV. Slice-Based Validation
	- Principle 5 placeholder -> V. Simplicity with a Cloud Migration Path
- Added sections:
	- Operational Constraints
	- Delivery Workflow
- Removed sections:
	- None
- Templates requiring updates:
	- ✅ .specify/templates/plan-template.md
	- ✅ .specify/templates/spec-template.md
	- ✅ .specify/templates/tasks-template.md
	- ✅ README.md
- Follow-up TODOs:
	- None
-->

# ContosoDashboard Constitution

## Core Principles

### I. Training-First Boundaries
ContosoDashboard MUST remain suitable for local, instructor-led, and self-paced
training. Features MUST prefer clarity over production completeness, MUST avoid
external service dependencies by default, and MUST document any deliberate
training simplifications or known limitations. Production-only hardening may be
described, but it MUST NOT be presented as already implemented.

Rationale: the repository exists to teach spec-driven delivery and secure design
patterns without requiring cloud access, paid services, or hidden infrastructure.

### II. Offline-First Architecture
New capabilities MUST work in a local development environment with offline-ready
defaults. Persistence, file handling, and authentication integrations MUST use
replaceable abstractions when there is a stated cloud migration path. A feature
may add an abstraction seam before a cloud dependency, but it MUST keep the
default implementation local unless the specification explicitly changes project
scope.

Rationale: the training value depends on reproducible local setup, while the
architecture should still demonstrate how local implementations are swapped for
Azure or equivalent services later.

### III. Defense in Depth for Access Control
Protected behavior MUST enforce authorization at every relevant boundary:
route/page access, service-layer decisions, and data access paths that select or
mutate user-owned records. Features that expose user-specific or privileged data
MUST define actor roles, allowed actions, and anti-IDOR behavior in the spec and
validate those rules during implementation.

Rationale: the repository already teaches claims-based access control and service
authorization; new work must preserve those guarantees rather than relying on UI
visibility alone.

### IV. Slice-Based Validation
Every feature MUST be planned and implemented as an independently demonstrable
user slice. Each slice MUST include the smallest validation needed to falsify its
main risk: automated tests when practical, or explicit manual verification steps
when UI flows or training constraints make automation disproportionate. Security,
authorization, and data-isolation changes MUST include focused validation before
completion.

Rationale: Spec Kit workflows depend on independently testable stories, and the
project needs fast feedback without imposing ceremony where a short manual check
is the right tool.

### V. Simplicity with a Cloud Migration Path
Designs MUST prefer the simplest implementation that satisfies the current
training need. Added layers, patterns, or dependencies require a written reason
in the plan when a direct implementation would otherwise suffice. When a feature
introduces infrastructure concerns, it MUST keep business logic independent from
the concrete provider so the documented cloud migration path remains intact.

Rationale: the project is intentionally small and educational; unnecessary
abstractions obscure the lesson, but hard-coding infrastructure decisions would
block future training scenarios.

## Operational Constraints

- The canonical application stack is ASP.NET Core 8 Blazor Server with Entity
	Framework Core and a local SQL Server-compatible development database.
- Mock authentication remains the default training mechanism until a future
	constitution amendment explicitly adopts a different baseline.
- Features MUST preserve local bootstrap simplicity: a new contributor should be
	able to run the app with standard .NET tooling and repo-local configuration.
- Documentation for new capabilities MUST state whether the behavior is training
	only, production-ready, or intentionally abstracted for later replacement.

## Delivery Workflow

- Specifications MUST describe user stories, offline or infrastructure impacts,
	and access-control implications when the feature touches protected data.
- Implementation plans MUST complete the Constitution Check before research and
	again after design decisions are recorded.
- Task lists MUST keep work grouped by user story and include validation tasks
	for security-sensitive, authorization-sensitive, or data-isolation changes.
- README or feature-specific quickstart guidance MUST be updated when a change
	affects setup, training assumptions, or verification steps.

## Governance

This constitution overrides conflicting local process notes for feature work in
this repository. Amendments require: (1) an explicit summary of the governance
change, (2) updates to dependent Spec Kit templates and affected guidance docs,
and (3) a semantic version decision recorded in the Sync Impact Report.

Versioning policy:

- MAJOR: remove or materially redefine a principle or governance rule.
- MINOR: add a new principle, section, or mandatory delivery requirement.
- PATCH: clarify wording, examples, or non-semantic guidance.

Compliance review expectations:

- Feature plans and reviews MUST confirm training scope, offline viability,
	authorization boundaries, validation coverage, and simplicity justifications.
- Any deliberate constitution violation MUST be documented in the plan's
	complexity tracking table with the rejected simpler alternative.
- Runtime guidance is anchored in README.md and this constitution; both MUST stay
	aligned when repository practices change.

**Version**: 1.0.0 | **Ratified**: 2026-06-01 | **Last Amended**: 2026-06-01
