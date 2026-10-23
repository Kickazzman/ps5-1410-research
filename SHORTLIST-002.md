# SHORTLIST-002 — D3 second layer: model-based re-scoring of crash-corpus families

> **WRAPPED column (two-column rule).** Every mechanism label, interest score and rationale in this shortlist was produced through a gated local multi-model **router/system path** (claim-check gate for 12 families, verified gate for 98; per-family provenance recorded with the scores). These are **WRAPPED** results — gated router/system outputs, **not raw model capability**. Deterministic facts (family size, TERMSIG, assertion source) are layer-1 / evidence facts.

Coverage: **110/330 families scored by the router** — all 51 families of size ≥ 2, all 14 remaining assertion-bearing singletons, and a deterministic tail sample of 45 further singletons (every 6th of the remaining 265 in layer-1 rank order) = 110 families covering 6492/6,712 programs (96.7%). The other 220 singleton families (220 programs) are listed in the JSON as `unscored_out_of_scope` under this stated rule.
Reconciliation vs layer 1: **MATCH** — 6,712 programs re-derived, 330 structural families, family sizes sum to 6,712, top-15 families identical to `triage-2026-10-22.json` (size, representative, bytes, signature preview).

Artifact bucket: **F001 (5,758 programs)** — signature is only the token `build`, leaked from the `/.build/` path in every file's CRASH INFO header, not program code. Scored by the router (interest 2, label “Yarr engine crash”) and kept in the accounting, but excluded from the interest ranking below. Meaningful families: the other 329 (954 programs), topped at 389/40/36/23/19.

Router reliability note: plain `lookup` seat calls intermittently returned empty text (Qwen3 reasoning-budget exhaustion on evidence-heavy prompts — a known reasoning-budget failure mode of the lookup seat); batch-of-10 returned empty and batch-of-5/3 lookup calls parsed only about half the time. The `verify` route's gated retry path parsed 32/32 batches fully, so the bulk of scoring used it. All scores remain WRAPPED router outputs.

## Top interest families (router interest desc, then family size desc)

| # | family | size | TERMSIG | tier | mechanism label (WRAPPED) | interest | surface | why — router rationale (WRAPPED) | deterministic facts |
|---|---|---|---|---|---|---|---|---|---|
| 1 | F002 | 389 | 6 | A | Yarr set operation assertion | 3 | Yarr | Assertion in Yarr set operation | assertion in YarrPattern.cpp; rep `program_20261021053258_198660FE-2DC5-482B-BFFF-373CC299F419_deterministic.js` (1118 chars, deterministic) |
| 2 | F005 | 23 | 11 | A | Yarr set-operation assertion | 3 | Yarr | Assertion in YarrPattern combiningSetOp on class set operation | rep `program_20261021001834_C4718E27-B30D-4A17-806B-3689D1F45AB5_flaky.js` (14595 chars, flaky) |
| 3 | F007 | 9 | 6 | A | regex non-ASCII character | 3 | Yarr | regex pattern non-ASCII character | rep `duplicates/program_20261022023752_85381085-79EE-4A4E-85BA-E1728C587CA4_deterministic.js` (840 chars, deterministic) |
| 4 | F012 | 8 | 11 | A | Yarr control character crash | 3 | Yarr | Memory access violation in Yarr regex engine | rep `program_20261021010821_BA8154DA-FE1A-4CBB-9629-D3ED18C4D280_flaky.js` (14735 chars, flaky) |
| 5 | F017 | 5 | 6 | A | engine assertion failure | 3 | Yarr | engine assertion from regex pattern | rep `duplicates/program_20261021164932_6B57A8AD-7EF0-4CF8-9758-48C55EE8E9D2_deterministic.js` (910 chars, deterministic) |
| 6 | F023 | 3 | 6 | A | Yarr assertion failure | 3 | Yarr | Regex pattern causes assertion | assertion in YarrPattern.cpp; rep `program_20261022052551_734231BD-AC69-4474-BD1A-BD8CF9114DDF_deterministic.js` (1158 chars, deterministic) |
| 7 | F024 | 3 | 6 | A | Yarr assertion failure | 3 | Yarr | Regex pattern causes assertion | assertion in YarrPattern.cpp; rep `duplicates/program_20261022004226_90E3B65C-DBE4-4022-A06C-054BF40D1390_deterministic.js` (1368 chars, deterministic) |
| 8 | F034 | 2 | 6 | A | unicode property in regex | 3 | Yarr | Unicode property in regex pattern | assertion in YarrPattern.cpp; rep `duplicates/program_20261022013755_9493C82D-DAE2-45AC-89FE-3A43D96CFA39_deterministic.js` (1348 chars, deterministic) |
| 9 | F089 | 1 | 6 | B | Yarr regex build assertion | 3 | Yarr | Assertion in Yarr regex build | assertion in YarrPattern.cpp; rep `duplicates/program_20261021192457_0BDF5823-442F-4765-B7DC-67F39B3D5505_deterministic.js` (1186 chars, deterministic) |
| 10 | F098 | 1 | 6 | B | Yarr regex build assertion | 3 | Yarr | Assertion in Yarr regex build | assertion in YarrPattern.cpp; rep `duplicates/program_20261021130910_A242FDDE-6EDF-4083-811B-450160B723D8_deterministic.js` (1246 chars, deterministic) |
| 11 | F141 | 1 | 6 | B | Yarr character class set assertion | 3 | Yarr | Yarr character class set assertion failure | assertion in YarrPattern.cpp; rep `program_20261021000749_05051B59-F33F-49A8-938E-E7FF98B0024D_flaky.js` (1503 chars, flaky) |
| 12 | F152 | 1 | 6 | B | regex engine assertion | 3 | Yarr | Property assignment triggers regex engine assertion | assertion in YarrPattern.cpp; rep `program_20261021090017_0D538B2F-1194-47C7-9AAD-A34DE7850AA3_deterministic.js` (1633 chars, deterministic) |
| 13 | F200 | 1 | 11 | C | Intl Collator compare crash | 3 | other | Collator compare with WeakMap | rep `program_20261021132114_C55F75B2-2C0F-414A-8F06-46FEF93BA0AB_flaky.js` (2488 chars, flaky) |
| 14 | F234 | 1 | 6 | B | Yarr assertion failure in character class | 3 | Yarr | Assertion failure in character class set | assertion in YarrPattern.cpp; rep `program_20261020165820_F4E71C40-ABE3-4026-A395-86C48C8F6087_flaky.js` (14951 chars, flaky) |
| 15 | F238 | 1 | 6 | B | Yarr assertion failure in character class | 3 | Yarr | Assertion failure in character class set | assertion in YarrPattern.cpp; rep `program_20261020191745_F74AC22E-2063-4156-89A1-812D38F12C59_flaky.js` (15121 chars, flaky) |

Interest scale (as given to the router): 3 = assertion inside engine internals or novel memory-unsafe path; 2 = deterministic segfault on a small/minimal trigger; 1 = segfault only in a large/flaky mutated program or heterogeneous grouping; 0 = boilerplate artifact.

Interest distribution over the 110 scored families: 1 → 62, 2 → 25, 3 → 23. Surface distribution: Yarr → 68, other → 42. Gate verdicts: PASS → 109, FAIL → 1.

Full per-family scores, gate verdicts and provenance: `triage-layer2-2026-10-23.json` (all 330 families accounted for; the full per-family JSON is retained in the authors' campaign record).
