# Release Notes

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
