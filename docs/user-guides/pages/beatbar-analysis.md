# Beatbar Analysis

Beatbar analysis detects visual cue hits from the loaded video. It is useful
when the video contains an on-screen beatbar, target marker, cue animation, or
other repeated visual timing signal.

![Beatbar analysis calibration](./images/beatbar-calibration.png)

## Open the Beatbar Analysis panel

Use `View > Beatbar Analysis` or press `Ctrl+2`.

Beatbar analysis needs:

- a loaded video;
- configured `ffmpeg` and `ffprobe`;
- a calibrated beatbar or target region;
- detector settings that match the visual cue.

Deterministic State does not require optional AI assets. Cue (AI) and State
(AI) require verified Beatbar AI assets from `Options > Beatbar AI Model`. When
those assets are available, Cue (AI) is the normal default for visible cue
events.

## Calibration concepts

The calibration overlay is drawn directly on the video. It stores normalized
video-frame rectangles, so the same calibration can be reused even when the
window size changes.

Important regions:

- `Beatbar region`: the larger visual area containing the cue or bar.
- `Target region`: the smaller region or target state to detect.
- Reference samples: saved examples of hit moments, visible non-hit moments,
  or AI sample roles.

Use `Set region and target` to draw the regions. Use `Suggest regions` when you
want the app to propose likely beatbar rectangles, then confirm or redraw the
right one.

## Detector choices

Choose one of the three current detector styles:

- `Cue (AI)`: default model-backed cue-event detection for moving markers,
  arrivals, crossings, contacts, dense cue rows, and cue artwork that changes
  over time.
- `State (AI)`: model-backed target or instruction-state detection for flashes,
  glows, occlusion, target-state changes, or layouts with no reliable cue
  trajectory.
- `State`: deterministic TargetState v2 CPU fallback for simple target-state
  flashes or when optional AI assets, CUDA, or the worker are unavailable.

Standalone deterministic `Cue tracking` is retired. Do not use old cue-template
setup instructions for new projects.

## Cue (AI) setup

Use Cue (AI) when a visible marker or cue event is the clearest timing signal.

1. Set the beatbar and target regions.
2. Choose or confirm the cue travel direction and anchor when the panel exposes
   those scorer hints.
3. Capture clear hit and visible non-hit examples.
4. Click `Preview`.
5. Adjust the selected Cue preset, `Min interval ms`, confidence threshold, or
   `Timing offset ms` if preview hits are too dense, missing, or consistently
   early/late.
6. Use `Recommend settings` when available, then review the pending full-scan
   result before applying it.

Cue (AI) uses an internal proposal/scoring pipeline. It does not store old
cue-template samples in the project file.

## State setup

Use deterministic State when the target area flashes, fills, changes color, or
otherwise enters a visible hit state and the local CPU fallback is sufficient.

1. Set the beatbar and target regions.
2. Capture at least a few clear hit and non-hit examples.
3. Click `Preview`.
4. Adjust `Detection`, `Release`, `Min interval ms`, and `Timing offset ms`.
5. Run `Analyze full video` once preview hits look reasonable.

If detection chatters, raise `Min interval ms` or adjust threshold values. If it
misses obvious hits, lower the detection threshold carefully or try State (AI)
for a more robust model-backed state scorer.

## State (AI)

Use `Options > Beatbar AI Model` before using State (AI). The app verifies the
approved local assets and runs the model through an external worker. The main
project file stores only safe analysis definitions and results, not local model
paths or frame data.

For State (AI):

- capture clear `Hit` examples;
- capture clear visible negative examples from the same target region;
- avoid occluded or ambiguous samples;
- use `Recommend settings` after sample capture when available;
- review `Calibration review` quality before full scan.

If the AI guidance says calibration is insufficient, add clearer samples,
remove mistaken samples, tighten the target region, or fall back to deterministic
State.

## Preview before full scan

Always use `Preview` before `Analyze full video`.

Preview lets you check a bounded section quickly. Full scan processes the video
and stages a pending result after success. If a full scan is canceled or fails,
the previous valid result is preserved.

Review the pending cue markers on the timeline before applying them. Pending
markers use a different color from committed markers. Use `Minimum confidence`
to hide lower-confidence final hits from the pending result; changing this
slider does not rerun video analysis, audio snapping, scoring, or
post-processing.

Use:

- `Apply`: commit the currently filtered pending result to the project.
- `Discard`: throw away the pending result and restore the previously committed
  timeline view.

Only applied beatbar cue hits are available as a motion-generation timing
source.

## Audio snap

Audio snap can align visual cue hits to the existing beat grid.

Use it when:

- you already ran beat analysis;
- visual hits are close to musical beats;
- small visual-timing offsets make generation feel late or early.

The main controls are:

- `Apply audio snap during full scan`;
- `Snap max ms`;
- marker policy such as beats-only or beats-and-accents.

Do not enable audio snap when the beat grid is wrong. Fix the beat grid first.

## Timeline cue markers

Beatbar cue hits appear in the Beat grid layer. `Mixed` shows them alongside
audio beats for comparison, and `Beatbar` shows committed hits as editable
markers. Pending markers are review-only until you apply the full-scan result.

To repair committed beatbar hits without rerunning analysis:

1. Switch to the Beat grid timeline layer.
2. Open the `Beatbar` tab.
3. Select the hit markers to edit.
4. Use `Delete`, midpoint insertion, fill, nudge, shift, stretch, redistribute,
   copy, or paste commands as needed.

Beatbar edits are undoable and change only the saved
`BeatbarAnalysisResult.Hits` list. Accent, downbeat, and measure-start commands
are Audio-only because beatbar hits do not store those fields.

## Practical review checklist

- The calibrated region covers only the relevant visual cue.
- Preview hits align with obvious visual cue events.
- Extra repeated decorations are not being detected as hits.
- Timing offset is corrected before full scan.
- Audio snap is used only with a trustworthy beat grid.
- AI sample labels are clean and not accidentally reversed.
