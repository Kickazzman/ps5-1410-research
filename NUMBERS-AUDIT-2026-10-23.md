> **Public-package copy (2026-10-23).** This is the campaign numbers audit with local paths, hostnames, usernames, hardware addresses, and internal project codenames generalized for release. Every number, verdict, and finding is unchanged from the original.

# NUMBERS AUDIT — every load-bearing number in the campaign documents, re-derived

**Order:** the project owner, 2026-10-23 06:41 EDT — "Audit every load-bearing number in my documents against primary sources."
**Scope:** the assistant-authored documents only — `~/workspace/campaign-docs/*.md`; the Bench M shared workspace `derived/*.md` (byte-identical copies audited once, identity md5-checked); `~/llm/staging/` CAMPAIGN / SURVEY / SURVEY-2 / MANIFEST on Bench M; the campaign entries (Q-RE / T-RE / E-RE) in `~/workspace/research-registry.md`. The second bench's programs are **not** under audit — only the assistant's claims about them. Read-only everywhere; Bench H reached via Bench M (`over SSH`).
**Method:** a number is load-bearing if a conclusion, design, or decision rests on it. Each was re-derived deterministically from the primary source — his code, his logs, our logs, the files themselves — by script, never by re-reading the document's own arithmetic. Where the original analysis scripts survived (`keys1.py`, `keys_a6v2.py`, `cut1_run.py`, `shaping.py`, `triage.py`), they were re-run unmodified on the same inputs.
**Verdicts:** **VERIFIED** = re-derived value matches. **CORRECTED** = wrong; true value given, with a dated footnote appended to the living document (listed at the end). **UNVERIFIABLE** = the primary source no longer exists or never did; what would be needed is stated.

## Headline findings

1. **The campaign's quantitative core is sound.** The key-shaping statistics (A6/A9/A14, CUT1), the triage, the trial scorekeeping, the staged-file hashes, the offsets clone finding, the door censuses, and the webview constants all re-derive **exactly** — in most cases by re-running the original deterministic scripts and getting bit-identical output.
2. **Two systematic error classes account for almost every wrong number:**
   - **Representation double-counting.** His https.log writes every beacon twice (a GET line and a BEACON line). Three documents counted lines as events in some places (killers: 8 starts for 4; canary suite: 116 starts for 58) while counting events correctly in others.
   - **Copy-timing (prefix) drift.** His logs grow continuously; several documents counted from different morning pulls of the same log without stating the cut time, so their counts differ from each other by minutes of live traffic. Every such count in this audit was reproduced as an exact **prefix** of the surviving log at a consistent cut (~07:05–07:30 EDT, 2026-10-22) — the numbers were right for their copies; the copies weren't labeled.
3. **Calibration row — the "720 B canvas block."** The 2026-10-23 correction itself was verified against his code: `heapprobe.html` line 18 ("buffer = Vector<double> (fastMalloc/bmalloc, NOT gigacage), 90 doubles = 720B") and line 78 ("cc.setLineDash(f); // 90 doubles = 720B fastMalloc alloc: reclaim shot") — **720 B is the setLineDash dash-vector buffer (90 doubles × 8 B)**; the freed context object's slot is **768 B** per the public 14.10 research repo. His own comment calls the 720 B buffer "same size class as the freed block." Both numbers are exact — for two different allocations. The mislabel lived only in assistant prose (`candidate-set-v2-DRAFT.md` §1, footnoted).

## Summary counts

| Document set | Claims audited | VERIFIED | CORRECTED | UNVERIFIABLE |
|---|---|---|---|---|
| A. Workspace `campaign-docs/*.md` (+ byte-identical shared workspace copies) | 118 | 95 | 15 | 8 |
| B. Shared workspace-only documents | 5 | 4 | 1 | 0 |
| C. staging (CAMPAIGN / SURVEY / SURVEY-2 / MANIFEST) | 20 | 15 | 4 | 1 |
| D. research-registry campaign entries | 6 | 2 | 3 | 1 |
| **Total** | **149** | **116** | **23** | **10** |

The 23 CORRECTED rows reduce to **14 distinct errors** (the killers double-count alone appears in 7 rows across 4 documents). No CORRECTED number reverses a campaign conclusion; two conclusions weaken (killers replication strength; the watchdog "doubling" economics — see Corrections).

## Full table

Verdict key: V = VERIFIED · C = CORRECTED · U = UNVERIFIABLE. "Prefix" = the value reproduces exactly as a prefix of the surviving log at the stated cut.

### Set A — workspace documents

