# Quick Start

This guide walks through the shortest release-user workflow: configure media
tools, load a video, analyze beats, generate an editable draft, review it, and
export `.funscript` files.

![Main window after a video is loaded](./images/main-window-loaded-video.png)

## 1. Configure FFmpeg

1. Open `Options > FFmpeg Settings`.
2. Confirm that `ffmpeg` and `ffprobe` are found.
3. If they are not found, use `Browse` to set the explicit paths.
4. Leave hardware acceleration on `Disabled` or `Auto` for the first run.

FFmpeg is required for media probing, audio extraction, beatbar analysis, and
video replacement export. ffprobe is required to read video metadata.

## 2. Load a video

Use `File > Load video`, or drag a supported video file into the main window.

Supported drag-and-drop video extensions are:

- `.mp4`
- `.mkv`
- `.mov`
- `.avi`
- `.webm`
- `.wmv`
- `.m4v`

When you load a video, the app probes metadata with ffprobe and attaches the
video to the active project timeline. Loading a video does not automatically
analyze beats or generate motion.

If matching same-base-name `.funscript` files are next to the video, the app
imports them during video loading. For example, loading `example.mp4` can import
`example.funscript` and supported per-axis sibling files such as
`example.roll.funscript`.

## 3. Save the project

Use `File > Save` after loading the video.

Project files use the `.fbsproj` format. They store editor state such as the
loaded video reference, beat analysis data, beatbar data, and timeline points.
They do not embed the video file, FFmpeg binaries, local model paths, decoded
frames, or optional app-managed assets.

## 4. Analyze beats

1. Open `View > Beat generation` or press `Ctrl+1`.
2. Choose an analysis mode.
3. For a first pass, use the default profile and sensitivity values.
4. Run the analysis and wait for the status bar to report completion.
5. Review the beat markers on the timeline.

Use `Edit > Beat editing...` or `Ctrl+B` when the generated beat grid needs
manual repair. See [Beat editing](./beat-editing.md) for the dedicated repair
workflow.

## 5. Generate a motion preview

1. Open `View > Motion generation` or press `Ctrl+3`.
2. Choose `Single axis` or `Multi axis`.
3. Select a style, timing source, target axis, and apply mode.
4. Click `Generate preview`.
5. Review the preview overlay in the timeline.

Preview generation is non-destructive. It shows proposed points before they are
committed to the editable timeline.

## 6. Apply and edit

When the preview looks useful, apply it from the Motion generation panel.

After applying, the points become normal editable timeline points. You can:

- select, move, copy, cut, paste, and delete points;
- add a point at the playhead with `Enter`;
- right-click points for context-menu edits;
- use `Edit > Point modifiers...` for selected-point transformations;
- use Undo and Redo for committed editor actions.

See [Point editing](./point-editing.md) for point movement, snapping,
modifiers, and speed-violation review.

## 7. Export funscripts

Use `File > Export funscript`.

FunnyBeatsStudio exports multi-axis timelines as `.funscript` data according to
the configured export format in `Options > Settings`. For broad compatibility,
confirm the target format expected by the player or tool that will consume the
exported files.

## Recommended first session

For your first project, keep the workflow simple:

1. Configure FFmpeg.
2. Load a short local video.
3. Run beat analysis.
4. Generate a single-axis preview.
5. Apply it.
6. Manually edit a few points.
7. Export and inspect the `.funscript` output.

After that path works, try beatbar analysis, multi-axis generation, optional
HighPrecision analysis, or video replacement export.
