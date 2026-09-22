# ssf-assign-smoke

A scratch repository for the SSF Chrome extension's "Assign agent" smoke test:
an item with no agent to assign one to from the overlay.

## Fixture: an item with an agent

The far side of the same flow: an item an agent is already on, because one was
assigned to it from the overlay.

| Item | State the overlay sees | Overlay must offer |
| --- | --- | --- |
| [#4 Third scratch item, to assign from the overlay](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/4) | agent attached | the attached agent — harness, model, branch — not the **Assign agent** form |

#4 is the item the assign flow was exercised on. Assigned from the overlay at
12:49:12Z; SSF recorded the session it attached at 12:49:35Z:

```ssf
harness: Oh My Pi
model: deepseek/deepseek-flash
effort: high
driver: herdr
branch: bot/issue-4-third-scratch-item-to-assign-from-the-ov
```

What the overlay reads here is *an agent is attached*, not *who is assigned*. The
assignee is mutable — an item can be unassigned again — while the attachment stays
recorded on the item as the `ssf` comment above and on the branch it names, so the
fixture holds whatever the assignee is at any later moment, and whatever the item's
own state is. #4 has already been through the round trip: closed at 12:50:18Z to
free its workspace, reopened at 12:51:09Z to assign from the overlay again. Neither
step touched the attachment, which is the point of keying the fixture on it.
