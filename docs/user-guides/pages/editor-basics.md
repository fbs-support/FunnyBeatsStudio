# Editor Basics

FunnyBeatsStudio is a timeline editor. Analysis and generation features create
useful drafts, but the timeline remains editable and reviewable before export.

![Main window after a video is loaded](./images/main-window-loaded-video.png)

## Main window layout

The main editor window is organized around three areas:

- The video pane shows the loaded source video.
- The playback row controls play, stop, frame stepping, seek, speed, mute, and
  volume.
- The timeline pane shows editable points, beat markers, previews, and the
  current playhead.

The status bar at the bottom reports operation progress, warnings, results, and
cancelable long-running work.

## Projects and videos

Use `File > New`, `File > Open`, `File > Save`, and `File > Close` for project
files. Use `File > Load video` to attach a local video to the current project.

When a video is loaded, its timeline starts at `00:00`. Script points and beat
markers use timestamps relative to the start of that video. Project files store
a reference to the selected video path, not a copy of the video.

Drag-and-drop can open a `.fbsproj` project or load a supported video file. If
you drop multiple items, the app uses the first recognized project or video and
ignores the rest.

## Playback and timeline sync

Playback, the current timestamp display, the timeline playhead, and visible
timeline center stay synchronized. The playhead is fixed near the center of the
timeline pane while the content scrolls underneath it.

Useful playback controls:

- `[` decreases playback speed by `0.25x`.
- `]` increases playback speed by `0.25x`.
- `R` resets playback speed to `1x`.
- Frame-step buttons move one frame at a time for detailed inspection.

Selecting exactly one committed script point seeks the editor presentation to
that point. Selecting multiple points changes the selection without surprise
seeking.

## Axis tabs

The timeline can contain multiple script axes. The visible axis tab controls
which committed points you are directly editing. Multi-axis generation and
import can populate several axes in one project.

Common axes include stroke-style motion axes and companion axes such as roll,
pitch, twist, surge, sway, and vibe-related axes. Not every project needs every
axis.

## Editing points

Committed script points are normal editable timeline data.

Use the top-level `Edit` menu for common commands:

- `Select all`
- `Copy`
- `Cut`
- `Paste`
- `Point modifiers...`
- `Add point at playhead`
- `Beat editing...`
- `Add beat at playhead`
- `Add accent at playhead`

Use the point context menu for timeline-specific commands:

- `Delete point`
- `Add point here`
- `Insert single midpoints`
- `Insert points on beat`
- `Reverse positions`
- `Snap to nearest beat`
- `Align selection to beat span`

`Enter` adds a position `50` point at the playhead without stopping playback.
This is useful for manual live tapping. If the active axis already has a point
at that timestamp, the command reports no change.

See [Point editing](./point-editing.md) for detailed point movement, snapping,
modifiers, readouts, and speed-violation review.

## Editing beats

Beat markers are edited in the separate Beat grid layer. Use `Edit > Beat
editing...` or `Ctrl+B` for settings-driven beat repair, and use `B`, `A`, and
`Delete` for quick beat-grid edits. In the Beat grid layer, use the `Audio` tab
for audio beats and the `Beatbar` tab for committed beatbar hits; `Mixed` is a
read-only comparison view.

See [Beat editing](./beat-editing.md) for beat, accent, timing, and downbeat
repair workflows.

## Selection, Undo, and Redo

Point edits are undoable editor actions. Commands that plan multiple changes,
such as midpoint insertion or modifier application, commit as one undo entry
when possible. No-op commands should not create undo entries.

Use:

- `Ctrl+Z` to undo.
- `Ctrl+Y` to redo.
- `Delete` to delete selected points in the point-editing layer.

## Visual feedback

The timeline draws point lines, selected points, beat markers, and generated
previews. Segments that exceed the active maximum speed threshold are rendered
as speed violations so you can spot motion that may be too fast.

Point tooltips show timestamp and position details. Near panel edges, tooltips
are clamped so they remain readable.

## Goods preview

Use `View > Goods preview` or `Ctrl+5` to toggle the left-side goods preview.
The preview samples the current timeline pose during playback and seeking, so it
is useful for checking multi-axis motion in context.
