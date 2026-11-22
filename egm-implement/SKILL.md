---
name: egm-implement
description: >-
  Implement an approved EGM design doc (docs/designs/<FEATURE>.md) in a fresh
  session, coordinating subagents per work package, running the Verification
  Plan, and finishing with a zero-context review of the changes against the spec.
argument-hint: "<path to design doc.md>"
disable-model-invocation: true
---

# EGM Implement

Implement the approved design in `$ARGUMENTS`.

If no path was given, list the files in `docs/designs/` and ask which design to
implement. Do not pick one yourself.

That design doc is the **only source of truth**. You have no earlier context
and must not invent requirements.

## 0. Preconditions

- Check that the project is a git repository with the approved design doc
  committed. If it is not, tell me and ask before running `git init` or
  committing anything.
- Note the current commit so you can report and review the full diff at the end.

## 1. Read the spec

Read the whole design doc. Pay particular attention to the
"Detailed Implementation Plan" section, especially:

- **Target Files to Create/Modify**: the only files you may create or change.
- **Verification Plan**: the tests and checks that must pass.

If a step needs a file that is not listed, or the doc is ambiguous or
contradicts the existing code, **stop and ask me**. Do not guess. If the spec is
substantially wrong, say so: the fix belongs in the design doc, back in the
Elephant session.

## 2. Plan the work

Split the target files into work packages:

- Packages that share no files and do not depend on each other may run in
  parallel.
- Dependent packages run in order (for example database/schema → backend →
  frontend → tests).
- Two subagents must never edit the same file.

Show me the plan and wait for my approval before changing any file.

## 3. Delegate

Give each package to its own subagent (general-purpose). Tell each one:

- the absolute path to the design doc and the sections that apply to it
- exactly which files it may change, and which it must not touch
- the tests/checks for its part from the Verification Plan
- to read the design doc itself, not rely on your summary
- to stop and report rather than guess when the spec is unclear

Each subagent reports the files it changed, what it did, and any deviation
from the spec.

## 4. Verify

When all packages are done, run the full Verification Plan yourself and fix any
failures. Report the commands and their results honestly. If something could
not be run, say so.

## 5. Fresh review

Start a fresh reviewer subagent. Give it **only** the design doc path and the
list of changed files (or the diff since the commit noted in step 0), not your
reasoning or the conversation. It checks the code against the spec for:

- items in the implementation plan that are missing or incomplete
- deviations from the spec
- changes to files outside the Target Files list
- obvious bugs

Show me its findings. Fix only obvious bugs without asking. Discuss everything
else with me first.

(Alternative: in a new session, run `/egm:egm-lite` and type `goldfish` to get
EGM's own Goldfish diff review of the uncommitted changes.)

## 6. Summary

Finish with:

- each item from the implementation plan as done or not done
- the Verification Plan results
- any deviations from the spec and why
- anything still open

Do not commit unless I ask.
