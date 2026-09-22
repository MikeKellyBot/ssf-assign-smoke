# ssf-assign-smoke

A scratch repository for the SSF Chrome extension's "Assign agent" smoke test:
an item with no agent to assign one to from the overlay.

## Fixture

| Item | Opened by | Assigned | Overlay must offer |
| --- | --- | --- | --- |
| [#1 An item with no agent](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/1) | `@MikeKellyBot` | `@MikeKellyBot` | **Assign agent** form |

The expectation is about the item's *agent*, not its assignee: #1 is assigned so a
session can work it, and stays un-agented until someone submits the form.
