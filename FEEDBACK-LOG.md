# Community Feedback Log — PS5 14.10 Research Line

Every substantive piece of community feedback on the public package (issues,
PRs, comments, replications, corrections) gets logged here and AUDITED the
same way our own numbers are: a claim enters as UNVERIFIED, gets re-derived
against primary sources, and only then moves a document.

| Date | Source (repo / handle) | Item | Claim | Audit verdict | Action taken |
|---|---|---|---|---|---|
| — | — | — | (awaiting first feedback) | — | — |

Rules:
- Feedback is evidence, not authority — verify before adopting, exactly as
  with our own results.
- Corrections to our documents land as dated footnotes, never silent rewrites.
- Credit every contributor by handle in the document their feedback improves.

## Contributions out (this line → upstream)

Standard (set by the account owner, 2026-10-23): we share and publish only what we
know to be true — re-derived against primary sources before it goes out — and
everything that is actually contributable gets shared.

- 2026-10-23 — msync(65) MS_INVALIDATE closure + docs-lag note, filed upstream:
  https://github.com/ZigZagBoi1/PS5-14.10-Research/issues/118
- 2026-10-23 — Stage 1 two-size clarification (768 B slot vs 720 B dash buffer) +
  boundary-persistence measurement + VCAND save()-fault status, filed upstream:
  https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/21
- 2026-10-23 — Lane A audit of the CONFIRMED_VULNS "full R/W" claim vs the frozen
  WK-1400 source (alias + controlled-field R/W hold; arbitrary R/W does not;
  IsoHeap internal contradiction + save()/realizeSaves() docs fix), filed upstream:
  https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/22
- 2026-10-23 — AIO docs-lag correction (the 662-670 sweep ran 2026-10-22; family
  live/functional), filed upstream as companion to #118:
  https://github.com/ZigZagBoi1/PS5-14.10-Research/issues/120
- 2026-10-23 — SCM_RIGHTS drop-leak extracted as a standalone finding note:
  https://github.com/ZigZagBoi1/PS5-14.10-Research/issues/121
- 2026-10-23 — SHORTLIST-002.md published in this repo (D3 second layer,
  WRAPPED column, label intact).
