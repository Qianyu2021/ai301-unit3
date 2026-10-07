I reproduced the stale-state bug again and the fix is targeted at the exact point where the app keeps serving the old value after the update completes.

The root cause is that the view is reading from stale state instead of the post-update source of truth. The reproduction evidence I am relying on is the same Unit 2 repro I posted earlier:

> "Steps to reproduce: open the screen, trigger the update action, and then immediately inspect the list after the action resolves. Expected: the view updates to the new value without a refresh or stale selection. Actual: the list remains on the previous value and the UI continues to show the old item until a manual reload or re-navigation."

I’m keeping this patch narrow: I will fix the update path and the consumer view that reads the stale value, and I will not broaden the change into unrelated refactors or cleanup. After the fix, I will re-run the same reproduction steps and expect the UI to show the new state immediately with no manual refresh.
