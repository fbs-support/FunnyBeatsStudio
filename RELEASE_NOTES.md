# Release Notes

## 1.2.3

Changes since `1.2.2`.

### Added

- Added the `Choreographed flow` multi-axis motion preset. It coordinates
  companion axes in phrase-scale pairs and bundles, varies motifs over longer
  sections to reduce short-loop repetition, and produces a sustained Vibe bed.
  All supported axes are enabled by default, and the existing companion
  strength, activity, and axis controls remain available before preview.

### Changed

- Audio reanalysis now preserves meter regions that you previously accepted
  from analysis, alongside manual and imported regions. Fresh analyzer timing,
  automatic regions, and review proposals are still replaced. If the new
  analysis timing cannot resolve a preserved region, the region remains visible
  while repeated measure lines and beat-aware emphasis may remain unavailable
  until the timing is repaired or reanalyzed.

### Fixed

- Improved High precision meter and downbeat analysis when several timing
  interpretations lead to the same measure boundaries. Equivalent results no
  longer create false ambiguity, and dense subdivisions are less likely to
  pull analysis toward an incorrect half- or double-time interpretation.
- Fixed timeline rendering regressions that could leave the selected timeline
  blank or stale after changing layers or rebuilding axis tabs. Multi-axis
  previews also appear correctly when generated while the Structure or Beat
  grid layer is open.
- Fixed timeline zoom and seek synchronization so zoom waits for the updated
  scrollable range before restoring its anchor, and delayed media-position
  updates do not unexpectedly recenter or overwrite a newer seek.
- Fixed crossfade video replacement exports allowing later placement audio to
  arrive early when a source audio stream or selected audio range ended before
  its video segment.
- Fixed point dragging so position `100` remains reachable when the point was
  grabbed away from its center. Continuing the drag beyond the plot boundary
  now contributes the full movement needed to reach either endpoint.

### Notes

- Project files continue to use format version `17`.

## 1.2.2

Changes since `1.2.1`.

### Changed

- Improved responsiveness on long or marker-dense timelines, including point
  and beat selection, rectangle selection, dragging, meter-handle previews,
  zooming, and switching timeline layers or tabs.
- Improved pulse, meter, and downbeat analysis for syncopated material, gaps,
  and half- or double-time ambiguity. Preliminary Beat and Accent labels no
  longer pull the structural pulse phase toward the wrong rhythm layer, and
  genuinely ambiguous sections remain Pending or unresolved instead of forcing
  a confirmed meter.
- Audio Beat timing edits now reconcile the structural pulse grid. Adding a Beat
  can create or repair a pulse slot, while moving or deleting a Beat retimes or
  removes any corresponding slot. `Toggle Beat/Accent` changes only the marker
  classification.
- Expanded timeline zoom to support visible windows from `1` through `300`
  seconds. Reset still returns to the default `20`-second view.

### Fixed

- Fixed valid manual meter edits being rejected or losing usable phase when
  analysis is incomplete. Within the current song region, edges can move through
  blank, rejected, Pending, or analyzer-derived pause areas up to the next
  confirmed region without inventing missing pulses. Repeated measure lines and
  beat-aware generation may remain unavailable where structural timing is
  unresolved.
- Fixed meter edits changing or deleting the underlying structural pulse
  evidence. Meter definitions, boundaries, and anchors now act as an overlay,
  so deleting a meter region keeps the analyzed pulse grid available for later
  meter definitions.
- Fixed meter commands requiring the marker at a meter position to be a Beat.
  Meter handles can use saved or resolved pulse positions, Beat or Accent
  markers, and a valid position on the Audio timeline when no timing candidate
  exists. Confirmed meter anchors also remain saved when the marker at that
  timestamp is changed with `Toggle Beat/Accent` or deleted.
- Fixed adjacent meter regions with matching definitions being combined when
  their structural phase conflicts or cannot be proved. The explicit boundary
  now remains until the user removes it.
- Fixed mouse-wheel timeline zoom also scrolling the timeline horizontally.

### Notes

- Project files continue to use format version `17`.
- A Pending meter proposal saved by an older analysis may require rerunning
  audio analysis before it can be accepted unchanged.

## 1.2.1

Changes since `1.2.0`.

### Added

- Added separate interval and amplitude controls for normal `Tremolo burst`
  motion and `Call and response` fill tremolo. Each set of last-used values is
  remembered independently between app launches.

### Fixed

- Fixed timeline zoom so buttons and keyboard shortcuts keep the current
  playhead timestamp centered, mouse-wheel zoom keeps the timestamp under the
  pointer in place, and rapid zoom input cannot restore an older view.
- Fixed point dragging to commit the final pointer-release position, including
  exact positions `0` and `100` when no final pointer-move event is delivered.
- Fixed Undo and Redo after timeline edits so they preserve the current zoom and
  move the playhead to the earliest timestamp changed by the restored edit.
- Fixed audio analysis navigation so `Structure` > `Meter boundary` opens
  whenever a section still needs meter review, including sections where no
  suggested meter card could be produced.
- Fixed normal tremolo bursts so they avoid incomplete alternating motion near
  position limits, use the configured interval and amplitude, and still respect
  nearby anchors, speed, spacing, and minimum-travel constraints.
- Fixed `Call and response` fill tremolo so it uses its own controls
  independently of normal tremolo detection and produces a clear fill toward
  the next phrase instead of flattened or misdirected motion.
- Fixed `Drop lock` preparation and bounce planning around nearby points and
  offset bounces. Valid preparation and landing points are retained while the
  bounce is reduced to the largest complete pattern that fits the constraints.

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
