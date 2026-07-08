# Release Notes

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


## 1.0.0

Initial release build.
