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

Manual and deterministic beatbar workflows do not require optional AI assets.
The model-backed State (AI) and Cue (AI) workflows require verified Beatbar AI
assets from `Options > Beatbar AI Model`.

## Calibration concepts

The calibration overlay is drawn directly on the video. It stores normalized
video-frame rectangles, so the same calibration can be reused even when the
window size changes.

Important regions:

- `Beatbar region`: the larger visual area containing the cue or bar.
- `Target region`: the smaller region or target state to detect.
- Reference samples: saved examples of cue templates, hit moments, non-hit
  moments, or AI sample roles.

Use `Set region and target` to draw the regions. Use `Suggest regions` when you
want the app to propose likely beatbar rectangles, then confirm or redraw the
right one.

## Detector choices

Choose a detector that matches what is visible in the source video:

- `Cue tracking`: tracks a moving cue crossing a target.
- `Target state`: detects a visible state change inside the target region.
- `State (AI)`: uses the optional local DINOv3 scorer with hit and non-hit
  sample evidence.
- `Cue (AI)`: experimental model-backed cue-event detection for explicit
  evaluation.

Use deterministic `Cue tracking` or `Target state` first when the visual signal
is simple and clear. Use AI detectors only when the deterministic detectors are
not expressive enough for the source.

## Cue tracking setup

Use cue tracking when a marker travels across the beatbar.

1. Set the beatbar and target regions.
2. Choose the cue travel direction.
3. Choose the cue anchor, such as center, leading edge, or trailing edge.
4. Capture a cue template sample if the panel requests one.
5. Click `Preview`.
6. Adjust `Min interval ms`, `Interpolation gap ms`, or `Timing offset ms` if
   preview hits are too dense, missing, or consistently early/late.

Cue tracking hit times are interpolated between video frames where the tracked
cue crosses the target.

## Target state setup

Use target-state detection when the target area flashes, fills, changes color,
or otherwise enters a visible hit state.

1. Set the beatbar and target regions.
2. Capture at least a few clear hit and non-hit examples.
3. Click `Preview`.
4. Adjust `Detection`, `Release`, `Min interval ms`, and `Timing offset ms`.
5. Run `Analyze full video` once preview hits look reasonable.

If detection chatters, raise `Min interval ms` or adjust threshold values. If it
misses obvious hits, lower the detection threshold carefully.

## State (AI) and Cue (AI)

Use `Options > Beatbar AI Model` before using model-backed beatbar detectors.
The app verifies the approved local assets and runs the model through an
external worker. The main project file stores only safe analysis definitions and
results, not local model paths or frame data.

For State (AI):

- capture clear `Hit` examples;
- capture clear visible negative examples from the same target region;
- avoid occluded or ambiguous samples;
- use `Recommend settings` after sample capture when available;
- review `Calibration review` quality before full scan.

If the AI guidance says calibration is insufficient, add clearer samples,
remove mistaken samples, tighten the target region, or fall back to deterministic
State or Cue detection.

## Preview before full scan

Always use `Preview` before `Analyze full video`.

Preview lets you check a bounded section quickly. Full scan processes the video
and replaces the current beatbar result only after success. If a full scan is
canceled or fails, the previous valid result is preserved.

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

Enable `Show beatbar cue hits on timeline` to display beatbar cue hits in the
timeline. These markers can serve as a timing source for motion generation.

Keep beatbar cue markers visible while reviewing a scan. Hide them when you want
to focus on script point edits.

## Practical review checklist

- The calibrated region covers only the relevant visual cue.
- Preview hits align with obvious visual cue events.
- Extra repeated decorations are not being detected as hits.
- Timing offset is corrected before full scan.
- Audio snap is used only with a trustworthy beat grid.
- AI sample labels are clean and not accidentally reversed.
