# Current Scope & Limitations

What this work does **not** yet show — listed first, on purpose. A trust project that hides
its limits has already failed its own thesis.

This page states the **thesis-level** limits. The detailed, measurement-level limitations of
the specific benchmark and runs live with the evidence, in
[patchward](https://github.com/kolesnikov-arch/patchward).

## Scope of the claim

- **Benchmark, not production.** The thesis is validated against an independent benchmark
  oracle — **not** a live CI or a real production merge. Whether a benchmark false-accept
  predicts real engineering risk is the top open question, not a settled fact.
- **One ecosystem so far.** Validation to date is within a single language ecosystem; nothing
  is claimed about others yet.
- **The number is held-out-only.** The published headline comes from a frozen, independent
  held-out evaluation completed against a pre-registered contract
  ([results](https://github.com/kolesnikov-arch/patchward/blob/main/RESULTS.md)); development
  observations remain feedback, not evidence. One held-out evaluation exists so far —
  replication is future work.

## Threats to validity (thesis level)

- **Construct validity:** the oracle is a *proxy* for "the change is correct." A change can
  satisfy or violate it without that perfectly matching real-world correctness or risk.
- **External validity:** results are from one benchmark and one ecosystem; generalization to
  other languages, repositories, task formats, and live CI is unproven.
- **The instrument must be trusted too:** a trust metric is only as good as its calibration
  and leak-safety. Verifying the instrument (calibration, leak-checks, the deliberate
  false-block hunt) is treated as part of the proof — the evidence repo shows how.

## Negative results are retained

Hypotheses that fail validation are kept as part of the project history, not deleted. The
measurement evolves through rejected assumptions as much as confirmed ones.

## What we explicitly do NOT claim

- We do **not** make the model smarter or raise solve rate — by design; the value is on the
  trust axis, not capability.
- We do **not** claim to define an industry standard. We publish reproducible measurements;
  adoption, if any, is earned later.
- We do **not** claim novelty of the *concept* of admission control. The claim is a
  calibrated, leak-safe, independently verifiable **measurement** of trust, with the evidence
  to back it.
