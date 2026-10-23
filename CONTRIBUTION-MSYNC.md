# msync(65) / CVE-2026-49418 on 14.10 — the trigger has been run, and it is refused

*Contribution note — for the Priority Vector #1 entry (msync device-pager
UAF). The "58a written, ready to run" status on master is stale: 58a and
its follow-ups were run on 2026-10-21/22, with the corrected syscall
number, and the CVE's first gate does not open. Closing this door with
the data so nobody else spends console time on it.*

## The correction lineage (where the confusion came from)

- The earliest probes (30 / 38 / 42b, and the first 58a draft) called
  syscall **226** for "msync". 226 is a nosys stub — those runs measured
  nothing about msync, and the Phase 8/9 changelog claims from that era
  ("msync confirmed instant-kill") are void. My side's record included.
- **PR #70** (commit `bcce72a`, merged 2026-10-21) fixed the number:
  226 → **65**, kernel-dump verified. Everything below uses 65.
- Separately: the "mincore/msync/madvise oracle — Lethal" KASLR-table
  entry is a different use of the name (an errno oracle, probe 56k,
  whose msync arm called 227 with MS_ASYNC against kernel VAs). It is
  not evidence about the CVE trigger in either direction.

## What was run (fw 14.10, Lua game process, syscall 65)

Probe series **58a / 58b / 58e / 58f** and **121e–h / 124a**, all
post-correction. The flag sweep on each mapping ran MS_SYNC (0),
MS_ASYNC (1), and MS_INVALIDATE (2) on the *same* mapping in the *same*
run:

- **MS_SYNC and MS_ASYNC return 0** on these mappings — the syscall
  reaches the kernel and the mappings are valid (positive controls).
- **MS_INVALIDATE returns −1 on every recorded call: ≥11 calls across
  ≥7 runs, 0 successes**, on five mapping classes:
  - GPU-anonymous mmap
  - regular anonymous mmap
  - private anonymous mmap
  - `/dev/dmem0` MAP_SHARED
  - `/dev/gc`
- After every INVALIDATE call the pages were unchanged — contents
  intact, no fault, no disappearance. The invalidation the CVE's
  sequence starts with **never happened**, so the double-insertion /
  double-free chain cannot start.

Gate-closed commits recording exactly this: `824e5ee` (2026-10-21),
`c6c80a9` and `f36bb46` (2026-10-22). They live in a checkout ahead of
public master, which is why master still shows the pre-run entry.

One caution for anyone re-reading the raw captures: probe 124a's own
printout labelled its −1 result "CVE gate: OPEN" (it treated
"returned, process alive" as openness). That reading was corrected by
the commits that recorded the same result: **−1 is the kernel refusing
the call.** The gate is the INVALIDATE flag specifically — which is
also why the priority entry's test as worded ("if msync returns 0 on
GPU-mmap pages, the path is reachable") is too loose: msync *did*
return 0, for SYNC/ASYNC. Only INVALIDATE decides it, and INVALIDATE
fails.

## Scope — what this does and does not claim

- **Claimed:** the CVE-2026-49418 trigger (msync(65, MS_INVALIDATE) on
  a device mapping, from the game process) is refused on 14.10 across
  every mapping class we could reach. Why it returns −1 (EINVAL-class
  rejection vs wired pages) was not errno-decoded; the uniform,
  flag-specific pattern points at MS_INVALIDATE handling itself,
  upstream of any pager-list code.
- **Not claimed:** anything downstream of a *successful* invalidate —
  never observed, so neither confirmed nor denied. (The advisory
  itself caps the primitive to a never-recycled fictitious-page pool;
  there is no public PoC.)
- **The one residual:** a device mapping class that is provably an
  *unmanaged* device-pager object, not yet mmap-able from the game
  process, could in principle behave differently. That substrate has
  never been observed; it is a hypothetical, not a route. Testing it
  means finding a *new* substrate first (an mmap on an openable
  `/dev` fd other than dmem0/gc, with evidence it is an unmanaged
  device pager) — re-running 58a/58b on the same mappings will only
  reproduce −1.
- **14.10 only.** Nothing here transfers to other firmware.

Suggested master updates: Priority Vector #1 → closed at trigger
(evidence above); Phase 8/9 "instant-kill" changelog lines → void
(226 era); KASLR-table oracle entry → annotate as an oracle use,
wrong-number arm, not msync-trigger evidence.

— cobrajet (runs from my fork-side checkout, 2026-10-21/22; happy to
merge the gate-closed commits up or re-run any single call on request)

---

## Correction — 2026-10-23 (community-digest provenance correction)

Appended, dated, not a rewrite — the text above is unchanged.
This note corrects the provenance framing in
PROCESSING-REPORT-2026-10-23.md §1 and §3 and in
CONTRIBUTION-MSYNC.md. Per COMMUNITY-DIGEST-2026-10-23.md:
the gate-closed msync(65) probe runs (58a/58b/58e/58f,
121e–h/124a) ARE present in ZigZagBoi1 public master at
37d05339 — the result files are in the public tree at that
HEAD. What lags is upstream's docs (README Priority 1,
docs/CVE-2026-49418-PS5-14.10.md, docs/STRATEGY.md
Priority 1), which still call 58a written-and-ready-to-run /
unrun. Earlier wording here — that the corrected runs "are
simply not in public master yet" (PROCESSING-REPORT §1),
that they "live in a checkout ahead of public master, which
is why master still shows the pre-run entry"
(CONTRIBUTION-MSYNC), and that we hold a "finished, citable
community contribution" in the data itself
(PROCESSING-REPORT §3) — is therefore corrected: the data
is already public; the upstream contribution narrows to a
docs/PR cleanup (README, CVE doc, STRATEGY priorities).
The elimination itself is unchanged: msync(65)
MS_INVALIDATE returns −1 on five mapping classes, with
MS_SYNC/MS_ASYNC at 0 as controls.
