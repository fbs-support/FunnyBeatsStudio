# Motion Generation

Motion generation creates editable draft `.funscript` points from timing
sources such as beat analysis or beatbar cue hits. Generated points are drafts:
review them, apply the useful parts, and edit the committed timeline before
export.

![Motion generation preview](./images/motion-generation-preview.png)

![Selected point modifiers](./images/selected-point-modifiers.png)

## Open the Motion generation panel

Use `View > Motion generation` or press `Ctrl+3`.

The panel supports:

- `Single axis`: generate one target axis.
- `Multi axis`: generate coordinated points across several motion and Vibe
  axes.

The normal sequence is:

1. Create or repair timing data with beat analysis, beat editing, or beatbar
   analysis.
2. Open Motion generation.
3. Choose mode and settings.
4. Click `Generate preview`.
5. Review preview points on the timeline.
6. Apply the preview if it is useful.
7. Continue editing committed points manually.

## Timing source

The timing source decides which markers drive generation. Common choices include
the analyzed beat grid and beatbar cue hits.

Use beat-grid timing for rhythm-following motion. Use beatbar timing when the
video's visual cue is more important than the audio grid, or when a Cock Hero
beatbar defines the intended hit moments.

## Single axis mode

Use `Single axis` when you want a focused draft on one axis before adding
companion motion.

Important controls:

- `Style`: choose the generation style.
- `Timing source`: choose beats, accents, beatbar hits, or another available
  timing source.
- `Target axis`: choose the axis to populate.
- `Max speed`: limit generated motion speed.
- `Min interval (ms)`: avoid overly dense points.
- `Apply mode`: choose how preview points are committed.

Single-axis generation is a good first pass because the result is easier to
inspect and edit.

## Multi axis mode

Use `Multi axis` when you want coordinated motion across several axes.

Important controls:

- `Preset`: load a starting set of enabled axes and tuning.
- `Motion axes`: enable or disable companion motion axes.
- `Vibe axes`: enable or disable Vibe channels.
- `Companion strength`: adjust companion movement range and intensity.
- `Companion activity`: adjust companion gesture frequency.
- `Apply mode`: choose how generated axes are merged or replaced.

Preset choices include:

- `Balanced`
- `Expressive dance`
- `Minimal companion`
- `Vibe reactive`

Start with `Balanced`. Increase companion strength or activity only after the
baseline is reviewable.

## Apply modes

Multi-axis apply modes are:

- `Replace generated axes`: replaces existing points only on axes that have
  generated preview output. Unrelated axes are preserved.
- `Merge into generated axes`: keeps existing points and inserts preview points
  using normal axis-plus-timestamp replacement rules.

Use replace when the generated draft should become the new version of those
axes. Use merge when you have manual edits that should remain and you only want
to add generated material.

## Preview behavior

`Generate preview` is non-destructive. Preview points appear on the timeline but
are not committed until you apply them.

Changing effective generation inputs clears the current preview. Applying a
preview commits the points as one undoable editor action and clears the preview.

If every enabled axis produces zero preview points, review the diagnostic text
and timing source before changing style controls.

## Modifier tabs

The Motion generation panel includes `Styles` and `Modifiers` tabs.

Use style controls for the broad generated pattern. Use modifier controls when
you want additional timing or motion behavior, such as:

- half-time or double-time behavior;
- groove weighting;
- build-up shaping;
- drop-lock preparation;
- call-and-response fills;
- hard beat bouncing;
- tremolo bursts;
- humanized variation.

Modifiers can make drafts busier. Increase them gradually and review the
timeline after each preview.

## Selected-point modifiers

Use `Edit > Point modifiers...` or `Ctrl+M` after selecting committed timeline
points. This panel transforms existing points; it does not use motion-generation
preview input. See [Point editing](./point-editing.md) for the full committed
point editing workflow.

Supported selected-point actions include:

- `Insert points`
- `Insert midpoints`
- `Alternate positions`
- `Curving`
- `Timing`
- `Half-time`
- `Double-time`
- `Groove`
- `Build Up`
- `Tremolo`
- `Hard Beat Bouncing`
- `Humanized`

Each modifier card has its own `Apply` button. One modifier application is one
undoable edit when it changes points. Result points remain selected so you can
chain another modifier intentionally.

## Constraints

Use constraints to keep generated helpers practical:

- `Maximum helper speed`
- `Minimum interval (ms)`
- `Minimum travel`

The constraints section also has an `Apply` action for position-only repair of
the current selection. It edits committed points; it is not a preview.

## Recommended motion workflow

1. Repair beat or beatbar timing first.
2. Generate a simple single-axis preview.
3. Apply only when the timing feels useful.
4. Manually fix obvious point issues.
5. Use selected-point modifiers for local decoration.
6. Try multi-axis generation after the main timing path is solid.
7. Toggle `Goods preview` with `Ctrl+5` to inspect coordinated axes.

Generation is strongest when it starts from trustworthy timing data. Bad beat
or beatbar markers usually create bad motion drafts.