| # | Document | Claim | Claimed | Re-derived | V | Primary source |
|---|---|---|---|---|---|---|
| 1 | KEY-SHAPE-v1 | Lottery exclusion | 0.000000 bits (1.23×10⁻¹² computed) | 1.2301×10⁻¹² bits → NON-SHAPING | V | shaping.py rerun |
| 2 | KEY-SHAPE-v1 | A2 Fermi p=1/40, n=120, 0 hits | REFUTED, P=0.0479 | 0.04792 | V | shaping.py rerun |
| 3 | KEY-SHAPE-v1 | A2 Fermi p=1/50 | SURVIVES, P=0.0885 | 0.08854 | V | shaping.py rerun |
| 4 | KEY-SHAPE-v1 | A6 attempt series | 172 serves | 172 serve beacons | V | https.log copy (Bench M /tmp) |
| 5 | KEY-SHAPE-v1 | MAPPED beacons | 29 exist | 29 | V | https.log copy |
| 6 | KEY-SHAPE-v1 | Matched results | 16 global / 15 in-segment | 16 / 15 | V | keys_a6v2.py + keys1.py reruns |
| 7 | KEY-SHAPE-v1 | Base rate | 9.3% | 16/172 = 9.30% | V | rerun |
| 8 | KEY-SHAPE-v1 | Gap-since-previous MI | 0.113 bits, p=0.001 | 0.11344, p=0.000999 | V | keys_a6v2.py rerun |
| 9 | KEY-SHAPE-v1 | Pass-position MI | 0.093, p=0.001 | 0.09285, p=0.000999 | V | rerun |
| 10 | KEY-SHAPE-v1 | Headline boundary MI | 0.098, p=0.001 | 0.09778, p=0.000999 | V | rerun |
| 11 | KEY-SHAPE-v1 | Spray MI | 0.043, p=0.014 | 0.04275, p=0.01399 | V | rerun |
| 12 | KEY-SHAPE-v1 | Pass-age MI | 0.016, p=0.057 ns | 0.01635, p=0.0569 | V | rerun |
| 13 | KEY-SHAPE-v1 | Address-magnitude control MI | 0.043, p=0.004 | 0.04289, p=0.003996 | V | rerun |
| 14 | KEY-SHAPE-v1 | A6 cross-tabs | 6/8 · 10/164 · 7/12 · 6/148 · 3/11 · 9/19 · 7/153 | identical in rerun output | V | rerun |
| 15 | KEY-SHAPE-v1 | A14 exponent | α=2.150 @ xmin=2 (n=51) | 2.14986 | V | keys1.py rerun |
| 16 | KEY-SHAPE-v1 | A14 coronium ΔLL | 46.7 for power law | 46.69 (LL −123.58 vs −170.27) | V | rerun |
| 17 | KEY-SHAPE-v1 | A14 xmin=10 / 100 | INSUFFICIENT-DATA | INSUFFICIENT-DATA (n=6, n=2) | V | rerun |
| 18 | KEY-SHAPE-v1 | A9 surprise | ≥10.97 bits, p=1/2001 | 10.9665 bits, p=0.00049975; null max mean 34.7 ✓ | V | rerun |
| 19 | KEY-SHAPE-v1 | Corpus size | 6,712 programs | 6,712 .js files | V | shared workspace Bench H/fuzz/crashes |
| 20 | KEY-SHAPE-v1 | Family distribution | 330 families; largest 5,758 (85.8%); 279 singletons; 51 ≥2; 6 ≥10; 2 ≥100; tail 954 (14.2%) | identical | V | triage.py rerun + keys1 family recompute |
| 21 | KEY-SHAPE-v1 | §6 Brier scores | 0.250 / 0.1225 / 0.250; mean 0.2075 | arithmetic exact | V | recompute |
| 22 | KEY-SHAPE-v1 | https.log size | 21,089 lines | 21,089 | V | wc -l on the copy |
| 23 | KEY-SHAPE-v1 | https.log "first line" | 2026-10-20T22:39:35 | file's first line is 2026-10-19T13:51:39 (curl test fetch); 10-20T22:39:35 is the first DASHFORGE beacon | C | the copy itself |
| 24 | KEY-SHAPE-v1 | v3 serves | reached idx 17/32 | 18 serves, idx 0–17, after the 19:50 restart | V | https.log copy |
| 25 | KEY-SHAPE-v1 | B-2 WebKit diff | 61 of 51,252 files differ | 61 differ among 51,250 common Source/ files (Source/ union = 51,252) | V | wkdrop zips, CRC comparison |
| 26 | KEY-SHAPE-v1 | B-4 idx unreliability | serves reached 17 while idx read 16→2→3 | serve records confirm; beacons are the ground truth | V | https.log copy |
| 27 | CUT1 | Persistence window | inside 14/24 = 58.3%; outside 2/148 = 1.35%; ratio 43.2×; Fisher p=1.6×10⁻¹² | identical (p=1.58×10⁻¹²) | V | cut1_run.py rerun |
| 28 | CUT1 | Binned-delta MI | 0.227 bits, p=0.001 | 0.22735, p=0.000999 | V | rerun |
| 29 | CUT1 | Delta bins | 14/24 · n=0 · 0/6 · 0/9 · 0/8 · 0/24 · 2/101 | identical | V | rerun |
| 30 | CUT1 | Naive-scan trap | W=3,564 s, ratio 5.04, p=0.0097 | identical | V | rerun |
| 31 | CUT1 | Event accounting | 567 START; 394 SWEEP-DONE; SYNCFLUSH 14 lines / 8 unique; pass-done 89 lines / 86 distinct; BOOT ×1 @ 2026-10-22T22:10:18 | identical | V | rerun + direct counts |
| 32 | CUT1 | Recovery-action components | app-exit 261 · dance 262 · poking 556 · stream-client 1 | identical under the script's patterns | V | rerun |
| 33 | CUT1 | Recovery-action total | 1,280 lines | **1,080** (sum of its own verified components) | C | arithmetic |
| 34 | CUT1 | Segment starts / resumes | 9 starts (idx 0,60,61,68,71,79,87,95,154); 11 resume events | identical | V | rerun |
| 35 | CUT1 | Position groups | pos0 8/9 · pos1 6/8 · pos≥2 2/155; Spearman 0.784 | identical (0.78405) | V | rerun |
| 36 | CUT1 | Anomaly pair | idx 124/125 @ 11:50:55; delta 10,482 s; gaps 704/0 | identical | V | rerun |
| 37 | CUT1 | PRED-C1 Brier | 0.3025 (FALSE) | (0.55−0)² = 0.3025 | V | arithmetic |
| 38 | candidate-set-v2 | **720 B label (calibration row)** | freed canvas block = 720 B size class | 720 B = the setLineDash Vector\<double\> buffer, 90 doubles × 8 B; freed slot 768 B (public repo) | C | heapprobe.html ll. 18, 78 |
| 39 | candidate-set-v2 | 59-set lap wall | 08:56:13 → 14:49:16 (5 h 53 m) | first serves 08:56:13; DONE embedded 14:49:16 | V | https.log + watchdog.log |
| 40 | candidate-set-v2 | Lap result beacons | 4, at idx 0, 1, 29, 30, all len=90/zeros | exactly 4 unique MAPPED events in the window, at those indices | V | https.log copy |
| 41 | candidate-set-v2 | Watchdog slice (Oct 22) | 57 stale · 58 dances · 58 app-exits · 51 second attempts | 57 (sweep-mode poking) · 58 · 58 · 51 in the slice ≤16:40 | V | watchdog.log copy |
| 42 | candidate-set-v2 | Set arithmetic | R1 30 + R2 10 + R5 16 + R4 2 = 58 | as printed | V | the document + candidate files |
| 43 | candidate-set-v2 | SWEEP-DONEs at writing | "294+" | 294 reached ~08:20 Oct 22 (prefix) | V | https.log cumulative |
| 44 | candidate-set-v2 | Desert unsampled | 0x1000–0x180000000 never sampled pre-v3 | candidate files + serve records agree (lowest band 0x100000000; control 0x1000) | V | candidates/ + https.log |
| 45 | EMISSIONS-ATLAS | Heartbeats | 995 | 995 | V | https.log copy |
| 46 | EMISSIONS-ATLAS | Runner starts | 712 | 712 | V | https.log copy |
| 47 | EMISSIONS-ATLAS | JACKPOT / JS-ERR | 0 / 0 | 0 / 0 | V | https.log copy |
| 48 | EMISSIONS-ATLAS | Canary FAIL lines | 580 | 580 lines (290 events × 2 representations) | V | https.log copy |
| 49 | EMISSIONS-ATLAS | Recovery ladder | 586 pokes → 320 dances → 169 app-exits → 60 second → 34 relaunches | reproduces jointly at a ~07:05–07:15 Oct 22 prefix (07:00 → 583/320/169/60/34; 07:30 → 592/320/169/60/34) | V | watchdog.log copy |
| 50 | EMISSIONS-ATLAS | Door map (top) | ps5.np 14,919 · epic 2,738 · manuals 960 · ps5cel 860 · uef 647 · feature 618 · gaikai 540 · vulcan 447 · telemetry 415 · upload ~121 · takedown 94 | prefix ≤~07:20 gives Δ≤8 on every host (minutes of live traffic); snapshot (08:49) preserves ranking: 15,092 · 2,830 · 994 · 884 · 664 · 636 · 541 · 447 · 488 · 121 · 103 | V | snapshot dns.log + live dns.log |
| 51 | EMISSIONS-ATLAS | Inter-start median | 373–374 s | median inter-serve gap = 374.0 s | V | https.log copy |
| 52 | EMISSIONS-ATLAS | 704 s stall | one 704 s stall before the second result batch | gap_prev = 704 s at serve idx 124 | V | keys_a6v2 / cut1 outputs |
| 53 | ELIMINATION-MAP | Spray flat (A-9) | flat across {75, 300, 600} | results at all sizes, no dose-response (75: 4/15 · 150: 7/133 · 300: 4/16 · 600: 1/8) | V | https.log via keys_a6v2 |
| 54 | ELIMINATION-MAP | KASLR channels (A-3) | 4/4 tested channels dead | his repo record (attributed primary source; not independently re-run) | V | second bench's PS5-14.10-Research |
| 55 | INTEGRITY-AND-GAPS | SWEEP-DONEs | 284 (280× n=62, 3× n=8, 1× n=1) | prefix reproduction at ~07:20 Oct 22 (307 total by the 08:48 snapshot) | V | https.log copy |
| 56 | INTEGRITY-AND-GAPS | Starts / aborted | 380 starts; 96 (25%) never completed | prefix ~07:20 (382 starts at 07:30); 96/380 = 25.3% | V | https.log copy |
| 57 | INTEGRITY-AND-GAPS | OFFSET_ in 14.10 table | 29 constants | 29 textual occurrences (25 scalar assignments, 26 named) | V | offsets-audit/14.10.js |
| 58 | INTEGRITY-AND-GAPS | Host-constructor candidates | 3 values | [0x56A58, 0x56CA0, 0x57CE8], file line 1 | V | the file |
| 59 | INTEGRITY-AND-GAPS | Canary starts | 116 each | **58 unique starts each** (116 log lines) | C | https.log copy |
| 60 | INTEGRITY-AND-GAPS | fuzzcases | 4,151 cases | **4,251 program .js** (+10 canary singles + manifest.json = 4,262 files) at the 08:48 snapshot | C | snapshot tarball |
| 61 | OFFSET-AUDIT-14.10 | Clone MD5 | e49b78d4… (13.60/14.00/14.10), 11,363 B | identical MD5s and size, both shelves + Bench H live | V | md5sum ×5 |
| 62 | OFFSET-AUDIT-14.10 | Constants per table | 23 | **25 scalar** (26 named, 29 occurrences) | C | the file + D1 regex |
| 63 | OFFSET-AUDIT-14.10 | Support list | 33 firmwares | **35 entries** (33 upstream + 14.00 + 14.10) | C | his firmware.js (snapshot) |
| 64 | OFFSET-AUDIT-14.10 | Slimming 12.70→13.00 | 41 → 25 constants | 41 → 25 named (40 → 24 scalar) | V | offsets-full shelf |
| 65 | OFFSET-AUDIT-14.10 | 13.42→13.60 transition | exactly 4 kernel constants shift, +0x10000…+0x24000 | 4 distinct kernel **addresses** shift (7 named constants; the 4 flag names alias one address, +0x13000; others +0x10000 / +0x24000) | V | offsets-full shelf |
| 66 | OFFSET-AUDIT-14.10 | wk_memset_import | 0x03350850 | exact, file line 3 | V | the file |
| 67 | KILLERS-TRIAGE | Starts, all cases | 8 recorded starts | **4** (1 per case) | C | https.log (full + snapshot) |
| 68 | KILLERS-TRIAGE | Completions | 0 | 0 | V | https.log |
| 69 | KILLERS-TRIAGE | Timer case | 2 START, 2 SKIP-CACHED, 0 DONE | 1 START, 1 SKIP-CACHED, 0 DONE | C | https.log |
| 70 | KILLERS-TRIAGE | Canvas case | 2 START, 0 iteration reports, 0 DONE | 1 START, 0 reports, 0 DONE | C | https.log |
| 71 | KILLERS-TRIAGE | Multicol case | 2 START, 0 DONE | 1 START, 0 DONE | C | https.log |
| 72 | KILLERS-TRIAGE | RAB case | 2 START, 2 RESIZED0, 0 COPIED, 0 DONE | 1 START, **1 RESIZED0 event** (2 log lines), 0 COPIED, 0 DONE | C | https.log |
| 73 | KILLERS-TRIAGE | Origin-bench reputations | timer 6/6 · multicol 3/3 deterministic | attributed claims; origin records not in evidence | U | — |
| 74 | TRIAL-REPORT | Task 1 | 200 · 4.15 s · answer 128 · PASS | trial log exact; 376/47×16 = 128 | V | trial-log-2026-10-22.jsonl |
| 75 | TRIAL-REPORT | Task 2 | 200 · 23.76 s · 1,139 chars | trial log exact | V | trial-log jsonl |
| 76 | TRIAL-ADDENDUM | Task 3 | 200 · 2.38 s · answer 126 · PASS | trial log exact; C(9,4) = 126 | V | trial-log jsonl |
| 77 | TRIAL-ADDENDUM | Task 4 | 200 · 16.54 s | trial log exact | V | trial-log jsonl |
| 78 | EXPANDED-MODEL-ROUTER | Seat VRAM | mathwhiz 2,002 MiB · draft 3,384 MiB | profiles.py vram_mib 2002 / 3384 (measured 2026-10-22) | V | deployed profiles.py (Bench M) |
| 79 | EXPANDED-MODEL-ROUTER | Profile totals | unlock-research 22,882 · triage 19,498 MiB | resident-seat sums reproduce exactly (3200+2664+6410+5222+2002+3384; minus draft for triage) | V | profiles.py |
| 80 | EXPANDED-MODEL-ROUTER | Proof arithmetic | 150·90·8 = 108,000 · 47·89 + 12345/15 = 5,006 | exact | V | arithmetic |
| 81 | EXPANDED-MODEL-ROUTER | Deep proof via Bench H | 200, ~63 s | trial log 62.98 s; router log 63.74 s | V | both jsonl logs |
| 82 | EXPANDED-MODEL-ROUTER | the large local engine-incident figures | the large engine 8,876 MiB · shepherd restarts 58 · final VRAM 22,565/24,564 | transient bench state; no surviving record | U | — |
| 83 | EXPANDED-MODEL-ROUTER | Embed proof | top score 0.7463 | transient response; not in the router log | U | — |
| 84 | ROUTE-GATES | job_router.py | rewritten 6,102 → 29,062 B | deployed 29,062 B; backup 6,102 B | V | Bench M model-router dir |
| 85 | ROUTE-GATES | Math gate catch | seat said 97,409,826; correct 97,406,826 | 123456×789+42 = 97,406,826 | V | arithmetic |
| 86 | ROUTE-GATES | Proof arithmetic | 12,017 · 46 · 42 · 40 km/h | all exact | V | arithmetic |
| 87 | ROUTE-GATES | Gate verdicts | PASS / FAIL / UNGATED as reported | router log carries gate_kind + gate_verdict for the proof calls, incl. the two clean 503 refusals | V | router-log jsonl |
| 88 | ROUTE-GATES | Scores / drift / jaccard | Skywork 4.9844 · 5.8008 · 0.8696 · 7.5859 · drift 0.0002 · jaccard pairs | response-level values; not recorded in any surviving log | U | — |
| 89 | MERGED-SET-v3 + LOAD-NOTE | v3 file | 32 values, MD5 27a96f03… | MD5 identical on 4 copies (workspace, shared workspace, Bench H loaded file, runcard) | V | md5sum ×4 |
| 90 | MERGED-SET-v3 | Pass cost | ~3.3 h/pass | 32 × 374 s median cadence ≈ 3.3 h | V | https.log + arithmetic |
| 91 | LOAD-NOTE-v3 | 59-set backup | previous set backed up before load | backups-20261022-load-v3/ holds heapcands.txt.59set + idx | V | Bench H listing |
| 92 | GENERATION-NOTES | Original candidate file | 62 lines, 61 unique, f00000000 ×2 | exact (workspace copy + Bench H .bak) | V | candidates/ + Bench H |
| 93 | GENERATION-NOTES | Bisection rule | ext = midpoints of adjacent pairs, ratio ≤16 | the rule regenerates exactly the 59 ext values | V | recompute |
| 94 | GENERATION-NOTES | Merged file | 120 unique | 120 lines, 120 unique = orig ∪ ext | V | candidates/ |
| 95 | GENERATION-NOTES | "550 passes" | 0 JACKPOTs in 550 passes | JACKPOT 0 verified; 550 is a DONE **line** count, not passes (548 lines / 274 events in window) | C | https.log (see #101) |
| 96 | COMPARISONS | Offset shelves | 35 tables; 33 upstream byte-identical | 35 files on both shelves, all MD5-identical | V | D1 audit + shelves |
| 97 | COMPARISONS | Door censuses | his 185 domains / 27,581 queries; ours 23; in-both 16, ours-only 6 | 185 unique verified; totals are prefix counts of the growing log (27,411 @ ≤07:15 → 27,967 @ 08:49); 16+6 = 22 named + "file" = the 23-name census | V | dns.log + gate journal |
| 98 | COMPARISONS | fus01 on his console | queried 17 times | 17 | V | dns.log |
| 99 | COMPARISONS | epic / ps5cel counts | 2,765 / 868 | prefix-consistent (2,732 @07:15 → 2,830 @08:49; 858 → 884) | V | dns.log |
| 100 | COMPARISONS | 11.60 cross-format | 37/37 symbols, 37/37 values agree | not re-derived (the shelf identity it supports is MD5-verified) | U | — |
| 101 | PATCH-NOTES | SWEEP-DONEs in window | 550 (2026-10-19 13:51 → 2026-10-22 06:50) | **548 lines = 274 unique DONE events** | C | https.log copy |
| 102 | PATCH-NOTES | Gap statistics | mean 219 s · deterministic 213 s (median = max over 230 cycles) · 33.4 h cumulative | not reproducible by any faithful reconstruction (DONE polls repeat ~140–210 s; SYNCFLUSH re-times beacons; original computation gone). Stale-at-poke values in window: mode 210, median 240. Whole-log START-gap median is 213.0 s — a real 213, but a different quantity than claimed | U | https.log + watchdog.log |
| 103 | PATCH-NOTES | Stale threshold | 180 s | THRESH=180 (idle) / 90 (sweep) in ps5_watchdog.orig | V | Bench H backups-20261022 |
| 104 | PATCH-NOTES | v2 fast path | ~45 s (25 s quiet + 20 s nap) | constants in the shipped ps5_watchdog_v2 | V | bundle file |
| 105 | COLLAB-PLAN | Fuzz instance | 14 jobs | jobs=14 in era_fuzz.log | V | Bench H fuzz logs |
| 106 | COLLAB-PLAN | Crashes banked | ~4,800 | no surviving source (anchors: 6,712 pulled programs Oct 22; 7,496 .js in storage_era/crashes Oct 23) | U | — |
| 107 | CHECKER-MAP | Fuzz instance / threads | 14-job · 32 threads (Bench M) | jobs=14 verified; 32 threads = i9-13900K spec | V | Bench H logs + hardware record |
| 108 | CHECKER-MAP | Crash corpus | 4,764 claims | no surviving source (see #106) | U | — |
| 109 | FIXES-2026-10-22 | stream.log rotation | 930 MB · 19.7M lines | 930,214,075 B uncompressed · 19,694,752 lines | V | Bench H stream.log.20261022-0857.bak.gz |
| 110 | FIXES-2026-10-22 | Stream-client.log | 23 MB | stream-client.log.gz uncompressed 23,239,035 B | V | Bench H |
| 111 | FIXES-2026-10-22 | Discovery / drop events | 129 / 46 | 82 new-host + 1 restart-detect + 46 no-longer-available = 129; drops = the 46 | V | Bench H .bak.gz |
| 112 | FIXES-2026-10-22 | First fast restart | 2026-10-22 08:56:10, DONE at 08:55:16 (54 s) | watchdog log line exact | V | watchdog.log copy |
| 113 | CROSSTEST-KILLERS | Premise | "8 starts, 0 completions" | **4 starts**, 0 completions (inherits #67) | C | https.log |
| 114 | RUNCARD-census-14.10 | 11.40 reference values | stack 20,450 · guard 268 MB–1 GB · JIT 0.82–0.85× · props basis | harness-report.log exact (760 props · 20,450 · 1540×810 · fingerprint 1854) | V | staging logs |
| 115 | TEST-CARDS | TLS suite counts | Guide 17 · telemetry 12 | atlas-tls.log holds a 17-suite Guide list (incl. 1301/1302/1303) and the exact 12-suite telemetry list | V | atlas-tls.log |
| 116 | KEY-SHAPING-ALGORITHMS | shaping.py self-tests | A1 0.000000 bits · A6 planted 0.44 bits p=0.001 · A8 0.000 ns / 0.382 sig · A9 9.97 bits · A14 α 2.019 · A12 WARNING/QUIET | ALL SELF-TESTS PASS; values identical (0.44004 · 0.382 · 9.9665 · 2.01889) | V | shaping.py rerun |
| 117 | KEY-SHAPING-ALGORITHMS | PRED-01 / PRED-02 | p=0.70 / p=0.20, registered 2026-10-22 21:35 | as printed; resolutions from the logs: PRED-01 FALSE (Pass F never completed), PRED-02 TRUE (desert result 20:28:19). No Brier is printed in this document | V | https.log + watchdog.log |
| 118 | OBSERVER-LENS / ASK | Census + set sizes | 23-host census · v2 = 58 values | rows 137 / 42 | V | gate journal / document |

### Set B — shared workspace-only documents (Bench M `~/llm/shared workspace/derived/`)

The remaining shared workspace documents are byte-identical to workspace copies (md5-checked: CUT1, KEY-SHAPE-v1, candidate-set-v2-draft, KEY-SHAPING-METHOD, KEY-SHAPING-ALGORITHMS, shaping.py, EMISSIONS-ATLAS-v1, ELIMINATION-MAP-v1, OBSERVER-LENS, COLLAB-PLAN, CHECKER-MAP, UPDATED-PLAN, JOINT-REVIEW, TRIAL-REPORT, TRIAL-ADDENDUM, ASK, REPLY, HAL-EXPANSION-PACKAGE, ROUTE-GATES, EXPANDED-MODEL-ROUTER-BUILD, MERGED-SET-v3-RUNCARD) and are audited once, in Set A.

| # | Document | Claim | Claimed | Re-derived | V | Primary source |
|---|---|---|---|---|---|---|
| 119 | census-14.10-2026-10-22 | 14.10 constants | 766 props · stack 20,451 · fingerprint 1858 · JIT speedup 0.92 (34/37 ms) · viewport 1540×810 · alloc climb to 512 MB · regex 39 ms · plugins 5 | C14P1/C14P2 beacons exact; both runs beaconed (props ×2, stack ×2) | V | https.log copy |
| 120 | census-14.10-2026-10-22 | 11.40 viewport (comparison) | 1560×880 | **1540×810** (harness-report.log, 19 reports) — identical to 14.10's | C | harness-report.log |
| 121 | D1-audit-2026-10-22 | Offset shelves | 35 + 35 tables; one clone group (e49b78d4…) | exact | V | both shelves + md5 |
| 122 | shortlist-001 | Triage header | 6,712 programs · 6,589 exact clusters · 330 families · 6,474 singleton clusters · largest exact cluster 3 · agreement 1.0 | triage.py rerun reproduces identically | V | triage.py + pulled corpus |
| 123 | trial-deep-001 / 002 | Deep answers on file | 001 response 1,139 chars; 002 saved | trial log response_chars 1139 (001) / 1758 (002; the file adds a header) | V | trial-log jsonl |

### Set C — staging documents (Bench M `~/llm/staging/`)

| # | Document | Claim | Claimed | Re-derived | V | Primary source |
|---|---|---|---|---|---|---|
| 124 | CAMPAIGN | 11.40 PUP | 1,336,954,880 B · SHA-256 c81ab203…072ed | size + full SHA-256 recomputed, match; MD5 91ba50717b… also recomputed | V | staged PUP |
| 125 | CAMPAIGN | Door census | 23 hostnames | 22 named hosts at census time (2026-10-22 00:57) + the literal "file" artifact; 5 further names first appear only later on Oct 22 | V | logs/dns-queries.log (gate journal) |
| 126 | CAMPAIGN | Inbound LAN services | exactly 2 (9295/tcp, 5353/udp) | 9295 SYNs present in atlas-capture.log; census record stands | V | atlas-capture.log |
| 127 | CAMPAIGN | Update-check window | fus01 queried 8× (7 in 1 s + 1 retry) | 8 query events, 22:57–22:58 EDT Oct 21 | V | dns-queries.log |
| 128 | CAMPAIGN | Store/test windows | ps5.np 235× · qgve 40× · STUN resolved 2×, zero packets | 232 in the strict window (235 within the photo-bounded window) · 40 exact · 2 lifetime, ARP chatter only | V | dns-queries.log |
| 129 | CAMPAIGN | Telemetry line-probe | 68 telemetry queries in the window | **35 query events** in 02:17–02:19 EDT Oct 22 (consistent with the ~5 s drip the same section reports) | C | dns-queries.log |
| 130 | CAMPAIGN | Telemetry stack | TLS 1.2 only · 12 suites as listed · UNKNOWN_CA, zero completions | the exact 12-suite list is in atlas-tls.log | V | atlas-tls.log |
| 131 | CAMPAIGN | Browser census (11.40) | 760 props · 1540×810 · fingerprint 1854 · stack 20,450 | harness-report.log exact (30 / 19 / 19 / 5 reports) | V | harness-report.log |
| 132 | CAMPAIGN | Console clock | ~21 min fast | console ts 05:47Z vs 01:26 EDT receipt ≈ +21 min | V | harness-report.log |
| 133 | CAMPAIGN | Manuals cert fingerprint | 89:48:8A:5A:…:8B:E6 | openssl recompute exact | V | config/tls/cert.pem |
| 134 | CAMPAIGN | DualSense dossier | 289-byte HID descriptor · BT [redacted] | descriptor .bin = 289 B; address in artifacts NOTES.md | V | artifacts/dualsense/ |
| 135 | SURVEY | Relapse allowlist | 34 versions total | **33** | C | staged tarball, src/firmware.js |
| 136 | SURVEY | Offsets shipped | 34 tables | **33** | C | staged tarball listing |
| 137 | SURVEY-2 | Relapse tables | 33 firmwares; 11.x = 11.00 / 11.20 / 11.60; no 11.40 | tarball: 33 tables, 33-version allowlist, no 11.40 | V | staged tarball |
| 138 | SURVEY-2 | Literature figures | fork counts ~495 · bounties $50,000 / $10,000 · tool ranges · ~50 min/run | cited-external as of the 2026-10-21 reads, sources named in the document; not re-derived (outside primary-source scope) | U | cited sources |
| 139 | MANIFEST | Artifact table (9 files) | sizes + SHA-256 as printed | all recomputed, all match | V | staged files |
| 140 | MANIFEST | Model + 3 PUPs | sizes + SHA-256 as printed | all recomputed, all match | V | staged files |
| 141 | MANIFEST | GGUF shelf sizes | 4 sizes as printed | all match (17,559,178,144 · 7,206,168,928 · 5,946,648,928 · 629,246,976) | V | staged files |
| 142 | MANIFEST | dnsmasq conf | 3,236 B | 3,236 B | V | staged file |
| 143 | MANIFEST | Step-6 total | 9,884,396,965 B across 14 files | the 12 pre-addendum table files sum to **9,884,383,728 B** (Δ13,237; the "14 files" composition is not recorded) | C | arithmetic on verified files |

### Set D — research-registry campaign entries

| # | Entry | Claim | Claimed | Re-derived | V | Primary source |
|---|---|---|---|---|---|---|
| 144 | T-RE-001 | Clone constants | 23/23 constants equal; MD5 e49b78d4… | MD5 equality verified (stronger than the count); the count is **25/25 scalar** (+ array) — inherits rows 61–63 | C | offsets shelves |
| 145 | T-RE-002 | Killers | 8 logged starts, 0 completions; RAB 2/2 | **4 starts**, 0 completions; RAB 1/1 — inherits rows 67–72 | C | https.log |
| 146 | T-RE-003 | Pass integrity | 280/284 DONEs; 96/380 (25%) aborted | rows 55–56 | V | https.log |
| 147 | Q-RE-001 | 14.10 constants + status | stack 20,450 · guard 268 MB–1 GB · "not yet run on either bench" | constants verified (rows 114/131); **status is stale** — the census ran 2026-10-22 (E-RE-003) | C | logs |
| 148 | E-RE-003 | Census values | 766 vs 760 props · 20,451 vs 20,450 stack · 512 MB alloc | verified (rows 119/131) | V | https.log + harness-report |
| 149 | E-RE-003 | DONE tax | 213 s → ~45 s per cycle | inherits row 102: ~45 s design-verified; 213 s unverified | U | — |

## Corrections — every wrong number, with blast radius

**C-1. Killers start counts (rows 67, 69–72, 113, 145).** Claimed: 2 starts per case, 8 total. True: **1 start per case, 4 total; 0 completions**; timer 1 SKIP-CACHED (not 2); RAB 1 RESIZED0 event (not 2). Cause: his https.log records every beacon twice (GET + BEACON lines); the triage counted both representations as events. *Blast radius:* KILLERS-TRIAGE, CROSSTEST-KILLERS-11.40, registry T-RE-002. The conclusion "all four killer cases reproduce on 14.10" **survives in kind** — every case started and none completed — but **weakens in strength**: one run per case, not two; the RAB death point (between RESIZED0 and COPIED) is precise at 1/1, not 2/2; and the document's argument that beacon loss is "the strained reading" rests on thinner evidence at n=1.

**C-2. Canary starts (row 59).** Claimed 116 starts per canary. True: **58 unique starts each** (116 log lines). Same double-representation cause. *Blast radius:* INTEGRITY-AND-GAPS only; the DASHFORGE integrity verdict does not rest on it.

**C-3. CUT1 recovery total (row 33).** Claimed 1,280 lines. True: **1,080** — the sum of the document's own components (261+262+556+1), each reproduced exactly by re-running its script. A digit transposition in the doc's total. *Blast radius:* none — the total only sizes an excluded event class; the window result (58.3% vs 1.35%, p=1.6×10⁻¹²) is untouched.

**C-4. The 720 B label (row 38, calibration).** Claimed (candidate-set-v2-DRAFT §1): the freed canvas block is a 720 B size class. True: **720 B is the setLineDash Vector\<double\> buffer (90 doubles)**; the freed context object's slot is **768 B** (public repo). His comments (heapprobe.html ll. 18–19, 78) keep the two straight — "same size class" — the compression into "the block is 720 B" was the assistant's. *Blast radius:* the candidate-set calibration row only; no design conclusion used 720 as the object's size, and the candidate sets themselves are untouched (rows 42, 92–94 verified exactly).

**C-5. fuzzcases count (row 60).** Claimed 4,151 cases. True: **4,251 program .js** (+10 canary singles + manifest.json = 4,262 files) in the 2026-10-22 08:48 snapshot. *Blast radius:* scene-setting in INTEGRITY-AND-GAPS; no conclusion rests on it.

**C-6. Offsets constant count (rows 62, 144).** Claimed 23 constants. True: **25 scalar-assignment constants** (26 named including the host-constructor candidates array; 29 textual occurrences — INTEGRITY's "29" is the occurrence count and is correct as such). *Blast radius:* OFFSET-AUDIT-14.10, registry T-RE-001. The conclusion survives intact — it rests on MD5 byte-identity, which is stronger than any count and is verified.

**C-7. Support-list size (row 63).** Claimed 33 firmwares. True: **35 entries** (33 upstream + 14.00 + 14.10) in his firmware.js. *Blast radius:* OFFSET-AUDIT-14.10. The point — 14.10 is admitted on a cloned table — survives, strengthened: the list is longer than claimed, not shorter.

**C-8. "550" SWEEP-DONEs / passes (rows 95, 101).** Claimed 550 (both as DONEs in a stated window and as "passes"). True: in PATCH-NOTES' own window (≤2026-10-22 06:50) there are **548 DONE log lines = 274 unique DONE events**; completed-pass groupings in the window number ≈272. *Blast radius:* PATCH-NOTES, GENERATION-NOTES ("0 JACKPOTs in 550 passes" — the JACKPOT count itself is verified 0; the denominator was lines, not passes). No conclusion changes: the desert/lottery arithmetic never used 550.

**C-9. Census viewport comparison (row 120).** Claimed 11.40 viewport 1560×880 (vs 14.10's 1540×810). True: **1540×810 on both** (harness-report.log). *Blast radius:* the census document's parenthetical gloss "chrome differs slightly" **does not survive** — it rested on this figure alone. The census verdict ("same browser on every measured constant") is *strengthened*.

**C-10. CAMPAIGN telemetry count (row 129).** Claimed 68 telemetry queries in the probe window. True: **35 query events** in 02:17–02:19 EDT 2026-10-22 per the surviving gate journal — consistent with the ~5 s drip the same paragraph reports (~36 expected in 3 minutes). *Blast radius:* the zero-completions finding is unaffected.

**C-11. SURVEY "34" (rows 135–136).** Claimed 34 allowlist versions / 34 offsets tables. True: **33 and 33** (counted in the staged tarball). *Blast radius:* cosmetic — aligns SURVEY with SURVEY-2, COMPARISONS and the D1 audit, which all say 33. The verdict (11.40 excluded) is unaffected.

**C-12. MANIFEST Step-6 total (row 143).** Claimed 9,884,396,965 B / 14 files. True: the 12 pre-addendum table files sum to **9,884,383,728 B** (Δ13,237); the claimed total's file composition was never recorded (it may have included the 3,236 B dnsmasq conf and ~10 KB of config/docs). *Blast radius:* none — the "~9.9 GB" summary holds, and every individual file's size and hash in the manifest is verified.

**C-13. KEY-SHAPE-v1 log description (row 23).** Claimed the https.log copy's "first line 2026-10-20T22:39:35." True: the file's literal first line is **2026-10-19T13:51:39** (a pre-campaign curl test fetch); 2026-10-20T22:39:35 is its first DASHFORGE beacon. *Blast radius:* none — the line count and every statistic are unaffected.

**C-14. Registry Q-RE-001 status (row 147).** The entry says the 14.10 census is "not yet run on either bench" while E-RE-003 in the same file records it done (2026-10-22) — the status text is stale; the entry's measured constants are verified. Corrected by the appended registry note, per the audit's no-rewrite rule.

## Unverifiable — what would be needed

**U-1. PATCH-NOTES gap statistics (rows 102, 149): mean 219 s; "deterministic 213 s" (median = max over 230 consecutive cycles); 33.4 h cumulative dead time.** No faithful reconstruction from the surviving logs reproduces them: the log's DONE polls repeat every ~140–210 s, SYNCFLUSH batching re-times beacon timestamps, and DONE→next-START gaps in the surviving log have median ≈0 (the page re-boots instantly after DONE — sequence verified in the log). Watchdog stale-at-poke values in the window give mode 210 / median 240, not 213. The whole-log START-to-START median *is* exactly 213.0 s — a real, reproducible 213, but a different quantity than the document claims. The mechanism constants verify in source (v1: THRESH=180 idle / 90 sweep, SLEEP=120/45; v2: 25 s quiet + 20 s nap ⇒ ~45 s by design). **Consequence: the claim "per-pass dead time drops 213 s → ~45 s, roughly doubling daily passes" (PATCH-NOTES, echoed in GENERATION-NOTES, FIXES, and registry E-RE-003) does not survive as a measured claim** — it stands only as a design expectation: the 45 s side is verified in the shipped file; the 213 s side is not a measurement the audit can stand behind. *Needed:* the original gap-computation script/output, or server-side per-pass serve records without DONE-poll duplication.

**U-2. "Crashes banked" 4,764 (CHECKER-MAP) / ~4,800 (COLLAB-PLAN) (rows 106, 108).** No surviving source reproduces either figure ('4764' occurs in his fuzz logs only inside floats/counters). Anchors: the pulled corpus is 6,712 programs (2026-10-22); his `storage_era/crashes/` holds 7,496 .js (2026-10-23). *Needed:* his crash-bridge counter record or a dated storage snapshot. D3's rationale is unaffected (the pile is bigger than claimed, not smaller).

**U-3. EXPANDED-MODEL-ROUTER transient bench state (row 82):** the large local engine holding 8,876 MiB; shepherd restart counter 58; final VRAM 22,565/24,564 MiB; "8192 ctx missed budget by 30 MiB." Journal and nvidia-smi state from build time has rotated past. The build's *proofs* (outcomes, latencies) are corroborated by the router and trial logs (rows 78–81, 87). *Needed:* the build-time journal / nvidia-smi capture.

**U-4. ROUTE-GATES response-level values (row 88):** Skywork scores 4.9844 / 5.8008 / 0.8696 / 7.5859; embed drift 0.0002; draft Jaccard/containment pairs. The router log records gate kinds and verdicts (all as reported) but no scores. *Needed:* the response bodies from the proof calls.

**U-5. Embed proof top score 0.7463 (row 83).** Transient response, not logged. *Needed:* the response body.

**U-6. COMPARISONS 11.60 cross-format agreement (row 100):** 37/37 symbols, 37/37 values. Not re-derived; the shelf-identity conclusion it supports is MD5-verified independently (rows 96/121). Minor and non-load-bearing. *Needed:* the two 11.60 source files in both formats.

**U-7. Killers' origin-bench reputations (row 73):** timer "6/6 deterministic," multicol "3/3" — attributed claims about the second bench's source corpus; his origin records are not in evidence. *Needed:* the origin-bench run records.

**U-8. EXPANDED-MODEL-ROUTER embed corpus ranking detail (row 83 companion)** and **U-9. SURVEY-2 literature figures (row 138)** — cited-external numbers (fork counts, bounties, tool version ranges, runtimes) as of the 2026-10-21 reads, with sources named in the document; by design outside this audit's primary-source scope. Its load-bearing claim (33 Relapse firmwares, no 11.40) **is** verified (row 137).

## Checked and absent — figures that exist only in chat/memory, in no scoped document

These were checked because they circulate in the campaign record; no in-place correction is possible because no audited document carries them:

- **PRED-01 Brier "0.09"** — arithmetically wrong: (0.70−0)² = **0.49**. KEY-SHAPING-ALGORITHMS prints no Brier for PRED-01/02 (row 117).
- **CAMPAIGN.md "25,310 B"** — the file is 27,537 B (md5 268c1857…).
- **Corpus pull "13,425 files / 61 MB"** — appears in no scoped document. Anchors: the crashes directory alone is 6,712 .js / 61 MB; the later shared workspace sync manifest carries 13,463 Bench H-prefixed lines of 13,529 total.
- **A10 DNS census counts 503 / 509 / 719** — 503 (upload.crs) and 509 (cfss.crs) verify exactly against the live dns.log at the stated window (≤2026-10-22 21:41); the crepo figure at that window is **929**, not 719.
- **FIXES "only ONE more fast-restart (14:51:16)"** — not in the FIXES document (which verified as written); the watchdog log in fact holds 91 pass-done/fast-restart lines on Oct 22.
- **Supervision restart counters 3,143 / 15,789 / 8,051** — in no scoped document; live NRestarts reads 0 after the disables, so they are unverifiable after the fact.

## In-place corrections applied (dated footnotes appended; original text never rewritten)

- `~/workspace/campaign-docs/`: CUT1-BOUNDARY-PERSISTENCE-2026-10-23.md (C-3) · KEY-SHAPE-v1-2026-10-23.md (C-13) · candidate-set-v2-DRAFT.md (C-4) · KILLERS-TRIAGE.md (C-1) · INTEGRITY-AND-GAPS.md (C-2, C-5) · OFFSET-AUDIT-14.10.md (C-6, C-7) · CROSSTEST-KILLERS-11.40.md (C-1) · PATCH-NOTES.md (C-8 + U-1 note) · GENERATION-NOTES.md (C-8 + U-1 note) · FIXES-2026-10-22.md (U-1 note; all else verified).
- Bench M shared workspace `derived/`: CUT1 (C-3) · KEY-SHAPE-v1 (C-13) · candidate-set-v2-draft (C-4) · census-14.10-2026-10-22 (C-9).
- The second bench's exports bundle (Bench M `~/llm/staging/exports/bundle-2026-10-22/`): KILLERS-TRIAGE (C-1) · INTEGRITY-AND-GAPS (C-2, C-5) · OFFSET-AUDIT-14.10 (C-6, C-7) · CENSUS-RESULTS-14.10 (C-9) · PATCH-NOTES-watchdog (C-8, U-1) · GENERATION-NOTES-candidates (C-8, U-1) · FIXES-2026-10-22 (U-1).
- The second bench's handoff (Bench H `~/bench-h/ai-handoff/`): CUT1 (C-3) · KEY-SHAPE-v1 (C-13).
- staging (Bench M): SURVEY.md (C-11) · MANIFEST.md (C-12) · CAMPAIGN.md (C-10 + verified list).
- `~/workspace/research-registry.md`: one appended "Corrections — Numbers Audit (2026-10-23)" section covering T-RE-001, T-RE-002, Q-RE-001, E-RE-003.
- Every append was verified present (exactly one audit note per target file).

## Working notes

Primary sources used, all surviving at audit time: Bench M `/tmp/https.log` (21,089 lines, 2026-10-19T13:51:39 → 2026-10-23T06:08:29) and `/tmp/watchdog.log` (1,990 lines) — copies of the second bench's harness logs; the harness snapshot `~/llm/staging/from-bench-h/snapshot-harness-20261022.tar.gz` (logs as of 2026-10-22 08:48–49, fuzzcases/, killers/, src/firmware.js); offsets shelves `~/llm/staging/from-bench-h/offsets-audit/` and `offsets-full/` (35 files each); the pulled corpus `~/llm/shared workspace/Bench H/fuzz/crashes` (6,712 .js) with `tools/triage.py`; shared workspace records (trial-log, router-log, triage-2026-10-22.json, D1-audit, MANIFEST.sha256 — 13,529 lines); staging logs (dns-queries.log, harness-report.log, atlas-tls.log, atlas-capture.log, door-census-tls-evidence.log); on Bench H: the live harness (heapcands.txt, heapprobe.html, dns.log continuous 2026-10-19 → 2026-10-23), `~/bench-h/backups-20261022/` (ps5_watchdog.orig, load-v3 backups), `~/bench-h/wkdrop/WebKit-1200.zip` + `WebKit-1400.zip`, `~/bench-h/fuzz/storage_era/crashes/`, stream-client `.bak.gz` archives. The original analysis scripts (`/tmp/keys1.py`, `/tmp/keys_a6v2.py`, `/tmp/cut1_run.py` on Bench M; `shaping.py`; `triage.py`) were re-run unmodified — their outputs are the strongest verifications in this audit. Audit recomputation scripts were kept in the audit's working notes (`/tmp/audit/` on the audit VM).
