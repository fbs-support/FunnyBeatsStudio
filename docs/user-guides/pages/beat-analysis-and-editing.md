# Beat Analysis and Editing

Beat analysis creates the timing grid used by snapping, beat editing, beatbar
audio snap, and motion generation. It does not create `.funscript` motion points
by itself.

![Audio analysis controls](./images/beat-generation-panel.png)

## Open the Beat generation panel

Use `View > Beat generation` or press `Ctrl+1`.

The panel has two main paths:

- `Simple beat` creates a BPM grid from typed values.
- `Audio analysis` analyzes the loaded video's audio and stores detected beat
  and accent markers in the project.

## Simple beat

Use `Simple beat` when you already know the song tempo or want a clean starting
grid without running audio analysis.

The inputs are:

- `Offset ms`: timestamp of the first generated beat.
- `BPM`: tempo in beats per minute.
- `Beats per measure`: meter used to mark generated downbeats.

Click `Generate simple beat` to replace the current beat grid. Generation
requires a loaded video with a known positive duration.

## Audio analysis modes

The `Audio analysis` tab exposes these modes:

- `Instant`: fastest local full-mix analysis.
- `Fast`: percussion-focused local analysis with fallback behavior when needed.
- `High precision`: stem-assisted analysis for difficult rhythm
  material.

`High precision` requires the optional Python runtime and stem analysis assets.
If those assets are not verified, the panel chooses `Fast` by default.

## High precision controls

When `High precision` is selected, the panel adds profile and sensitivity
controls:

- `Profile`: choose `Adaptive`, `Auto`, `Balanced`, or a genre-oriented profile
  such as electronic, rock/pop, hip-hop/trap, bass-driven, dense fills, or
  live/acoustic.
- `Multi song`: propose and confirm song regions before analyzing each region.
- `Detection sensitivity`: lower values keep only stronger rhythm events;
  higher values may include more accents and subdivisions.
- `Beat judgment sensitivity`: lower values require stronger beat-grid
  evidence; higher values trust stable tempo grids more when promoting accents
  to beats and repairing missing beats.

For a first pass, use `Adaptive` with both sensitivity controls at `Normal`.
Move sensitivity one step at a time and review the timeline after each run.

## Multi song analysis

Use `Multi song` when one video contains multiple songs or obvious tempo
sections. The workflow proposes boundaries, then asks you to confirm, delete,
add, or move boundaries on the timeline before final analysis.

Confirmed regions are analyzed independently and merged back into absolute
timeline positions. This avoids one song's tempo or profile forcing the rest of
the video into the wrong grid.

## Beat, accent, and downbeat markers

`Beat` markers are the primary musical skeleton. They define beat order,
ordinary snapping positions, downbeat phase, and the default timing source for
motion generation.

`Accent` markers are extra timing hints. Use them for offbeats, pickup notes,
rapid decoration, and fill moments that should help editing or generation
without changing the primary beat count.

Downbeats mark estimated measure starts. They render distinctly on the timeline
and help generation understand musical phrasing.

## Open Beat editing

Use `Edit > Beat editing...` or press `Ctrl+B`.

The Beat editing panel helps repair selected beat and accent markers after
analysis. It works on the beat-grid layer, not on script point axes. See
[Beat editing](./beat-editing.md) for the dedicated beat-grid repair guide.

## Common beat edits

Use these commands when the analysis is close but not perfect:

- `B`: add a beat at the playhead.
- `A`: add an accent at the playhead.
- `Delete`: delete selected beat or accent markers on the Audio tab, or
  committed beatbar hits on the Beatbar tab.
- `Fill from selected tempo`: project missing beats forward or backward from
  selected beats.
- `Redistribute run`: keep the selected run endpoints and space interior beats
  evenly.
- `Clear accents`: remove accent markers from a selected span.
- `Mark downbeat` and `Clear downbeat`: manually adjust measure starts.
- `Set measure start`: recalculate downbeat phase from one selected primary
  beat.

Beat editing commands preserve unrelated markers and are undoable when they
commit a change.

## Timing repair

The Beat editing panel includes timing tools:

- fixed nudge values such as `-10 ms`, `-5 ms`, `-1 ms`, `+1 ms`, `+5 ms`, and
  `+10 ms`;
- frame-step nudge when the loaded video frame rate is known;
- typed shift offsets;
- stretch range controls.

Use small nudges when a section is consistently early or late. Use stretch only
when the first and last selected markers are trustworthy and the interior timing
needs retiming across that span.

## Suggested workflow

1. Run `Audio analysis`.
2. Watch a short section and compare beats against the video.
3. Add or delete obvious markers.
4. Use `Fill from selected tempo` or `Redistribute run` for local gaps.
5. Mark or correct downbeats in important sections.
6. Save the project before motion generation.

Beat analysis is usually worth reviewing before generation. A clean beat grid
makes generated motion easier to edit.
