# The Verdict Layer Manifesto

*The reasoning behind the framework: independent verification over self-report.*

## The shift

Agents can already write code. The field measures whether they can — resolve rate, pass
rate, benchmark scores. That is **capability**, and capability is a property of the *model*.

It is not the question an engineering organization has to answer before a change reaches
`main`. That question is **trust**:

> **Capability asks: can the agent solve the task?**
> **Trust asks: can the organization safely accept the change the agent produced?**

The one principle the rest of this document unfolds from:

> **Trust is a property of the engineering *process*, not of the model.**

Capability lives in the model; trust lives in how a change is admitted. Keeping these
separate is what keeps this work off the model/agent battlefield — where frontier labs and
agent frameworks already compete — and on an axis of its own.

So the word can't quietly drift back into "governance," we pin it to something measurable:

> **Trust = the probability that an automatically admitted AI-generated change actually
> conforms to the stated requirements** — measured as `1 − false-accept rate` on an
> independent oracle.

Every use of "trust" here must reduce to that property. Definition first, then numbers,
then any broader claim — never the reverse.

## Why a self-graded change cannot be trusted

The default loop lets the agent grade its own work: it writes the change *and* the test
that vouches for it. But a test an agent writes for its own change is **self-referential** —
it passes for a correct fix and for a confidently wrong one alike. Adding a second model as
a "reviewer" does not fix this; you have added another self-interested narrator, not an
independent measurement.

"The agent said it works" is not evidence. The verdict has to come from something the agent
never controlled.

## The decision is tri-state, not binary

Optimistic systems answer accept/reject. A trustworthy one needs a third state — an
**answer-or-escalate** system that knows when it does not know:

> **accept · review · reject**

The honest **review** — "this conforms as far as can be independently checked, but the
specification under-determines the rest, so a human should look" — is a feature, not a
weakness. A trustworthy *yes* (low false-accept) is worth the cost of more honest *I can't
vouch for this*.

## Independent, leak-safe verification

The verdict is formed against evidence the agent did not author and cannot influence:

- an **acceptance test written blind to the fix** — from the stated requirement only, not
  from the agent's solution;
- a **regression check** that the change does not break what already worked;
- and that verification **never touches the hidden oracle** it is being measured against —
  it must not be able to "study for the test." That leak-safety is what makes the resulting
  number mean something.

The verdict is **reproducible**: the same evidence yields the same decision, and it comes
with an archivable trace of *why*. A reproducible decision can be audited; a probabilistic
opinion cannot.

## Why this matters now

As development autonomy rises, the number of human checks per change falls — review stops
being a full inspection and becomes a sampling process. So the cost of a single silently
accepted wrong change grows **faster** than the cost of generating the code. The market is
heading toward more AI-written code *and* lower human-control density — exactly the
conditions under which an independent admission decision becomes load-bearing rather than
optional.

## The objections, answered

**"The next model will fix this."** Answered architecturally, not empirically: even if a
future model lowers the absolute error rate, an organization still needs an *independent*
admission decision. Trust in a change cannot be fully delegated to the system that produced
it — that is a structural requirement, not a temporary gap in model quality.

**"This is just CI / a linter / a policy engine."** Those are valuable and not the claim.
The claim is an **independent, leak-safe, calibrated** verification of AI-generated changes
whose verdict is built from evidence the agent never controlled — and which is measured, on
an independent set, by how much it cuts *shipped* false-accepts.

## A trust metric must itself be trustworthy

This is the deepest point. A measuring instrument can lie — if it is mis-calibrated, or if
it leaks the answer, it will report trust that isn't there. So the instrument has to be
verified *before* any number built on it is published: calibration, leak-safety, and a
deliberate hunt for **false-blocks** (cases where the instrument wrongly rejected a correct
change) are part of the proof, not housekeeping. A trust framework that hid its own
measurement errors would have already failed its own thesis.

## Status — honest by construction

This is an active research effort, and the limits come first:

- The headline figure comes from a **frozen, independent held-out evaluation**, completed
  2026-07-05 against a pre-registered scoring contract: **17/50 silently shipped wrong fixes
  ungated vs 0/50 gated** — full results and reproducible artifacts in
  [patchward](https://github.com/kolesnikov-arch/patchward/blob/main/RESULTS.md).
  Development observations remain what they are — not evidence.
- Validated so far against a public software-engineering benchmark oracle, **not** production
  CI.
- See **[Current Scope & Limitations](CURRENT_SCOPE_AND_LIMITATIONS.md)** before drawing any
  conclusion.

## One line

> Agents can already write code. The unsolved problem is **trust in the change**. This
> framework describes an independent, non-gameable layer that measures not "did the agent
> solve it" but "when the agent is confidently wrong, is it caught" — and on an independent,
> pre-registered held-out set, it cut silently shipped wrong fixes from **17/50 to 0/50**,
> with the full cost published alongside
> ([results](https://github.com/kolesnikov-arch/patchward/blob/main/RESULTS.md)).

*(N comes from the held-out evaluation; until it exists, it stays a placeholder.)*

---

*Intelligence is probabilistic. The admission decision must be independent, reproducible,
and honest about what it cannot yet verify.*
