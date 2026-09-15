# AS20

Agent Studio 2.0 functional testing repository.

## Purpose

This repository stores the functional test strategy, requirements and design decisions, role/access definitions, business scenarios, manual and automation test definitions, execution evidence, and reporting assets for Agent Studio 2.0.

## Current Status

- Phase 1 — Strategy & Test Model: In progress
- Functional Test Strategy / Master Test Plan: Draft v0.1
- Role/accessibility matrix: Pending
- Detailed Business Scenario Catalogue: Next

## Repository Structure

- `docs/strategy/` — Functional test strategy and master planning documents
- `docs/requirements/` — Requirements and confirmed business rules
- `docs/role-access/` — Role/accessibility matrices and RBAC decisions
- `docs/test-data/` — Test data definitions
- `docs/decisions/` — Testing/product clarification decisions
- `scenarios/` — Business scenarios grouped by capability
- `test-definitions/manual/` — Manual test definitions
- `test-definitions/automation/` — Automation test definitions/assets
- `executions/` — Test execution records
- `evidence/` — Execution evidence
- `reports/` — Test reports

## Traceability Model

`Capability → Business Scenario → Test Definition → Execution → Evidence / Defect`

Role/access is treated as an execution dimension where practical, with dedicated permission test definitions for access-control behaviour.
