# Development Process

This document describes how software development is carried out in this project
with a coding agent. It defines the artifacts, the order of work, and the gates
that must be passed before code reaches `main`.

## Process overview

```
dev_requirements.md          dev_plan.md        dev_vplan.md
(what to build)      -->    (iterations)  -->  (how to verify)
                                        |
                                        v
                              [ Approval gate ]
                                        |
                                        v
                    GitHub branch named after iteration / sub-task
                                        |
                                        v
                              Implementation
                                        |
                                        v
                    Verification (tests defined in dev_vplan.md)
                                        |
                                        v
              Pull request  -->  main   +   progress report
                                        |
                                        v
                              Sync & continue
```

## Roles

- **Human** — approves the plan documents, reviews pull requests, merges them,
  and steers priorities.
- **Coding agent** — drafts the plan documents, implements iterations and
  sub-tasks on branches, runs verification, and reports results.

## 1. dev_requirements.md — what to build

The single source of truth for what the software must do.

- One entry per requirement, each with a unique ID (`R1`, `R2`, ...).
- Written from the user's perspective where possible
  ("As a user, I can ... so that ...").
- No priority is needed as all requirements have to be worked through.
- New or changed requirements are added to this file and reviewed before they
  are planned.

## 2. dev_plan.md — how the work is structured

Derived from `dev_requirements.md`. It lists the development iterations.

- Each **iteration** (`I1`, `I2`, ...) represents a milestone or a major
  feature and maps to one or more requirements (e.g. `R1`, `R2`).
- Each iteration can be broken down into **sub-tasks** as needed
  (`I1.1`, `I1.2`, ...). Every requirement is covered by exactly one sub-task
  so nothing is double-assigned or lost.
- Each iteration / sub-task lists: a short description, the requirement(s) it
  satisfies, and its status (see legend below).

Status legend: `proposed` → `approved` → `in progress` → `verified` → `done`.

## 3. dev_vplan.md — how work is verified

Shows how each sub-task and iteration in `dev_plan.md` is going to be verified.

- For every sub-task and iteration: the verification method (unit / integration
  tests, manual checks, lint, type-check, build), the exact command(s) to run,
  and the expected outcome that counts as passing.
- Includes a **definition of done** for the whole iteration (all sub-tasks
  verified, tests green, no regressions).
- Verification steps are written before implementation starts so "done" is
  objective.

## 4. Approval gate

The agent presents `dev_requirements.md`, `dev_plan.md`, and `dev_vplan.md`
for approval.

- No implementation starts before the plan is approved.
- If requirements change mid-flight, the documents are updated first, and the
  affected iterations are re-verified.

## 5. Branching

Once approved, the agent creates a GitHub branch for the work at hand.

- Branch off the latest `main`.
- The branch is named after the iteration or sub-task being implemented,
  e.g. `I2-auth` or `I2.1-login-form`.
- Keep each branch small and focused: one iteration or sub-task per branch.

## 6. Implementation

- The agent implements the sub-task on the branch.
- Prefer test-driven development: write or update the verification (tests)
  from `dev_vplan.md` first, watch it fail, then make it pass.
- Commit in small, descriptive increments.

## 7. Testing

- Run the verification defined in `dev_vplan.md` for the sub-task / iteration.
- Fix failures until the expected outcomes are met.
- Run the full verification suite to confirm no regressions before opening a
  pull request.

## 8. Pull request and progress report

When tested, the agent sends a pull request to merge the branch into `main`.

The pull request must include a **progress report** covering:

- which sub-task and/or iteration was completed (IDs from `dev_plan.md`),
- which requirements it satisfies,
- the changes made,
- the test results (what was run, pass/fail, output summary).

The human reviews the pull request and merges it into `main`.

## 9. After merge

- `main` is synced locally (fast-forward pull).
- The iteration / sub-task status is updated to `done` in `dev_plan.md`
  and `dev_vplan.md`.
- The finished branch may be deleted after the pull request is merged.

## Rules of thumb

- Never commit directly to `main`; all implementation work goes through the
  branch → test → pull request flow above.
- Keep `main` green at all times.
- One pull request = one iteration or sub-task with its verification results.
