# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

### What to read first

1. Read the issue context and repo facts before reading the plan. This tells you what the project expects, what the bug is about, and what the maintainer values in a proposal.
2. Read the reproduction evidence next, and write down the concrete behavior it proves: the steps, expected result, and actual result. The plan must explain or follow that behavior, so the reproduction is the ground truth for every later check.
3. Read the candidate plan after the reproduction. Capture its stated cause, scope boundaries, concrete change, and test plan before grading anything.
4. Read the candidate plan comment last, and compare it to the issue thread and repo facts. This is the communication layer, not the source of truth for the fix itself.
5. Keep a running note of the exact evidence source for each claim while reading: issue, repo facts, reproduction block, plan, or plan comment. This prevents a grader from inventing evidence later.

## Evidence gathering

### How to gather the evidence

1. For each rubric check, locate the exact evidence family it asks for: diagnosis, scope, executability, test plan, honesty, or comms. Do not grade a check from the overall impression of the plan.
2. Pull the fact from the source the rubric names. In an eval package, that means the issue text, repo facts block, repro-evidence block, candidate plan sections, and/or plan comment. In live mode, use the corresponding issue thread, repo docs, repro comment, draft plan, and draft comment.
3. Record the exact fact or quote that supports or contradicts the check. Write down the section name and the specific sentence or step that matters, so the evidence is easy to quote in the grade.
4. If a required fact is absent, mark it as genuinely missing rather than merely unsearched. A check can be graded `unclear` only when the evidence the rubric requires is not present in the package.
5. Do not gather extra evidence beyond the rubric's named sources unless a check explicitly requires cross-checking the issue against the plan. The goal is targeted proof, not a full reread for every decision.

## Check execution

### How to grade each check

1. Execute the checks in a fixed order, starting with diagnosis and grounding, then scope, executability, test plan, honesty, and comms. This order matches the way a maintainer would read a plan: first whether it explains the bug, then whether it is bounded and buildable, then whether it can be verified and communicated.
2. For each check, compare the plan's claim to the evidence you gathered. A check passes only if the plan's actual wording meets the rubric's pass condition and the evidence supports it.
3. If the plan contradicts the issue or reproduction, grade it `fail` with the contradictory fact as evidence. If the plan is silent where the rubric requires proof, grade `unclear` only when the missing proof is genuinely absent.
4. Grade the plan itself, not its tone or formatting. A short but precise plan can pass; a long, confident plan can fail if it hides the real cause, scope, or test conditions.
5. Record one short evidence line for each grade. That line should name the relevant fact or quote, not a summary such as "looks good" or "seems reasonable."
6. After a check is graded, do not reread the entire package unless a later check specifically depends on a different section. Reuse the evidence already captured for that check to keep grading consistent.

## Verdict assembly

### How to reach the verdict

1. Apply the rubric's verdict rule to the per-check grades exactly as written. Required checks gate the result; preferred checks do not change the verdict by themselves.
2. Treat `unclear` according to the rule. If the rule does not say otherwise, treat it as a fail because a plan that cannot be verified is not ready to build from.
3. Build the final verdict from the decisive required checks, not from the overall impression of the package. A single required failure or unresolved evidence gap is enough to reject the plan when the rubric says it is required.
4. Quote the deciding evidence in the output: the fact or sentence from the plan and supporting issue/repro evidence that decided the verdict. The output should state the final verdict as `accept` or `reject` only.
5. If the plan comment or comms checks fail, include that in the verdict only if the rubric marks those checks as required. Do not let a communication issue override a structurally sound plan unless the rule says it does.

---

The procedure is complete when another grader can read the issue, the repro evidence, the plan, and the comment in order and grade the same package the same way without inventing their own rules.
