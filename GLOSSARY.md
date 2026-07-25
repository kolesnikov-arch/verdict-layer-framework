# Glossary

Definitions for the terms used across this framework. These describe **concepts on the
trust axis** — not implementation details. Tool names, stage names, prompts, and internal
logic are deliberately omitted. Where a term has a public-facing wording that differs from
how a practitioner might say it internally, the public wording is given.

---

## The axis

**Capability**
A property of the *model*: can the agent solve the task? Measured by resolve rate / pass
rate (SWE-bench, Terminal-Bench, and similar). Important, well-served by the rest of the
field, and **not** what this framework measures.

**Trust**
A property of the engineering *process*: can the organization safely accept the change the
agent produced? Operationally —

> **Trust = the probability that an automatically admitted AI-generated change actually
> conforms to the stated requirements.**

The measured proxy is `1 − false-accept rate` on an independent oracle. Whenever "trust"
appears, it must reduce to this measurable property; it is never a vibe.

**Trust axis vs capability axis**
The two are orthogonal enough to be distinct questions. A more capable model can still
produce a change an organization should not blindly admit; admitting it safely is a process
problem, not a model problem.

---

## How trust is measured

**False-accept**
A change the layer **admitted** (verdict: accept) that does **not** actually conform — it
fails the independent oracle (does not resolve the issue, or regresses existing behavior). A
shipped false-accept is the costly event the whole framework exists to reduce.

**False-accept rate**
The share of admitted changes that are false-accepts. The core trust signal; `1 − this` is
the operational proxy for trust. The headline claim is always **false-accept ↓ at equal
solve-rate** — never a rise in solve-rate.

**False-block**
The opposite error: the layer **rejected** (or failed to confirm) a change that was actually
correct. False-blocks matter because an instrument that over-blocks can fake a low
false-accept rate. Hunting and fixing false-blocks is part of proving the instrument is
trustworthy.

**Independent oracle**
The external standard of correctness a change is measured against (e.g. a benchmark's
reference tests), kept **separate** from anything the agent or the verification layer could
influence. Numbers only mean something relative to an oracle the system could not study for.

**Held-out evaluation**
A frozen, seeded task set, with **no overlap** with any set used during development, run once
to produce the publishable number. Development ("dev-set") observations are feedback, not
evidence — the headline figure comes only from the held-out run.

**Calibration**
Tuning the verification so its confidence matches reality: a confident *accept* should
correspond to a genuinely conforming change, and uncertainty should surface as *review*
rather than a false *accept*. A mis-calibrated instrument reports trust that isn't there.

---

## How the verdict is formed

**Independent verification**
Forming the admission decision from evidence the agent **never controlled** — rather than
from the agent's self-report. The premise of the whole framework.

**Self-referential test**
A test the agent writes for its own change. It passes for a correct fix *and* for a
confidently wrong one, so it carries no independent signal about whether the change should be
trusted. Independent verification exists precisely because self-referential evidence does
not.

**Fix-blind acceptance test**
An acceptance test authored from the **stated requirement only**, without sight of the
agent's fix (or of the hidden oracle). Because it is blind to the solution, passing it is
evidence *about the requirement*, not about the agent's narrative.

**Regression check**
Verification that the change does not break behavior that previously worked — the second half
of "conforms": a change can satisfy its own goal and still be a false-accept if it regresses
something else.

**Leak-safety**
The guarantee that the verification process never sees or touches the hidden oracle it is
measured against — it cannot "study for the test." Without leak-safety, a high pass rate is
meaningless.

**Reproducible verdict**
The same evidence yields the same decision, accompanied by an archivable trace of *why*. A
reproducible decision can be audited; a probabilistic opinion cannot.

---

## The decision

**Tri-state decision**
The output is three-state, not two: an "answer or escalate" system that knows when it does
not know.

> **accept · review · reject**

- **accept** — independently verified as conforming.
- **review** — conforms as far as can be independently checked, but the specification
  under-determines the rest; a human should look. (Internally this honest "I can't fully
  vouch" state may be labelled differently; the **public** wording is *review* / *needs
  review* / *escalate* — never "insufficient evidence," because the layer *does* have
  evidence; it simply covers only the specified part.)
- **reject** — the independent check contradicts the change (fails the acceptance test or
  regresses).

**Escalation**
The deliberate hand-off to a human when verification cannot honestly reach *accept* or
*reject*. The value of *review* is that it makes "not sure" an explicit, trackable outcome
instead of a silent false-accept.

---

## The three components of the asset

**Trust Benchmark**
A reproducible method to measure false-accept (and related trust signals) on an independent
task set. Answers "how trustworthy is this admission process?" in numbers.

**Trust Controller**
The admission/verdict layer that applies the principle inside the engineering process:
independent, leak-safe verification → tri-state verdict → repository. The Controller is
implementable by others; the compounding part is the measurement methodology around it.

**Trust Evidence**
The reproducible cases, calibrations, and results that show *why the measurements can be
trusted* — controls, leak-safety checks, and the false-block hunt. A trust metric must
itself be trustworthy, and this is where that is demonstrated.

---

## Cross-reference

| Concept | Where it's discussed |
|---------|----------------------|
| Capability vs trust, the process principle, the objections | [MANIFESTO.md](MANIFESTO.md) |
| Self-referential test, independent / leak-safe verification, tri-state | [MANIFESTO.md](MANIFESTO.md) |
| What is **not** yet proven; held-out status; threats to validity | [Current Scope & Limitations](CURRENT_SCOPE_AND_LIMITATIONS.md) |
| The verdict logic, illustrated interactively | [the sim, in your browser](https://kolesnikov-arch.github.io/patchward/sim/) |
