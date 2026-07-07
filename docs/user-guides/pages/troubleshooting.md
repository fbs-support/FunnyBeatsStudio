# Troubleshooting

Start with the status bar. FunnyBeatsStudio reports most workflow failures
there first, and longer failures may point to a local diagnostic file.

## FFmpeg or ffprobe is not found

Open `Options > FFmpeg Settings`.

Check that:

- `ffmpeg.exe` and `ffprobe.exe` exist;
- both paths point to executable files, not just a folder;
- both tools come from the same FFmpeg build when possible;
- the app can access the folder.

If explicit paths are blank, the app also checks `tools/ffmpeg/bin` inside the
extracted app folder and then `PATH`.

## A video will not load

Check that:

- the file extension is a supported video type;
- ffprobe can read the file;
- the file has a video stream, not audio-only content;
- the file is not locked by another application;
- the path is still valid after moving or renaming files.

If video probing fails, no video is attached to the project.

## A matching funscript was not imported

For automatic sidecar import, the script files must use the same base name as
the video.

Example:

```text
example.mp4
example.funscript
example.roll.funscript
```

If the file uses an unsupported version, invalid content, unsupported axes, or
duplicate axis ownership, import is rejected instead of silently dropping data.
Use `File > Import funscript` to test explicit import separately from video
loading.

## Beat analysis is unavailable or poor

For `Instant` and `Fast`, confirm that the loaded video has an audio stream and
that FFmpeg can extract analysis audio.

For `High precision`, open:

- `Options > Python Runtime`;
- `Options > Audio Stem Separation Model`.

Check or install the required assets. High precision also depends on compatible
local NVIDIA CUDA support. If High precision is not available, use
`Fast` or `Simple beat`, then repair the grid with Beat editing.

If analysis produces too many or too few markers, adjust Detection sensitivity
one step at a time. If the beat/accent roles or inferred repairs feel wrong,
adjust Beat judgment sensitivity one step at a time.

## Multi song boundaries are wrong

Use the timeline boundary review workflow before confirmed Multi song analysis.

Accept only useful boundaries, delete incorrect proposals, and add manual
boundaries where the song or tempo really changes. Boundary proposal is an
assistant, not an automatic final decision.

## Beatbar preview finds the wrong hits

Check the calibration before changing many thresholds:

- the beatbar region should include only the relevant visual area;
- the target region should be tight enough to avoid unrelated animation;
- cue direction and cue anchor should match the visible movement;
- hit and non-hit samples should be correctly labeled;
- timing offset should be adjusted if all hits are consistently early or late.

Use `Preview` before `Analyze full video`. If audio snap is enabled, make sure
the beat grid is already trustworthy.

## Beatbar AI says the model is not ready

Open `Options > Beatbar AI Model`.

Check or install the Beatbar AI assets, confirm local CUDA/GPU availability, and
verify any required upstream gated access. Non-AI beatbar workflows remain
available without Beatbar AI assets.

If the guidance says calibration needs clearer samples, remove mistaken samples,
add clearer Hit examples and visible negative examples, or tighten the target
region.

## Motion generation creates no preview points

Check that:

- a video is loaded;
- the chosen timing source has usable markers;
- the target axis or enabled axes are selected correctly;
- `Min interval (ms)` is not too high;
- constraints are not rejecting all candidates;
- beatbar timing is available if selected as the timing source.

Try a simpler single-axis preview from the beat grid before multi-axis
generation. If that works, reintroduce companion axes and modifiers gradually.

## Generated motion is too fast or too dense

Use:

- lower companion activity in Multi axis mode;
- lower modifier intensity;
- higher `Min interval (ms)`;
- lower `Max speed`;
- selected-point constraints after applying;
- manual deletion of unnecessary points.

Speed-violation rendering helps identify sections that need cleanup.

## Video replacement export fails

Check that:

- a source video is loaded;
- a beat grid exists and contains eligible markers;
- the source library folder exists and contains readable video files;
- the output folder exists or can be created;
- FFmpeg and ffprobe resolve;
- numeric settings are within reasonable ranges;
- the selected source videos are long enough for the planned segments.

Unreadable individual library files can be skipped, but the export fails when
the remaining eligible pool cannot satisfy the render plan.

## The app feels slow during analysis or export

Try these settings:

- keep FFmpeg hardware acceleration on `Disabled` or `Auto` until basic
  workflows are stable;
- reduce maximum concurrent FFmpeg processes;
- reduce beatbar frame preparation workers;
- close other GPU-heavy applications before AI analysis;
- use shorter preview ranges before full scans.

Large full-video beatbar scans and video replacement exports are naturally more
expensive than timeline edits.

## Where to find logs

Open `Options > Diagnostics`, then open the diagnostics folder.

Logs are local troubleshooting files. They may contain local paths or
machine-specific details. Do not publish them without reviewing and removing
private information first.

Use the cleanup command to remove app-created diagnostic files.
