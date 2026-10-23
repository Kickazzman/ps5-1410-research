# Stage 1 reconciliation — CVE-2026-43720, the 720/768 question, and a boundary-persistence finding

**Prepared 2026-10-23 by a two-bench independent PS5 14.10 research program, for the community working on this bug. Not yet posted anywhere by the authors as of preparation.**

## The same bug

The public repository [pastawithpesto/PS5-14.10-Jailbreak-Research](https://github.com/pastawithpesto/PS5-14.10-Jailbreak-Research) identifies its Stage 1 as **CVE-2026-43720**, a Canvas Context Lifecycle bug in `HTMLCanvasElement::getContext()`: a reentrant path (via `bitmaprenderer` → property getter → `2d`) frees the inner `CanvasRenderingContext2D`, and the freed slot can be reclaimed. Their method replaces guessing with structure: a same-size ArrayBuffer spray reclaims the slot, and the aliased context then supports bidirectional read/write through legitimate Canvas2D APIs. They report a full 12-API capability pass confirmed on device, with the context's `State` struct mapped (`sizeof(State) = 400`; `lineWidth` at +48, `miterLimit` at +64, `m_stateStack` at +112, the `lineDash` Vector at +168).

Independently, and over the same days, the second of our two benches was running an unattended harness (we call it **DASHFORGE**) against **the same freed `CanvasRenderingContext2D` object** on PS5 firmware 14.10 — but by address lottery: each candidate was a byte-exact guessed address for the freed block, the page forged a context whose dash-vector pointer carried the guess, and a result beacon (or a page crash) was the verdict. Four days of unattended running produced, across the analyzed series of 172 attempts, **zero** byte-exact hits — and every result beacon ever recorded was stereotyped (a 90-element read, all zeros: the spray array reading itself; the forged chain never engaged). The lottery was groping for what the repository's slot-reclaim achieves directly. We say so plainly because the community is better served by one directed method than by two groups quietly duplicating the blind one.

## The 720 vs 768 discrepancy — resolved, and the error was ours

Our program's documents described the freed block as **720 B**. The repository gives the freed slot as **768 B**. Both numbers are exact — for two different allocations:

- **720 B** is the size of the reclaim spray's `setLineDash` buffer: a `Vector<double>` of **90 doubles × 8 B**, exactly as annotated in the harness's own probe source ("90 doubles = 720B fastMalloc alloc: reclaim shot"). It is also the 90 in every result beacon's read length.
- **768 B** is the freed `CanvasRenderingContext2D` object's own slot size, per the repository.

The mislabel happened in our summarizing, not in the harness's measurement: the spray buffer's size got attached to the freed object in our candidate-set document, and repeated from there. Our numbers audit (included in this package) caught it by going back to the probe source rather than to our own summary. We publish the correction with the finding because the two numbers will meet again in anyone's notes who reads both programs' records.

## What we can offer: boundary persistence in trigger survival

Re-deriving the harness logs deterministically (the analysis we call CUT1) produced one result we believe is useful to anyone running this bug — or any fragile WebKit trigger — on device:

**Result beacons concentrate immediately after console state changes.** Defining a state change as a fresh webview boot, a pass/segment start, or a resume after a stall:

- Attempts within **60 s** after a state change produced result beacons at **58.3% (14/24)**.
- Attempts later than that produced them at **1.35% (2/148)**.
- Fisher exact p ≈ **1.6×10⁻¹²**; binned time-since-state-change mutual information **0.227 bits** (1,000-shuffle permutation test, p = 0.001).
- The effect does not decay gradually: every populated bin from 181 s to 1800 s after a state change is **0/47**. The exact edge inside (60, 181] s is unresolvable at this harness's cadence — no attempts land there.

**Caveats, stated in full, because they bound what this means:**

1. The measured outcome is *beacon production* — the page surviving long enough to report — not exploit success. Every result in the series carried the spray-self-read signature described above.
2. Time-since-state-change and *position within a pass* are strongly confounded in this data (Spearman ρ = 0.78): every in-window success is simultaneously one of the first two attempts after a state change. The two cannot be separated post hoc. The instrument that can separate them is a paired design — the same candidate set served fresh vs. after a long settled stall, with attempts deliberately scheduled into the 61–180 s gap and interleaved-probe activity logged as first-class state changes.
3. Our first-pass analysis overstated the contrast's denominator (its "mid-run" base rate was contaminated by segment-start successes). The corrected figures above are the ones that survived re-derivation; the audit in this package shows the working.

Read conservatively, the finding is about **heap weather**: a fragile page's survival-to-report is concentrated at state boundaries, and a trigger that looks flaky mid-run may be weather-bound rather than bug-bound. If you are scheduling attempts against this bug, the first minute after a state change is worth roughly forty mid-run minutes — provisionally, and pending the paired test.

## The harness-mortality lesson

Our program registers forecasts before runs and scores them after. The forecast for the merged candidate pass — completion by a stated hour, at p = 0.70 — resolved **FALSE** (Brier 0.49). The console was not the cause: the harness's supervisor process died three times in one night with nothing supervising it, and the lap's bookkeeping (an index file) silently re-based across restarts while the beacons proved more serves than the index admitted.

Three rules we now run by, offered in the same spirit:

- **Forecasts must carry a harness-mortality term.** Measure your supervisor's death rate the way you measure the console's pace; a completion estimate without it is fiction.
- **Score coverage from beacons, not from harness state.** The device's own emissions are the ground truth; the harness's index is a claim about them.
- **A watchdog without a supervisor is a single point of silence.** Whatever watches the console needs something watching it.

## Credit

- Stage identification, the directed slot-reclaim method, and the `State` layout: **pastawithpesto/PS5-14.10-Jailbreak-Research**, and the researchers it builds on.
- The four-day unattended 14.10 harness run, the probe lineage, and the logs re-derived here: the second bench's operator and their tooling.
- The numbers audit and the boundary-persistence analysis: this program.

Nothing in this note is a jailbreak, a kernel stage, or a claim past Stage 1. On 14.10 the kernel rung remains exactly where it was; what changed is that the userland bug now has a directed method and a public name, and our lottery records reconcile with it.
