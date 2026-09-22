# ssf-assign-smoke

A scratch repository for the SSF Chrome extension's "Assign agent" smoke test:
an item with no agent to assign one to from the overlay.

## Fixture: the timeout fallback

The third state the overlay has to render, after the form and a refusal: the write
is accepted, but no frame ever shows the item with an agent, so *Assigning…*
cannot end on one and ends on the factory's own returned result, with the
dashboard link beside it.

| Item | State the overlay sees | Overlay must offer |
| --- | --- | --- |
| [#7 Seventh scratch item, for the timeout fallback](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/7) | assigned, no agent, and none on the way while the item is closed | *Assigning…*, then the result the factory returned and the dashboard link |

**Why nothing clears the wait here.** This is the accepted-write counterpart of a
refusal: nothing is refused, the frame simply never arrives. #7 is *closed* when
the assign lands, so the assignment reaches GitHub while no session starts, the
item keeps reading *No agent*, and the form has nothing to end on. The wait is the
fallback [mikekelly/simple-software-factory#421](https://github.com/mikekelly/simple-software-factory/issues/421)
gives 30 s before it shows the server's own result and a link to the dashboard.

#7's record, from its GitHub events and the factory's own launch time:

| Time (UTC) | What | Record |
| --- | --- | --- |
| 13:28:53 | #7 opened | `created` |
| 13:28:55 | closed, two seconds later, on purpose | [event](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/7#event-31603007295) |
| 13:29:49 | assigned to `@MikeKellyBot`, while closed | [event](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/7#event-31603072405) |
| 13:30:41 | reopened | [event](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/7#event-31603133526) |
| 13:30:54 | the session starts — 65 s after the write, so only once the item was open | factory `launched_at` |
| 13:30:57 | the session attaches to the item | [comment](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/7#issuecomment-5777441886) |

The fixture is keyed on *the item is closed when the write lands*, not on it
staying closed: the fallback needs no agent on the item for as long as the form
waits, and reopening it afterwards is what gives the session its start.

**To re-run it**: close #7, assign it from the overlay, and watch the wait end on
the factory's returned result and the dashboard link rather than on an agent. It
survives a re-run because the two states are the item's own: closing it retires
the record, and `ssf assign` refuses only an item whose session is still active,
so a closed item is assignable again; and it is the reopen, not the assignment,
that starts the session, since ssf runs nothing on an item that is closed.

[#8](https://github.com/MikeKellyBot/ssf-assign-smoke/issues/8) was opened a second
later for the same fallback's *wording*, and is closed and agentless too: closed
13:30:47Z, assigned 13:32:01Z, both while closed, so no session ever started on
it. It stands as a spare item for the same state; #7 is the one this section pins,
because it records the whole shape, the session that starts on the reopen
included.
