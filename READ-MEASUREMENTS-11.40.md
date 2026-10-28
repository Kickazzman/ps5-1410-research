# Read measurements on 11.40 (follow-up to #41 and #43)

## What this is

A follow-up to the device confirmations already posted in #41 (C-18/C-19)
and #43 (C-20 and the C-21 cluster). Those posts established that the
bugs exist on 11.40. This post is about something the community has
not had in the browser line so far: measured reads from inside the
webview — what the heap geography actually looks like along a read
ray, and what a before/after pair can and cannot measure.

All readings below were pre-registered in writing before each run.
Where a result is a lead, a partial answer, or unmeasured, it is
labelled as such. Nothing here claims kernel access, a write, or a
payload. This is measurement only.

The read instrument is the C-18 silent over-read already reported
in #41, used as a forward ray: a 510-byte strip sampled at a known
past-EOF displacement, repeated across displacements and across
sessions. No pointer values are reported anywhere below.

## 1. A sub-millisecond clock inside the webview (C-22)

- A dedicated Worker constructed from a Blob URL runs in the
  webview; SharedWorker also constructs without throwing.
- The main thread's performance.now clock is clamped at exactly
  1.0 ms.
- A counting worker delivered 841,466 counts per second — about
  1.2 microseconds per count, roughly 840x finer than the clamp,
  over 60 windows.
- Fence: this is a relative clock, calibrated against the clamped
  windows. Window-to-window variance was not captured.

## 2. The C-20 splice, mapped read-only

First map (v1): childNodes of both roots list the spliced element
simultaneously, read directly. parentNode reports body only, and
getElementById returns the same node, agreeing with body. The
sequence then ends at the serializer step on every load.

Second map (v2, 16 loads): none of the scheduled probes fired.
The first probe was scheduled 700 ms after the splice existed, so
the measurement is a survival bound: after the splice exists, the
process has less than 700 ms to live (16/16).

Third map (v3, synchronous sprint, serializer last): the readable
half completed.
- MATCHES: self = true, bodyChild = true, htmlChild = false —
  selectors follow parentNode, exactly as predicted.
- TreeWalker: the target was visited 22 times at a 48-step cap —
  document-order traversal through the splice is a cycle, not a
  double visit. Uncapped traversals do not terminate.
- Unmeasured, not negative: QSA counts, range extractions, and
  serializer behaviour in this sprint.

## 3. Heap geography along one ray (ruler v1)

One load, four strips, 510 bytes each. Nonzero bytes by
past-EOF displacement:
- 0: 31/510, sparse, including pointer-shaped values of one shape.
- 1528: 92/510, a repeated 8-byte structure, unidentified.
- 7648: 162/510, repeated structured data.
- 32128: 245/510, with content identified in clear ASCII:
  WebCore CSS atom strings ("-webkit-media-slider-container",
  "-webkit-slider-runnable-track") — the first content-identified
  heap read of this work. The ~32 KB window sits in the engine's
  string region.

Geography along the ray is non-uniform: zeros, then sparse
pointers, then arrays, then a string table. No strong landmarks
were found in this run, and no inter-allocation distance was
measured yet at this stage.

## 4. Stability split (survey v2)

One fresh load, 24 grooms parked.
- Near field is a fixture: the P170 strip is 491/510 bytes
  identical to run 1, with the pointer-shaped family recurring at
  the same strip offsets (6/14/22/46) with relocated values.
  Stable fields; targets move.
- Far field is session-dependent: the P10880 strip is only
  105/510 bytes identical to run 1. The CSS atoms did not recur;
  instead the strip held HTTP/session strings, including this
  run's own groom URL — a content landmark of a new class.
