# CHECKS-REPORT — temperature-is-concentration

PROOF GATE, written before the first slate compiles (ai-explainer SKILL.md).

```
9 SHOW / 1 justified-CARD / 0 PUNT

Teaching arc:  FRAMEWORK ✓ | WORKED EXAMPLE ✓ | FALSIFIABILITY ✓
               SCAFFOLDED TASK ✓ | BOOKENDS ✓ | NO-SOURCE-NO-VERDICT ✓
```

## Per-beat classification

| Beat | Act | Class | Artifact named in `shot.show` |
|---|---|---|---|
| B00 | ASK | SHOW | composer types the ask; 3 result lines land in sequence |
| B01 | BLUF | SHOW | writer types "a creativity dial", turns it terracotta, deletes, retypes "a concentration control" |
| B01A | ANALOGY | SHOW | contrast slider travels; three swatches spread to near-ink/near-white, then wash to one grey; the terracotta marker on the brightest never moves |
| B02 | FRAMEWORK | SHOW | 3 score chips → bars rise while their values count up → sum settles 1.000000 |
| B03 | ASK | SHOW | composer with the plot request typed; send button pulses |
| B04 | MECHANISM | SHOW | identity types in; gap pins at 2; three ratio bars grow to 4/2/1 units; e-column lands |
| B05 | BOUNDARY | SHOW | bars sweep T=1→0.1; sliver remains; refusal card snaps; closing line holds alone |
| B06 | VERDICT | SHOW | artifact page reveals 4 lines in narration order, boundary line last in terracotta |
| B07 | HANDOFF | SHOW | the viewer's prompt types itself in full, held for pausing |
| B08 | OUTRO | CARD | title restate + credit (reel-local Manim) — **justified**: the outro brand card is a CARD by doctrine (OUTRO LAW) |

No beat is a bare CARD carrying a factual claim. No PUNTs.

## Teaching-arc checklist

- **FRAMEWORK before examples** ✓ — B02 builds the whole softmax machine before
  B04 uses it. The baseline distribution is on screen before any ratio.
- **WORKED EXAMPLE** ✓ — B04 computes p₂/p₀ at three temperatures and checks
  each against exp(2/T); the numbers are the chapter's own.
- **FALSIFIABILITY** ✓ — B05 is a dedicated boundary beat: it names what the
  explanation does NOT establish, and shows the function refusing T=0 rather
  than degrading gracefully. This is the 2-point rubric line, on screen.
- **SCAFFOLDED TASK** ✓ — B07 gives a runnable task with a specific
  perturbation (change only the middle score) and tells the viewer what to look
  for (which ratio stays fixed, and why it had to).
- **BOOKENDS** ✓ — cold open (B00) → BLUF (B01) → body → verdict (B06) →
  handoff (B07) → title outro (B08).
