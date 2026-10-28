# Contributions — Kickazzman

All contributions listed here were posted under the handle Kickazzman.
No personal information is included on this page: no real names,
emails, locations, console identifiers, network details, or private
project internals. Statuses are as of the last verified check on
2026-10-23/24; live status has not been re-checked, because the
usual push route is currently unavailable.

Total: 37 issues, plus 1 pull-request comment.

## First contributions — 2026-10-23

- **pastawithpesto/PS5-14.10-Jailbreak-Research #21** — Stage-1
  two-size clarification, Cut 1 boundary persistence, and the
  VCAND save()-fault status.
- **ZigZagBoi1/PS5-14.10-Research #118** — msync closure, with
  the 124a banner trap included; fork-line data credited to its
  original source.
- **pastawithpesto/PS5-14.10-Jailbreak-Research #22** — Lane A
  correction: alias and controlled-field read/write hold;
  "full R/W" / Stage 2 claims refuted from the repo's own
  documents; save()/realizeSaves() documentation fix included.
- **ZigZagBoi1/PS5-14.10-Research #122** — AIO documentation lag,
  companion to #118, with the 352-series evidence.
- **ZigZagBoi1/PS5-14.10-Research #123** — SCM_RIGHTS drop-leak
  finding note (151d/151e; file-descriptor counter 34 to 46),
  with the Finding 75 degradation caveat carried.

## Audit corrections, batch 2 — 2026-10-23

Posted in order. Pesto items are #23–#39; Zig items are
#124–#135. Each was re-verified against a fresh clone before
posting; one further candidate (Z10) failed verification and
was not posted.

- **pastawithpesto/PS5-14.10-Jailbreak-Research #23** — FINDINGS.md contradicts itself on unitsPerEm=0 (T11): REJECTED at :111 vs loads-and-renders at :91 — the beacon log sides with :91
- **pastawithpesto/PS5-14.10-Jailbreak-Research #24** — Font loca OOB: two incompatible verdicts both 'device-confirmed' (V180A vs V260) — neither has a log in the repo
- **pastawithpesto/PS5-14.10-Jailbreak-Research #25** — CSSFontFace UAF: three incompatible stories in-repo (TESTING / CONFIRMED via re-entry / DoS-only, no re-entry) — no p458 or p504 result exists
- **pastawithpesto/PS5-14.10-Jailbreak-Research #26** — Canvas CVE-2026-43720: no V527-V630 beacon log committed in results/ (trails live in issue #11 / PR #14); mechanism and alias index disagree across docs
- **pastawithpesto/PS5-14.10-Jailbreak-Research #27** — State-buffer AB reclaim listed as confirmed — every recorded attempt (v587/v589/v620/v627) crashed during spray
- **pastawithpesto/PS5-14.10-Jailbreak-Research #28** — OOB state-stack 'strong info leak candidate' in CONFIRMED_VULNS summary should carry FINDINGS:145's probe-needed status
- **pastawithpesto/PS5-14.10-Jailbreak-Research #29** — tee() 'OOB read 8 bytes past the Vector' (CONFIRMED_VULNS §3) refuted in-repo — teardown nulls the slots; the crash is a null deref
- **pastawithpesto/PS5-14.10-Jailbreak-Research #30** — ATTACK_SURFACE lists BYOB readers as available — five other docs record BYOB as not implemented on 14.10
- **pastawithpesto/PS5-14.10-Jailbreak-Research #31** — README:144's heap paragraph inverts the repo's own model (MADV_FREE decommit; release assertions)
- **pastawithpesto/PS5-14.10-Jailbreak-Research #32** — WebContent memory ceiling stated three incompatible ways (~500MB / ~1200MB held / ~500MB-live) — never reconciled with the V150 runs
- **pastawithpesto/PS5-14.10-Jailbreak-Research #33** — MetadataTable dispatch guide's body still teaches the wrong stride (96 / N=44,739,243) its appendix corrects (112 / N=38,348,816)
- **pastawithpesto/PS5-14.10-Jailbreak-Research #34** — p149g read as both 'CONFIRMED DEAD' (STATUS-REPORT-v80) and proof the sweep is alive (EXPLOIT-PLAN / VP_DEAD_END_INVESTIGATION)
- **pastawithpesto/PS5-14.10-Jailbreak-Research #35** — RESEARCH_MAP is a generation behind: CSSFontFace 'best lead', Stage 2 'not reached', Canvas CVE-2026-43720 absent
- **pastawithpesto/PS5-14.10-Jailbreak-Research #36** — KERNEL_AUDIT keeps UMTX CVE-2024-43102 Tier-1 'not verified' — DEAD_ENDS already closed it (SHM stubbed on 14.10)
- **pastawithpesto/PS5-14.10-Jailbreak-Research #37** — API_FINGERPRINT claims thr_create works from the browser (8 threads, child execution) — no probe, beacon, or log in tree, history, or issues
- **pastawithpesto/PS5-14.10-Jailbreak-Research #38** — Re-entrancy audit's F1-F10 'CONFIRMED' rest on upstream fixes alone — no device results in-repo; unreconciled with adoption-scoped SAFE verdicts
- **pastawithpesto/PS5-14.10-Jailbreak-Research #39** — Phase-0 'golden primitive' is 'CONFIRMED viable' while its own table lists p150f/p151a/p152a READY (never run) — plus V655 data and progress.json hygiene

