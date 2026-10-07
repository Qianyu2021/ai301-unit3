# Draft plan

## Diagnosis

The reproduced bug is a stale-state/render mismatch: the app keeps the old state after the user triggers the action that should update it. The evidence from the Unit 2 repro comment is the deciding fact for the fix:

> "Steps to reproduce: open the screen, trigger the update action, and then immediately inspect the list after the action resolves. Expected: the view updates to the new value without a refresh or stale selection. Actual: the list remains on the previous value and the UI continues to show the old item until a manual reload or re-navigation."

This points to the underlying condition that the UI is reading stale state from an earlier render or a cached value instead of the post-update state. The fix must target that stale data path, not the broader app behavior around unrelated rendering.

## Scope

### In scope

- Trace the state transition that runs when the action completes.
- Fix the stale value so the view reads the new state immediately after the update succeeds.
- Keep the patch limited to the reducer/store update path and the component or selector that consumes that state.
- Re-run the original reproduction steps and verify the expected after-state is visible.

### Out of scope

- No unrelated refactor of the broader application shell.
- No rewrite of the data model or migration of neighboring features.
- No cleanup of adjacent UI code that is not required to eliminate the stale-state bug.
- No speculative improvements to performance or styling that do not directly address the reproduced failure.

## Files to touch

The fix is likely limited to the state update and the consumer view, with one or two targeted files rather than a broad sweep:

- The reducer/store logic that writes the updated value after the action completes.
- The component or selector that renders the affected list/view and reads from the stale state.
- Any small helper used to derive the view state from the latest record, if the stale value is coming from memoized or cached selection.

The scope is intentionally narrow: one root cause, one failing behavior, one clear check.

## Approach

1. Re-check the original repro path and confirm which source of truth is stale after the action resolves.
2. Trace the update flow from the triggering action to the reducer/store write and then to the consumer view.
3. Patch the code so the post-update value is written to the canonical state immediately and the selector/view reads the new state instead of an older cached snapshot.
4. Ensure the update does not regress the pre-existing happy path by preserving the same data flow for non-error cases.
5. Keep the change minimal: no large refactor, no unrelated cleanup, and no additional features.

## Test plan

I will re-run the original Unit 2 reproduction steps and confirm the app reaches the expected post-fix behavior:

1. Start from the screen or entry flow that reproduces the stale-state issue.
2. Trigger the update action that was previously leaving the old value visible.
3. Observe the list or item after the action completes.
4. Expected after the fix: the UI updates immediately to the new state and no manual reload or second interaction is required.
5. Also verify the no-bug path still behaves normally if the user updates a different item or reloads the page after a successful action.

The key observable success condition is that the post-action view reflects the latest state without requiring a manual refresh, exactly matching the reproduced expected behavior.

## Risks and unknowns

- The stale value may be coming from a memoized selector rather than the reducer itself, which would require a narrow fix in the derived-state layer.
- There could be a race between the async update completion and the view re-render, so the patch needs to preserve ordering rather than only swapping data at one layer.
- If the bug is intermittent, verifying it may require a repeated run of the same repro steps to confirm the stale-state path is gone.
- I do not expect a broad refactor to be necessary unless tracing shows the stale value originates in shared state owned by a common helper.

## Deviations

TBD after the build.
