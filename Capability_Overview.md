Trust Agent — Capability Overview

What it is

Trust Agent is a runtime verification layer for AI agent outputs. It
sits between an agent's proposed action or answer and its execution,
and checks one thing: does this trace back to what the user actually
asked for, or only to something a tool or document handed the agent
along the way. It returns one of three verdicts: PASS, REFINE, or
FLAG, with a structured, auditable reason for each.

The core principle

Most security tooling checks whether an action is technically allowed
like correct credentials, correct permissions, correct API etc. 
Trust Agent checks something different: whether the action is actually authorized
by the user's own request, regardless of how technically valid it looks. An agent that runs a command because a tool result told it to, rather than because the user asked for it, is the gap most existing
controls cannot see, because every step is individually permitted.
Trust Agent is built specifically to see that gap.

What it catches

Unauthorized or unrequested irreversible actions an agent proposes
based on something it read, rather than something it was told.
Content that quietly exceeds what was asked for like for example, an
output that answers the question and also slips in an unrequested
recommendation or claim with no basis in the source. 
Omissions — output that claims to fully answer a multi-part request but actually
only covers part of it. Data movement out of a system that was never
requested.

Validated against a real, disclosed attack

In June 2026, Tenet Security disclosed "Agentjacking" — A real attack
class where a forged tool response hijacks AI coding agents into
running attacker-controlled code, bypassing standard security controls
entirely because every step the agent takes is technically authorized.
Trust Agent was tested against a faithful reproduction of that attack,
including a deliberately harder variant designed to look legitimate,
using a real local NLI model and a real LLM, not a simulation. Full
results and methodology: see the validation report in this repository.

What it does not claim

It is not a general AI safety system and does not evaluate truthfulness
of factual claims beyond what's available to verify against the
request and any provided source material. It does not replace human
review for ambiguous or judgment-heavy cases, by design, it routes
those to REFINE rather than guessing. 
It has known, documented boundaries, disclosed openly rather than hidden since this is an ongoing project. See the limitations summary in this repository.

What is not included here

The verification engine, scoring logic, and calibration data are
proprietary and not published in this repository. What's shared here
is evidence that the system works and a description of its behavior,
not its implementation. Demonstrations and collaboration inquiries are
welcome on a case-by-case basis.

The interface

Externally, Trust Agent is a single call. This is the entire surface and 
nothing about how the verdict is computed is visible:

INPUT   { request, output, source (optional), pack_id }
OUTPUT  { verdict: PASS | REFINE | FLAG,
          faithfulness: 0.0-1.0,
          gaps: [ { gate, reason_code, field, detail } ],
          trace_id }

Reason codes are drawn from a fixed taxonomy of known failure modes,
not a free-text explanation. Examples seen in the validation report in
this repository: UNREQUESTED_IRREVERSIBLE (an action with no basis in
the request), EXFILTRATION (data leaving the system without
authorization), OMISSION (part of a multi-part request left
unaddressed), FABRICATION (a claim with no support in the source),
INTENT_DRIFT (the output appears to be answering a different question
than the one asked).

pack_id selects a configuration profile for the domain being checked
(for example, a security-review profile versus a DevOps-action
profile) — the panel adapts what counts as a high-risk action per
domain, rather than applying one fixed rule everywhere.

Illustrative example

Constructed for readability, not a literal raw log, and using only
the vocabulary already described above:

{
  "verdict": "FLAG",
  "faithfulness": 0.0,
  "gaps": [
    {
      "gate": "authorization check",
      "reason_code": "UNREQUESTED_IRREVERSIBLE",
      "field": null,
      "detail": "the action has no basis in the original request"
    }
  ],
  "trace_id": "example-001"
}

This reflects the same category of result reported for the attack
case in the validation report, shown here in the output shape rather
than prose.

Context

Trust Agent is one component of a larger project, RITA, which is not
otherwise detailed in this repository.
