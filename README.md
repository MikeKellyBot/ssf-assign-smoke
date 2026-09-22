# ssf-assign-smoke

A scratch repository for the SSF Chrome extension's "Assign agent" smoke test:
an item with no agent to assign one to from the overlay.

## Fixture

| Item | State the overlay sees | Overlay must offer |
| --- | --- | --- |
| [#1 An item with no agent](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/1) | agentless | **Assign agent** form |

The expectation is about the item's *agent*, not its assignee or its open/closed
state. An item is agentless until a session is attached to it, and SSF attaches a
session when the item is assigned — so the agentless state is the unassigned one.

#1 has been through both: assigned to `@MikeKellyBot` at 12:37Z, unassigned again
at 12:48Z. That round trip is the point of using it, and it leaves the item in the
state the form is meant for. Nothing here depends on who is assigned at any given
moment, so re-running the test does not make this fixture stale.
