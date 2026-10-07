# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives:
- In an eval bundle, the decisive evidence sits in the issue description and the "Repro evidence" block, then in the candidate plan's stated cause or diagnosis.
- In live mode, compare the issue thread and the student's posted repro comment to the draft plan's cause statement.

What good looks like:
- The diagnosis names the underlying condition the reproduction proves, not a separate symptom or a vague guess.
- The cause explains the observed behavior in the issue and matches the reproduction: the plan says why the stale state persists until the view is rebuilt, rather than blaming a general UI issue.

## Scope

Where it lives:
- In the candidate plan, look for the "Change" lines, any "In:" or "Out:" boundaries, and the explicit scope statement.
- In live mode, the issue thread and the repo facts can help confirm whether the plan is a narrow fix or a project-wide rewrite.

What good looks like:
- The plan names the specific file, subsystem, or behavior it will change and clearly excludes adjacent work that is not required to fix the bug.
- A bounded plan says, in effect, "this one fix in this area" rather than "refactor the relevant code path and perhaps also clean related issues."

## Executability

Where it lives:
- In the candidate plan, read the concrete change description, file locations, and the order of operations. If the plan is written as a checklist or mini-approach, those steps are the evidence.
- In live mode, this may also include the issues or code ownership cues in the thread, but the plan itself must still be actionable without follow-up questions.

What good looks like:
- A stranger could start the work using the plan alone: the file, subsystem, and sequence of edits are named, and the change is specific enough to begin.
- The plan does not rely on hidden context or a missing explanation such as "fix the bug in the relevant component" without saying where or how.

## Test plan

Where it lives:
- In the candidate plan's "Test" section, read the named repro steps and expected result.
- Compare those steps to the actual reproduction evidence in the package, especially the observed failure and the expected outcome.

What good looks like:
- The test plan names the observable success condition and ties it directly to the reproduced bug, such as "at step 3 the color must flip without leaving the view."
- The plan uses evidence-based checks, not vague outcomes like "the fix works" or "the UI behaves correctly."

## Honesty

Where it lives:
- In the candidate plan, look for risk notes, unknowns, dependencies, and deviations from the original description.
- In live mode, an honest mid-build change is recorded in the updated plan or comment, not only in the code diff.

What good looks like:
- The plan states what is known, what is uncertain, and what may need follow-up during implementation without pretending certainty.
- If a plan changes as work proceeds, the updated plan records the reason and new scope instead of silently drifting away from the original diagnosis.

## Comms

Where it lives:
- In the candidate plan comment, read it alongside the issue thread highlights and the repo facts block.
- In live mode, the comment should also respect the repo's contribution policy and any maintainer signal about review bandwidth or AI-generated PRs.

What good looks like:
- The plan comment clearly states the reproduction, the minimal change, and the follow-up verification, and it matches the issue's real expectations.
- It is concise, thread-aware, and consistent with the repo facts: it does not sound like boilerplate, and it does not ignore maintainer guidance or the project's contribution norms.
