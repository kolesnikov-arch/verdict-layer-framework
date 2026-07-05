# Verdict Layer Framework

**🇺🇸 English | [🇨🇳 简体中文](README_zh.md)**

A measurement-first framework for **trust in AI-generated changes** — patterns and
standards for deciding which AI changes an engineering organization can safely admit.

## The reframe

Most of the field measures one axis — **capability**: *can the agent solve the task?*
(resolve rate, pass rate). That is a property of the model. It is not the question an
engineering organization has to answer before code reaches main.

> **Capability asks: "Can the agent solve the task?"**
> **Trust asks: "Can the organization safely accept the change?"**

**Trust is a property of the engineering *process*, not of the model.** This framework is
about that second axis.

Operationally, so the word can't drift into "governance":

> **Trust = the probability that an automatically admitted AI change actually conforms to
> the stated requirements** (measured as `1 − false-accept rate` on an independent oracle).

## Why a second axis

A test an agent writes for its own change is self-referential — it passes for a correct
fix *and* a confidently wrong one. As AI autonomy rises, human review stops being a
complete inspection and becomes a **sampling process**. So the cost of a single silently
accepted wrong change grows faster than the cost of generating the code. That is where an
independent admission decision earns its place.

The decision is **three-state, not two** — an "answer or escalate" system that knows when
it does not know:

> **accept · review · reject**

## Status — honest by construction

This is an active research effort. A trust project that hides its limits has already
failed its own thesis, so the limits come first:

- The headline number comes from a **frozen, independent held-out evaluation**, completed
  2026-07-05 against a [pre-registered scoring contract](https://github.com/kolesnikov-arch/patchward/blob/main/PREREGISTRATION.md)
  published before the outcome existed: on 50 held-out tasks, the same model **silently
  shipped 17/50 wrong fixes ungated vs 0/50 gated** — full results, confidence intervals,
  disclosed costs, and reproducible artifacts in
  **[patchward — held-out results](https://github.com/kolesnikov-arch/patchward/blob/main/RESULTS.md)**.
- One held-out evaluation so far; validated on a public software-engineering benchmark
  only, not production CI.
- See **[Current Scope & Limitations](CURRENT_SCOPE_AND_LIMITATIONS.md)** before drawing
  any conclusion.

## What this is

Abstracted patterns and standards for building an independent trust/admission layer for
AI-generated changes. They are **not** a product (there is no code to install), **not** a
startup pitch, and **not** implementation-specific (tool names, stage names, prompts, and
internal logic are deliberately omitted).

What is public is the **method and the proofs**; the implementation is not the object of
publication. When results are ready, reproducibility means two things: *verify our
published evaluation artifacts*, and *measure your own trust* with the method — never
*reproduce our controller*.

## Contents

| Document | What it covers |
|----------|---------------|
| [Verdict Layer Manifesto](MANIFESTO.md) | The reasoning: independent verification over self-report |
| [Current Scope & Limitations](CURRENT_SCOPE_AND_LIMITATIONS.md) | What this work does **not** yet prove |
| [Glossary](GLOSSARY.md) | Definitions for every term on the trust axis |
| [Architecture Logic Simulation](architecture_logic_sim/README.md) | An interactive walkthrough of the tri-state verdict logic |

> This is the theory layer, kept intentionally minimal. Earlier architecture-pattern drafts
> that did not serve the trust thesis have been removed; their history remains in git.

## Who this is for

- CTOs / VP Engineering weighing how to safely accept AI-generated changes
- Platform & enabling teams designing AI-delivery admission controls
- Engineering leaders who want a measurable property, not slides

## Author

**Dmitriy Kolesnikov.**
**Contact:** [kolesnikov.arch@gmail.com](mailto:kolesnikov.arch@gmail.com)  ·
[LinkedIn](https://www.linkedin.com/in/dmitriy-kolesnikov-631b67169) ·
[X @kolesnikov_arc](https://x.com/kolesnikov_arc) ·
[Newsletter: Trust in AI Delivery](https://dmitriykolesnikov.substack.com)

## License & Usage

Published under **Creative Commons Attribution-NonCommercial 4.0 International
(CC BY-NC 4.0)**. You may read, study, cite, and use these blueprints for internal
organizational governance. Commercial use, resale, consulting, derivative commercial
products, or training offerings require written permission via the contact above. See
[LICENSE](LICENSE).