- **NO-SOURCE-NO-VERDICT** ✓ — every figure traces to `main.py`; see
  `FACTCHECK.md`. The one judgement claim ("concentration is not
  correctness") is stated as an argument, never as a measurement.

## PPT test

No two consecutive beats share a visual scheme, and no beat is a headline over
a paragraph: B02/B04/B05 animate their mechanism, B01 animates its own
correction, B06 reveals line by line, B07 types. The only static hold is the
2.47s outro.

## Legibility contract

Checked on every SHOW beat: artifact named in `shot.show`; ~15–35% negative
space; nothing faded below ~40%; the three-temperature comparison in B04 is
side-by-side and held well over 2s (each row holds ≥2.8s).

## Gate status at time of writing

| Gate | Result |
|---|---|
| A — static pre-flight (all 5 Manim scenes) | CLEAN — B08 carries the expected non-blocking "text-only" note (it is a title card) |
| W — WCAG + margins + overlap (all 5) | CLEAN |
| L — library-first | 3 hits, 0 slates; the outro gap is filled in-reel (see SHOTLIST.md). B01A re-ran the gate — `./art scenes "everyday analogy: contrast knob rescales differences without reordering"` returned 5 candidates, all unrelated figure scenes (top score 6.0, a WCAG contrast meter). A genuine PUNT, so the beat was authored in the reel's own `scenes.py` rather than slated. |
| F — paperwork set | FACTCHECK.md · SHOTLIST.md · PROMPTS.md present |
| B — post-render layout audit | CLEAN — 27 snapshots, 0 errors, 0 warnings (`--curve-strict`, `ART_STRICT=1`) |
| V — frame-level visual QC | CLEAN — 20 frames, 0 BLOCKER, 0 MAJOR. Round 1 found 6 MAJOR (canvas-fill); the B01A pass found a caption defect the sampler missed (below). |

### GATE V round 1 → fixes applied

| Defect | Beat | Root cause | Fix |
|---|---|---|---|
| empty-frame | B05 @85% | card faded out before the closer faded in | cross-fade in one `play`; closer lands beneath the card |
| underfill 37% | B04 @50% | rows revealed one at a time, so the midpoint was half-empty | table frame (all 3 `T =` + strip) lands first, values populate after |
| underfill 3%/9% | B01 @50/85% | component centres 2 lines; sample landed mid-typing | props only: 4 short lines, `fontSize` 76→120, `charMs` 46→22 |
| underfill 47% | B06 @50/85% | artifact card sized to 4 lines | 5th line added carrying the T=0.1 / T=0 evidence |

No gate was loosened and `ART_STRICT` stayed at 1 — every fix is a root-cause
fix in the reel's own source or props.


---

## B01A — the everyday-analogy beat (added 2026-09-22)

Added on request: the reel was correct but front-loaded with algebra, so one
beat now grounds the idea in something anyone has touched — a photo contrast
slider — before B02 opens the softmax.

**Why it is a SHOW and not a decorative card.** The slider is the mechanism:
sliding it rescales how much the three swatches differ while the marker pinned
to the brightest one never moves. That is the reel's two central claims
(temperature rescales the ratio; temperature never reorders) enacted in a
medium with no notation in it. The beat carries no figure from `main.py` and
says "analogy — illustrative, not measured" on screen for its whole duration,
so it cannot be mistaken for evidence. Fidelity argument in `FACTCHECK.md`.

**Placement.** After the BLUF (B01), before the framework (B02) — the advance
organizer lands, then the intuition, then the machine. Nothing was removed and
no number changed: the graded evidence beats B02/B04/B05/B06 are byte-identical
to the previous master (`input_sha256` in `temperature-is-concentration.verified.json`).

### Gate V round 2 — the defect the sampler could not see

| Defect | Beat | Root cause | Fix |
|---|---|---|---|
| Caption illegible mid-change (glyph soup) | B01A @ ~18.5s | `Transform()` between two `Text` mobjects interpolates letter-by-letter when the glyph counts differ; every caption change had a ~1.2s unreadable window | Replaced all four caption changes with an explicit `FadeOut`/`FadeIn` cross-fade (`swap_cap()` in `scenes.py`) |

Gate V samples 20 frames across 171s — roughly one per 8.6s — so a 1.2s garble
window is very likely to fall between samples, and did. It was caught by the
manual VISUAL QC LAW pass (frames at 15/50/85% of the beat's own span, read
rather than probed) and verified fixed at t=20.0s. Recorded here because the
lesson generalises: a gate that samples uniformly across a reel cannot be
trusted to catch a defect shorter than its sampling interval, and per-beat
sampling is the thing that actually finds them.

---

## B05 — the analogy callback, and captions (2026-09-23)

**B05 extended.** The boundary beat now closes on the B01A callback: the three
swatches return above the `ValueError` card at full contrast, and the line "a
sharper picture of the wrong person" lands beneath "concentration ≠
correctness". Narration 67 → 80 words; measured clock 23.70s → 26.30s; the
scene was rebuilt to the new duration rather than stretched. Reel total
171.24s → 174.08s (2:54), still inside the 2–4 minute target.

Classification unchanged — B05 was already SHOW and remains SHOW. The callback
adds a second, non-numeric encoding of the same boundary claim; it introduces
no figure, and the "analogy — illustrative, not measured" obligation was
discharged at B01A where the analogy is established.

**Captions added.** `align.py` produced word-level timing for all 10 beats (0
fallbacks — the caption text is the known narration snapped onto Whisper
timestamps, not a transcription). The reel's own `make_srt.py` emits the SRT,
because the toolkit's writer ships with the publishing skills and this pipeline
never publishes.

| Check | Result |
|---|---|
| Gate A / W — static pre-flight, WCAG, margins | CLEAN |
| Gate B — post-render layout audit | CLEAN, 0 errors / 0 warnings |
| Gate V — frame-level visual QC | CLEAN, 20 frames, 0 BLOCKER / 0 MAJOR |
| Manual per-beat frame pass | CLEAN — B05 ending read at t=22.0s and t=25.0s |
| Caption lint | 57 cues · longest line 42 chars · 0 cues over 2 lines · 0 overlapping or inverted timestamps · last cue ends 173.96s against a 174.17s timeline |

Two defects in `make_srt.py` were found by reading its output rather than its
exit code — a greedy wrap that overflowed to 51 characters, and a cue grouper
that flushed after exceeding its budget instead of before. Both fixed at the
root; the budget is now enforced against the *wrapped* lines, which is the
only formulation that actually holds.