- **ZigZagBoi1/PS5-14.10-Research #124** — Threading record: Finding 2 'eliminated entirely' + README thr_new wall falsified by the repo's own results (156c/156d, 383a, 136 race files)
- **ZigZagBoi1/PS5-14.10-Research #125** — PROGRESS_AUDIT rests points on probes 274c/274e/274f that exist nowhere, and a set_mcontext root cause withdrawn 2026-10-21
- **ZigZagBoi1/PS5-14.10-Research #126** — CVE-2026-58093: two of three stated blockers are dead in-repo; the surviving tty blocker should cite probe 58d
- **ZigZagBoi1/PS5-14.10-Research #127** — r230171 spent three incompatible ways (FreeBSD 9.x / ~11.x era / bare identity) — the CVE-2026-58090 closure rests on the 9.x mapping alone
- **ZigZagBoi1/PS5-14.10-Research #128** — DEAD_ENDS contradicts itself on AIO (:18 vs :89); ATTACK_SURFACE's msync table row (:136) contradicts its own header
- **ZigZagBoi1/PS5-14.10-Research #129** — Corpus accounting: README '518, not fully run' vs WEBKIT_CORPUS '507/510 over 509' — and the cited results/webkit/ logs exist in no revision
- **ZigZagBoi1/PS5-14.10-Research #130** — TODO's PMU chain presents 13.60 decompile readings as device fact — the only device survey (128a) shows no MSR write
- **ZigZagBoi1/PS5-14.10-Research #131** — Status-hygiene cluster: dated docs preserving pre-measurement states (49418 protocol, GOLD_VECTORS, NOVEL_ATTACK_CHAINS, 49422, Finding 13, README, Oct-16 report)
- **ZigZagBoi1/PS5-14.10-Research #132** — Thread budget is not a fixed '8 children max' — CHANGELOG correction + 242a measured ceilings of 25/11/9 per loader
- **ZigZagBoi1/PS5-14.10-Research #133** — Finding 81's lethal trio and Finding 1's execute-only scope both fail against the repo's own captures (353a/353b, 56l, 272a/56d)
- **ZigZagBoi1/PS5-14.10-Research #134** — The 'unmeasured' remainder was measured: 530-532/537, the 677-734 tail (57a), and UMTX op 19 all have captures in-tree
- **ZigZagBoi1/PS5-14.10-Research #135** — Status-line/aggregate hygiene: 45258 status line vs its own 54a result; ALL_PROBES/ALL_RESULTS frozen 2026-10-18; TODO Priority 0; PANIC_ORACLE's missing watchdog log

Zig issues #118 and #122–#135 were observed closed in a sweep on
2026-10-23; the contents of their closing comments were not
read at that time.

## Later contributions — 2026-10-23

- **pastawithpesto/PS5-14.10-Jailbreak-Research #40** —
  save()-model correction: the Phase-4 save() expectation is
  source-false, plus the bindings-gap note (the generated
  bindings layer is absent from the source drop).
- **pastawithpesto/PS5-14.10-Jailbreak-Research #41** — C-18 /
  C-19 contribution, with device updates: C-19 device-confirmed,
  C-18 v2 device-confirmed silent branch. Open at last check.
- **pastawithpesto/PS5-14.10-Jailbreak-Research #43** — C-20
  device-confirmed plus the C-21 cluster, dispositioned with
  fences intact (CSS member device-confirmed; EventTarget
  source-only; SerializedScriptValue fenced; JSCell not-a-bug;
  TransformStream fenced). Open at last check.
- **Comment on pastawithpesto PR #120** — dmem1 grade / comment.

## In this repo

- `README.md` — public package overview.
- `STAGE1-RECONCILIATION.md` — stage-1 reconciliation.
- `NUMBERS-AUDIT-2026-10-23.md` — numbers audit.
- `FEEDBACK-LOG.md` — community feedback log; claims enter as
  unverified and are re-derived before moving any document.
- `SHORTLIST-002` — published shortlist (scrubbed public copy).
- `READ-MEASUREMENTS-11.40.md` — read measurements on 11.40
  (worker clock, C-20 splice map, ruler, survey, census,
  mechanism, differential, and the C/D 32-byte shift).
  STAGED, pending push with this page — not yet live at the
  time this file was written.

## Deliberately not on this page

- The private campaign record.
- Multiplex and federation internals.
- Home infrastructure details and console/account identifiers.
- Any personal information.

