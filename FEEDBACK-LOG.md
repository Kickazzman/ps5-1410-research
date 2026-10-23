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
  https://github.com/ZigZagBoi1/PS5-14.10-Research/issues/122
- 2026-10-23 — SCM_RIGHTS drop-leak extracted as a standalone finding note:
  https://github.com/ZigZagBoi1/PS5-14.10-Research/issues/123
- 2026-10-23 — SHORTLIST-002.md published in this repo (D3 second layer,
  WRAPPED column, label intact).
- 2026-10-23 — BATCH 2: the 30 sweep contributables were independently
  re-verified against fresh clones at the pinned HEADs (pesto eb68f95, Zig
  1b304052), with git-history + issues/PRs searches behind every absence claim.
  Result: 25 VERIFIED + 4 VERIFIED-SCOPED posted; 1 FAILED (Z10) not posted.
  Pesto (pastawithpesto/PS5-14.10-Jailbreak-Research):
  P1 unitsPerEm flip -> #23 (VERIFIED); P2 loca OOB both-ways -> #24 (VERIFIED);
  P3 CSSFontFace three stories -> #25 (VERIFIED);
  P4 Canvas logs not committed -> #26 (VERIFIED-SCOPED);
  P5 state-buffer reclaim crashes -> #27 (VERIFIED);
  P6 OOB leak promotion scope -> #28 (VERIFIED-SCOPED);
  P7 tee() mechanism refuted -> #29 (VERIFIED); P8 BYOB listed available -> #30
  (VERIFIED); P9 README heap paragraph -> #31 (VERIFIED);
  P10 memory ceiling x3 -> #32 (VERIFIED); P11 dispatch stride -> #33 (VERIFIED);
  P12 p149g dead/alive -> #34 (VERIFIED); P13 RESEARCH_MAP stale -> #35
  (VERIFIED); P14 UMTX Tier-1 -> #36 (VERIFIED);
  P15 browser thr_create claim -> #37 (VERIFIED);
  P16 re-entrancy audit scope -> #38 (VERIFIED-SCOPED);
  P17 golden primitive hygiene -> #39 (VERIFIED).
  Zig (ZigZagBoi1/PS5-14.10-Research):
  Z1 threading record -> #124 (VERIFIED); Z2 progress audit 274-series -> #125
  (VERIFIED); Z3 58093 blockers -> #126 (VERIFIED-SCOPED);
  Z4 r230171 premise -> #127 (VERIFIED); Z5 reference-doc self-contradictions
  -> #128 (VERIFIED); Z6 corpus accounting/logs -> #129 (VERIFIED);
  Z7 TODO PMU chain -> #130 (VERIFIED); Z8 status-hygiene cluster -> #131
  (VERIFIED); Z9 thread budget -> #132 (VERIFIED);
  Z11 lethal trio + XOM scope -> #133 (VERIFIED);
  Z12 unmeasured remainder -> #134 (VERIFIED);
  Z13 status-line/aggregate hygiene -> #135 (VERIFIED).
  Z10 (/dev counts) FAILED re-verification — a 79-entry listing DOES exist
  (results/phase17_new_vectors/295a_jail_inventory_20261022_111637.txt, PR #85),
  falsifying the sweep's "no 79-node listing" claim. NOT posted; the sweep doc
  carries a dated correction footnote.
- 2026-10-23 — fa-v568 save()-model correction + bindings-gap note (from the
  VCAND audit: Base.h:143 increments unconditionally; device save-path death
  eliminates to the generated-bindings layer absent from the source drop):
  https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/40
- 2026-10-23 — Attribution-strengthening comment on ng643's PR #120 (dmem1
  crash surface; behaviour graded supported-by-own-evidence in our DMEM1
  grade; five items to move the panic mechanism from claimed to shown):
  https://github.com/ZigZagBoi1/PS5-14.10-Research/pull/120
