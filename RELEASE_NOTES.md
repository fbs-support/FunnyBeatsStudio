# Release Notes

## 1.2.0

Changes since `1.1.1`.

### Added

- Added a `Structure` timeline layer with `Song boundary` and `Meter boundary`
  tabs. The Meter boundary tab shows confirmed meter regions and reviewable
  suggestions directly against the audio pulse grid.
- Added timeline tools for comparing up to three meter candidates per detected
  section, accepting or rejecting a suggestion, editing pulse grouping and an
  optional time signature, and moving region edges or the first complete
  measure anchor. Committed meter edits are undoable.
- Added `Maximize segment speed` to Point modifiers. It preserves each selected
  segment's timestamps and original rise or fall direction while maximizing
  travel within both its own speed ceiling and the overall speed ceiling.

### Changed

- `Instant`, `Fast`, and `High precision` analysis now evaluate musical meter
  and phase from the available rhythm evidence instead of marking every fourth
  beat by default. Ambiguous results remain suggestions and do not affect
  generation until they are accepted.
- Meter structure is now kept separately from editable Beat markers. A compact
  structural pulse grid preserves bar phase when a non-anchor Beat is deleted,
  changed to an Accent, inferred, or hidden by a display filter.
- Improved meter and downbeat analysis for syncopated material, sparse or
  interrupted pulse grids, variable meter, and multi-song videos. Adaptive
  analysis also uses grid quality to avoid unsuitable half- or double-time
  choices.
- Removed Beatbar audio snap. The `Unified` timing view now resolves nearby
  audio and visual evidence automatically while committed Beatbar hits retain
  their native visual timestamps. Changing an accuracy or post-processing
  setting clears the old preview; click `Preview` to check the new values.
- Consolidated vibration output on one UI axis named `Vibe` (`Vibe0`
  internally). The separate Vibe axes and the `Vibe reactive` preset have been
  removed, and the remaining presets use the single Vibe axis.
- Saved `Set measure start` commands now retain the primary pulse count,
  grouping, and optional time signature. Older saved commands reopen as one
  group of the stored size with notation left unknown.

### Fixed

- Fixed meter proposal, boundary, and anchor presentation so controls remain
  usable near shared edges and while the timeline is scrolled.
- Fixed meter-region edits across gaps so valid structural pulse ordinals,
  measure phase, and variable-meter sections are preserved.
- Fixed `Maximize segment speed` changing the intended direction of selected
  segments.

### Notes

- Projects saved by `1.2.0` use project format version `17` and are intended for
  `1.2.0` or later. Keep a copy before saving if you need to return to an older
  release.
- Older projects still open, but points on the removed `Vibe1`, `Vibe2`, and
  `Vibe3` axes are discarded and are not merged into `Vibe0`. Convert or back up
  those points before opening and saving the project in `1.2.0`.
- The single Vibe axis continues to use `.vib0` for version `1.0` sidecar files,
  `V0` for version `1.1` axis IDs, and `vib1` for version `2.0` channel names.
- Older projects do not gain explicit meter structure automatically. Rerun beat
  analysis, set meter regions manually, or create and review a proposal from
  stable legacy downbeats when needed.

## 1.1.1

Changes since `1.1.0`.

### Added

- Added `Saved commands` to Point modifiers and Beat editing. After applying a
  supported edit, users can name it and reuse the same values with the current
  selection in one click.
- Saved commands are available across projects and app restarts. They can be
  reordered by dragging, reviewed by hovering, and removed when no longer
  needed.
- Added position-based keyboard shortcuts for the first 30 saved commands in
  each editor. Reordering a command also changes its shortcut position.

### Fixed

- Video replacement exports now include committed beatbar timing alongside
  audio beats when choosing visual cuts. Beatbar-supported downbeats also keep
  their downbeat behavior during export.
- Fixed source clips becoming quieter in 2x2 video replacement segments when
  the left/right audio balance was applied.

### Notes

- Saved commands store an operation and its values, not the points, beats, or
  selection it was created from. Each command runs against the current editor
  context and is not included in project or funscript files.

## 1.1.0

Changes since `1.0.1`.

### Added

- Added a `Unified` beat grid view that resolves audio beats and committed
  beatbar hits into one reviewable timing layer.
- Added timeline evidence badges for beat markers, so users can see whether a
  marker is supported by audio analysis, beatbar analysis, or both.
- Added a `Beatbar evidence` control to Motion generation. Users can keep
  beatbar hits as timing-only hints or make beatbar-supported beats drive
  stronger generated motion.

### Changed

- Motion generation now uses the unified beat grid instead of asking users to
  choose between audio beat analysis and beatbar cue hits.
- Beatbar hits that line up with reliable audio beats are merged into one timing
  marker, reducing double-hit drafts while preserving the visual cue as evidence.
- Beatbar-only timing can still contribute to generated motion when no suitable
  audio beat is nearby.
- The Beat grid read-only comparison tab is now named `Unified` instead of
  `Mixed`.
- Beat marker tooltips are shorter and focus on timestamp, confidence, local
  interval, and local BPM.
- Saved projects now store beat timing evidence in the current project format,
  including whether saved timing came from audio, beatbar, or both.

### Notes

- Projects saved by `1.1.0` use a newer project format and are intended for
  `1.1.0` or later. Keep a copy before saving if you need to return to
  `1.0.1`.
- Older projects still open, but beat analysis and beatbar analysis results
  saved by `1.0.1` or earlier are not reused. Existing videos and script points
  remain, but users should rerun audio or beatbar analysis after upgrading when
  they need those timing layers.
- The old motion-generation timing source setting is replaced by `Beatbar
  evidence`. Older settings fall back to the balanced beatbar evidence behavior.

## 1.0.1

Changes since `1.0.0`.

### Added

- Added a separate stem separation cache location in `Options > Storage Location`.
  Users can choose a custom cache folder, return to the default, and clean
  app-created stem cache files from the selected cache location.
- Added app-managed stem cache indexing and cleanup. Cleanup removes known stem
  cache entries and the cache index while preserving unrelated files and folders
  in the selected cache root.
- Added dedicated last-used settings for selected-point modifiers. Modifier
  input values are restored independently from motion generation settings.

### Changed

- High precision stem analysis now stores derived stem cache entries under the
  configured stem cache root instead of beside the source video.
- Selected-point modifier Humanized random seeds remain reusable during the
  current panel session, but are not saved as last-used settings.
- Motion generation last-used settings no longer save random seeds.

### Notes

- Existing video-side stem cache entries are not migrated or reused. The first
  High precision stem analysis after upgrading may rebuild stems in the
  configured cache location.
- Changing the optional asset storage location still requires checking Python,
  stem, and beatbar AI assets again before dependent workflows are enabled.
  Changing only the stem cache location does not clear those asset checks.
