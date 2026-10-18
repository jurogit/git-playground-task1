# Changes

## Prediction

I changed the session timeout  and added a countNotes function."

## Current changes

┌┌──────────────────┬────────────────────────────────────────────────────────────────────────┬────────────────┐
│       File       │                                 Change                                 │     Status     │
├──────────────────┼────────────────────────────────────────────────────────────────────────┼────────────────┤
│ lib/config.js    │ SESSION_TIMEOUT_MINUTES 15 → 30                                        │ Fine           │
├──────────────────┼────────────────────────────────────────────────────────────────────────┼────────────────┤
│ lib/store.js     │ before renamed to countBefore (with the return updated), plus a new    │ Needs a fix,   │
│                  │ countNotes() function exported from the module                         │ see below      │
├──────────────────┼────────────────────────────────────────────────────────────────────────┼────────────────┤
│ package.json     │ Version 1.0.0 → 1.1.0                                                  │ Fine           │
├──────────────────┼────────────────────────────────────────────────────────────────────────┼────────────────┤
│ notes.js         │ No longer modified. The earlier countNotes() and count changes are     │ Fine, but see  │
│                  │ gone from this file.                                                   │ point 2        │
├──────────────────┼────────────────────────────────────────────────────────────────────────┼────────────────┤
│ notes.md         │ Still there                                                            │ See point 3    │
│ (untracked)      │                                                                        │                │
└──────────────────┴────────────────────────────────────────────────────────────────────────┴────────────────┘

## Still suspicious

1. lib/store.js: countNotes() will crash. It calls store.all(), but there is no store variable inside store.js. That name only exists in notes.js, where the module is imported. Calling countNotes() throws ReferenceError: store is not defined. Inside this file, use all().length instead.
2. countNotes() is still not reachable from the CLI. notes.js has no count case, so notes count prints the help text. The function is exported but nothing calls it. If you want a count command, it needs a case "count" branch (with a break) and a line in the help text.
3. notes.md is still untracked in the repo root. It's the "Prediction" file, and its text is now out of date: it says you added a countNotes function in a place that no longer matches the diff. Keep it out of the commit unless it's meant to be part of the exercise.
4. The 1.1.0 bump promises a feature users can't reach yet. It's fine if the commit is only about adding the function. Otherwise, bump the version after count is wired up.
