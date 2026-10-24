# Community Feedback Log — PS5 14.10 Research Line

Every substantive piece of community feedback on the public package (issues,
PRs, comments, replications, corrections) gets logged here and AUDITED the
same way our own numbers are: a claim enters as UNVERIFIED, gets re-derived
against primary sources, and only then moves a document.

| Date | Source (repo / handle) | Item | Claim | Audit verdict | Action taken |
|---|---|---|---|---|---|
| 2026-10-24 | pesto / #41 | sizeof thread: libpas OFF, State-inline, 768B context, 272B refuted, FontVariantAlternates 72B | VERIFIED (libpas OFF both drops; Vector<State,1> :436; 272B fails inventory lower bound; FVA 4 strings, 72B aligned); 768B CONVERGENT (measured slot vs computed class, not independent proof) | Reply posted: https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/41#issuecomment-6384795096; IsoSpace inference struck from our survey-v2 record (dated footnote) |
| 2026-10-24 | pesto / #43 | Canvas-chain note: V701 10/10 UAF, same-type alias idx 4, cross-type 0/10; sizing question | Device data filed as pesto's bench (UNVERIFIED by us); sizing mooted by context-not-State correction | Reply posted: https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/43#issuecomment-6384795279 |
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
- 2026-10-23 — C-18/C-19 filed (source findings with desktop reproduction,
  device occurrence unproven, labeled as such): BMP RLE absolute-mode OOB
  read + Yarr {0}-elision dangling forward reference from the 61-file
  diff grading: https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/41
- 2026-10-23 — Device update on Issue #41: C-19 CONFIRMED on a retail
  11.40 (2/2 deterministic WebProcess kills at the predicted compile
  step, control clean); C-18 not exhibited via the <img> path (empty
  frame, survived) — device status remains unproven:
  https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/41
- 2026-10-23 — C-18 v2 update on Issue #41: v1's empty frame explained
  (missing RLE terminator -> frame never committed; v1 = no test
  performed, replicated once more by accident); trigger v2 confirms
  the OOB read ON DEVICE via the pre-registered silent-branch checksum
  (PIXSUM 9a5d6681, alpha 24, survived) — claim fenced to rendered
  output with a zero-filled landing; live-heap return not shown:
  https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/41
- 2026-10-23 — Issue #43 (new): completing the WK-1200 diff — C-20 XML
  re-entrancy DEVICE-CONFIRMED on 11.40 (double-parented node witnessed
  by the document's own script, 3/3, control sane; teardown escalation
  not claimed) and the C-21 CSS member DEVICE-CONFIRMED (nesting
  enabled in the Guide build — precondition settled on device; 10k-deep
  stylesheet kills the web process every load), with the rest of the
  cluster dispositioned in the same post: EventTarget SOURCE-ONLY,
  SerializedScriptValue FENCED, JSCell NOT-A-BUG (60,037-check battery),
  TransformStream FENCED:
  https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research/issues/43
- 2026-10-23 — Community columns received on #41/#43 from cobrajet302gt
  and answered: (a) C-19 CLEAN on retail 14.10 (7/7 loads, same Guide
  surface) — the fixed column the source hunk predicts; (b) C-18 on
  14.10 corrected by its author to UNTESTED (pre-v2 shapes = no test
  performed; 1400 indexes runs relative to startX, so absolute-column
  triggers steer nothing); our trigger-v2 blob (122 B, md5 ef8b8ac6...)
  supplied as hex in our reply for their byte-exact run, with the
  committed-control scoring gate; (c) source-level closure posted for
  both #41 findings (the exact 1400 fix hunks); (d) #43: C-20 fix hunk
  verified line-exact and C-20 + C-21 CSS filed FIXED on 14.10 (C-20
  parse stops 3/3; CSS nesting enabled but capped, DONE arrives 2/2);
  the C-21 gate mechanism sharpened (rule-list counter at the head of
  consumeStyleRule; m_styleRuleNestingLevel boolean-only in both
  generations); m_isAlwaysNestedContext recorded as an UNVERIFIED
  bypass lead. Pesto acknowledged the C-19 confirmation on #41.
