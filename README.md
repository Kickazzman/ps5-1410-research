# Public package v1 — a two-bench PS5 14.10 research program

**Prepared 2026-10-23. Prepared only: as of preparation, this package has not been posted anywhere.**

## Contents

| File | What it is |
|---|---|
| `README.md` | This file — provenance, methods, and the scrub statement. |
| `STAGE1-RECONCILIATION.md` | A community-facing note reconciling our program's records with the public Stage 1 identification of CVE-2026-43720, resolving the 720/768 size discrepancy, and offering a boundary-persistence finding and a harness-mortality lesson. |
| `NUMBERS-AUDIT-2026-10-23.md` | A full audit of every load-bearing number in the program's own documents, re-derived against primary sources: 149 claims — 116 verified, 23 corrected (14 distinct errors), 10 unverifiable. Included as the worked example of the correction discipline described below. |

## Provenance

This package comes from a two-bench independent research program into PS5 firmware 14.10 (with a second, sealed console on 11.40 used as a comparison oracle), run during October 2026. The two benches are independently owned and operated; each ran its own tooling, and results crossed between them as files for independent re-derivation. The documents were authored by the program's research assistant on the operators' instructions; the audit was ordered by an operator after a wrong number (see the reconciliation note) reached him in a summary, and its scope was the assistant's documents — never the other bench's programs, which served as primary sources.

## Methods

Three disciplines produced everything in this package, and we state them because they are the actual contribution as much as any single finding:

1. **Deterministic re-derivation.** A claim is trusted in proportion to how much of it a deterministic procedure can reproduce from primary sources — device logs, probe source code, file hashes. Where the original analysis scripts survived, the audit re-ran them unmodified on the same inputs; the strongest verifications in the audit are bit-identical re-runs. A final gate is a re-derivation, not a judgment.
2. **A prediction registry.** Forecasts are registered before probes run, with stated probabilities, and Brier-scored after — published either way, including a scored-false forecast that appears in the reconciliation note.
3. **Corrections by dated note, never by rewrite.** When a number in a living document is found wrong, the original text stands and a dated correction is appended, naming the old value, the true value, and the source. The audit's corrections section gives each error's blast radius: which conclusions rested on it and whether they survive.

## Scrub statement

This package was prepared for public release and scrubbed before packaging:

- No network addresses (public, private, or overlay) and no hardware addresses.
- No hostnames, local usernames, or personal names.
- No access secrets or sign-in mechanics of any kind.
- No console identifiers or service-subscription details.
- No internal infrastructure detail beyond the plain fact that the program ran on two benches.

In the audit copy, local file paths and internal project codenames were generalized to generic descriptors; **no number, verdict, or finding was altered by scrubbing**. The package was re-scanned after scrubbing for address patterns and identifier terms, with zero hits. The underlying logs, code, and unscrubbed documents remain on the benches; what else is released, and where, is the operators' decision.
