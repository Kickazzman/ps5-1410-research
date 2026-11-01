# Neighbor audit — the 14.10 offset table (from perg's bench, 2026-10-22)

Method: the eight tables 12.70 → 14.10 pulled byte-exact from `exploit/offsets/` and compared constant-by-constant (23 constants per table in the current format). This is the stability-map method from perg's own 11.40 campaign: a constant that moves between every real neighbor pair and then stops moving hasn't been verified — it has been *carried*.

## Headline finding

**`14.10.js` is byte-for-byte identical to `13.60.js` — and to `14.00.js`.** Same MD5 (`e49b78d4…`), same 11,363 bytes, all 23 of 23 constants equal. The file under the 14.10 name contains **zero 14.10-derived values**. Whatever its author's intent — an assumption that the builds carry, or a placeholder awaiting derivation — every constant in it is unverified for 14.10.

## The shelf's derivation history, as the values tell it

| Transition | Constants changed | Which |
|---|---|---|
| 12.70 → 13.00 | format slimmed 41 → 25 | libc (`lc_`) family and KASLR-leak constants dropped — a chain redesign |
| 13.00 → 13.20 → 13.40 → 13.42 | 0 | frozen |
| 13.42 → 13.60 | **4** | exactly the kernel quarter: `OFFSET_KERNEL_ALLPROC`, `OFFSET_KERNEL_DATA`, `OFFSET_KERNEL_ROOTVNODE`, `OFFSET_KERNEL_SECURITY_FLAGS` (each shifted by +0x10000…+0x24000) |
| 13.60 → 14.00 → 14.10 | **0** — the files are clones | — |

So the only re-derivation anyone ever did on this shelf was the kernel half, once, for 13.60. The WebKit/libkernel 19 have been frozen since 13.20.

## What this means for 14.10, graded

- **The 4 kernel constants are presumptively wrong for 14.10** — not merely unverified. They changed at the one measured transition (13.42 → 13.60); kernel data placement moves per build. A 14.10 kernel stage reading `KERNEL_DATA` at its 13.60 address is reading the wrong structure.
- **The 19 wk_/lk_ constants are unverified.** They include raw binary-layout addresses (e.g. `OFFSET_wk_memset_import 0x03350850`) that move when the WebKit binary changes — and 14.10's WebKit is not 13.20's WebKit. They may partly hold (some libkernel entries are stable across long spans); none has been checked against 14.10 by anyone, as far as these files show.
- **The three host-constructor candidates** (`0x56A58, 0x56CA0, 0x57CE8`) are likewise the 13.00-era trio, carried unchanged through every table since. The entry uncertainty isn't a 14.10 measurement — it's inherited.

## The honest alternative reading

Sony may have shipped near-identical WebKit builds across some of these versions; point releases do sometimes carry a binary unchanged. Against that: three *different* firmware releases sharing every raw import address to the byte, files cloned at kit-assembly time (identical timestamps), and a campaign on the bench that behaves as if the entry doesn't work — fuzzing primitives and grooming heap — rather than as if a known-good chain merely needs reliability. The discriminator is empirical and already running: the canary suite. Every canary verdict is a per-bug ground-truth probe of 14.10's actual WebKit; the table has had no equivalent check.

## Recommendation

Treat `14.10.js` as a *hypothesis file*: 23 claims, 4 presumptively false, 19 untested. The cheapest verification order follows the crash cost — the chain dies at the first wrong constant it touches, so stage-by-stage single-constant probes (entry constructor first, since three candidates already enumerate that search) convert the table from folklore into measurements at the price of crashes the loop already pays. DASHFORGE and the canaries are the right instruments; they were never the side project — they are the only source of 14.10 truth on the bench.

---
**Correction (Numbers Audit, 2026-10-23):** (1) The 14.10 table's constant count is **25 scalar-assignment constants** (26 named constants including the `OFFSET_wk_host_constructor_candidates` array; 29 textual `OFFSET_` occurrences) — not 23. The equality result is unaffected: the file is byte-identical to 13.60.js (MD5 e49b78d4…), so every constant is equal by construction. (2) The host's support list (`firmware.js`) holds **35 entries** — the 33 upstream firmwares plus 14.00 and 14.10 — not 33 in total. See NUMBERS-AUDIT-2026-10-23.md.
