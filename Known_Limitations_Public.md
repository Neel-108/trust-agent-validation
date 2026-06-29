## Trust Agent — Known Limitations 

Trust Agent has known, tested boundaries, disclosed here rather than
left for someone else to find.

There are categories of phrasing and claim structure where the system
cannot yet confirm a match with full confidence, even when a human
reviewer would consider the case clearly fine. These are specific,
named, and tracked internally, not described in detail here.

In each of these cases, the system's default behavior is to decline
to auto-confirm rather than to wrongly approve or wrongly block. It
routes the uncertain case to human review (a REFINE verdict) instead
of guessing. 

This is a deliberate design choice: a verification layer
that fails by asking for a human look, rather than by silently passing
or wrongly flagging, is the safer failure mode.

These are active, tracked engineering items, not unknowns. A fuller
technical account exists internally and is available on request for
serious collaboration or evaluation discussions.