- Extent: P10240 (~30.2K) holds a CSS atom
  ("-webkit-validation-bubble-message"); P11520 (~34.0K) is JSC
  territory ("Unexpected identifier", "IsoSpace
  UnlinkedProgramCodeBlock"). The ray tours named subsystems:
  WebCore atoms around 30K, network/session around 32K, JSC
  around 34K.
- Caution: an "IsoSpace" string names a JSC class. It is not,
  by itself, proof of iso-heap allocation on this console.

## 5. Census (12 strips, 0 to ~164K on one ray)

- First measured inter-allocation distance: a second copy of our
  own file sits in the P680 strip as a full BMP header at strip
  offset 484 — 2012 bytes past the first copy's data end
  (2592 bytes from its data start).
- Planted marker: a token planted in a JS global, a DOM text
  node, and document.title was found in 0/12 strips, in ASCII
  and UTF-16LE. Planted strings live outside these rays.
  (Other session strings were readable in the near field, so
  readability is not the issue.)
- Zero deserts: 5/12 census strips are all zeros.
- Near-field fixture confirmed a third time: the P170 pointer
  family again at offsets 6/14/22/46, same shape, relocated
  values; P170 nonzero count 256 this session, versus 31/35
  in runs 1/2, with prior-page strings present.
- Far field differs every run, as in section 4.

## 6. Why is there a second copy? (mechanism v1)

Five P680 draws, no grooms, probe files of unique sizes
(584/616/712) never loaded before.
- Plain draws (3): nonzero count 131 in all three, zero headers.
- Busted draws (2, fresh URLs, same bytes): first draw zero
  headers; second draw one header at offset 452 — a second copy
  1980 bytes past the first copy's data end (2560 from data
  start), 32 bytes different from the census figure of 2012.
- Probe headers: 0/5 draws.

Grades, stated exactly:
- A shared cache entry as the sole explanation is ruled out —
  the fresh-URL draw still duplicated.
- A per-load duplicate is possible, but intermittent (1/5
  draws) and distance history-dependent (1980 vs 2012), not
  rigid pipeline adjacency.
- Files-as-landmarks do not generalise to unrelated loads:
  the landmark must be load-adjacent to the reading segment.
  Designable landmarks are not yet achieved.

## 7. Before/after: can an action's footprint be measured? (differential v1)

One ray (P680), 510-byte strips. Baselines A and B, with no
action between them: A nonzero 131, B nonzero 0 — the noise
floor is bimodal, not a single number. Action: eight loads of
a 584-byte probe file, each under a distinct URL.
- Post-action strip C: nonzero 449, BMP header (size 584) at
  offset 484 (= 2012 past data end).
- Post-action strip D: nonzero 444, BMP header (size 584) at
  offset 452 (= 1980 past data end).
- The action's own files landed in the ray in both post draws.
  Placement is bimodal, 32 bytes apart — the same two distances
  as census (2012) and mechanism (1980), now for a different
  file size and within one session.

New analysis of the saved C and D strips (recomputed from the
saved bytes):
- C and D are the same byte sequence shifted by 32 bytes:
  C[32:426] equals D[0:394] exactly.
- Under that shift they agree on 439 of 478 compared
  positions; all 39 differences lie in D positions 396–445,
  not spread across the strip.
- So most of the unshifted C-vs-D churn (456/510 differing)
  is the shift itself, not independent churn.
- The ramp bytes at the start of each strip (+1 sequences
  starting at 0x94 in C and 0xb4 in D) are observed only;
  their identity is unidentified.
- The shift is exact arithmetic on saved bytes. It is not,
  by itself, proof of a slot size or a placement mechanism.

## What is NOT claimed

- No kernel access, no write primitive, no payload, no
  pointer values, no addresses.
- No claim about what causes the 32-byte shift, the duplicate
  copy, or the bimodal placement — those are observed
  regularities, not mechanisms.
- QSA counts, range extractions, and serializer behaviour in
  the v3 sprint remain unmeasured.
- The C-20 map v4 design (body-scoped probes first, doc-scoped
  last) is designed, not built or run.

## What we would like back from the community

- Does anyone else's webview geography look like this — a
  near-field fixture with a session-dependent far field?
- Does the 1980/2012 bimodality, or the 32-byte C/D shift,
  match anything you have seen in the drops or in other
  engines?
- Corrections welcome, especially where a measurement above
  can be re-derived differently. Claims from other work will
  be treated the same way we treat our own: verified before
  they move into any document.

