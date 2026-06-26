# Changelog

All notable changes to the Verdict Layer Framework will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-06-26

Re-conceived from an "AI governance" pattern collection into a focused **trust-measurement**
framework. The organizing question is no longer governance mechanics but a single axis:
*can the organization safely accept the change an agent produced?* — measured as
`1 − false-accept rate` on an independent oracle.

### Changed
- **README, MANIFESTO, GLOSSARY rewritten to the trust axis.** Capability vs trust, the
  process principle, self-referential tests, independent/leak-safe verification, and the
  tri-state decision (accept / review / reject) are now the spine of the documents.
- **Architecture Logic Simulator re-skinned to the tri-state verdict.** Three scenarios —
  verified → accept, underspecified → review, confidently-wrong → reject — illustrate why a
  self-authored test cannot establish trust and how an independent verdict is formed.

### Added
- **Current Scope & Limitations** (EN + zh) — an honest, limits-first statement: benchmark
  (not production), one ecosystem, held-out number pending, threats to validity. A trust
  project that hides its limits has already failed its own thesis.

### Removed
- **Swarm / sovereign / token-economics material** (the Sky & Governant distributed topology,
  the "communication tax" telemetry, the sovereign-compute infographics) — it did not serve
  the trust thesis and diluted it.
- **The governance-pattern docs and standards** (automation-boundary, governance-foundations,
  sandboxed-worker, event-log schema, directory-layout, self-validating-governance, the
  branching/code-review/release standards, and the framework-internal ADRs). Their history
  remains in git; the theory layer is intentionally minimal.
- **Unverifiable empirical claims** (e.g. "0% escape across N governed runs", accept-rate /
  pass-rate figures). No quantitative result is published until the frozen held-out evaluation
  completes.

## [1.0.0 – 1.3.0] - 2026-06-05 … 2026-06-12

Earlier releases framed the repository as an "AI governance" pattern collection, with a
distributed multi-node topology and R&D telemetry as its centerpiece. That framing was
superseded by the 2.0.0 trust refocus above. The full entry-by-entry history is preserved in
git; it is summarized here rather than reproduced, to keep the changelog on the trust thesis.
