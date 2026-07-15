# Keyboard Shortcuts

Application shortcuts work from the main editor window. When focus is inside an
editable text control, normal text editing takes priority.

## File and panels

| Shortcut | Action |
| --- | --- |
| `Ctrl+N` | New project |
| `Ctrl+O` | Open project |
| `Ctrl+S` | Save project |
| `Ctrl+1` | Open Beat generation |
| `Ctrl+2` | Open Beatbar Analysis |
| `Ctrl+3` | Open Motion generation |
| `Ctrl+4` | Open Video replacement export |
| `Ctrl+5` | Toggle Goods preview |
| `Ctrl+M` | Open Point modifiers |
| `Ctrl+B` | Open Beat editing |

## Saved commands

These shortcuts use the current order in `Saved commands`. They apply Point
modifiers in the points timeline layer and Beat editing commands in the Beat
grid timeline layer.

| Saved-command position | Shortcut |
| --- | --- |
| 1-10 | `Ctrl+Alt+1` through `Ctrl+Alt+9`, then `Ctrl+Alt+0` |
| 11-20 | `Ctrl+Shift+1` through `Ctrl+Shift+9`, then `Ctrl+Shift+0` |
| 21-30 | `Ctrl+Alt+Shift+1` through `Ctrl+Alt+Shift+9`, then `Ctrl+Alt+Shift+0` |

Top-row and numeric-keypad digits both work. The ordinal shown in each row's left
drag handle is its shortcut position. Drag the numbered handle to change that
position and shortcut. Rows after position 30 keep their ordinals and remain
clickable but have no number-key shortcut.

## Playback

| Shortcut | Action |
| --- | --- |
| `[` | Decrease playback speed by `0.25x` |
| `]` | Increase playback speed by `0.25x` |
| `R` | Reset playback speed to `1x` |

## Timeline point editing

These shortcuts apply in the points timeline layer.

| Shortcut | Action |
| --- | --- |
| `Ctrl+A` | Select all points on the visible axis tab |
| `Ctrl+C` | Copy selected points |
| `Ctrl+X` | Cut selected points |
| `Ctrl+V` | Paste copied points at the visible timeline center |
| `Enter` | Add a position `50` point at the playhead |
| `Delete` | Delete selected points |
| `Left` | Select the previous point on the active axis |
| `Ctrl+Left` | Add-select the previous point on the active axis |
| `Right` | Select the next point on the active axis |
| `Ctrl+Right` | Add-select the next point on the active axis |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |

## Beat grid editing

These shortcuts apply in the Beat grid timeline layer. `Unified` is read-only;
use `Audio` or `Beatbar` for selection and editing.

| Shortcut | Action |
| --- | --- |
| `Ctrl+A` | Select all visible markers on the active editable source tab |
| `B` | Add a beat at the playhead on Audio or Beatbar |
| `A` | Add an accent at the playhead on Audio only |
| `Delete` | Delete selected markers on Audio or Beatbar |
| `Left` | Select the previous marker on Audio or Beatbar |
| `Ctrl+Left` | Add-select the previous marker on Audio or Beatbar |
| `Right` | Select the next marker on Audio or Beatbar |
| `Ctrl+Right` | Add-select the next marker on Audio or Beatbar |

## Structure editing

These shortcuts apply with keyboard focus on `Structure` > `Meter boundary`.

| Shortcut | Action |
| --- | --- |
| `Enter` | Edit the selected confirmed region, or accept the selected proposal |
| `Delete` | Delete the selected region, remove a selected internal boundary, or reject the selected proposal |
| `Escape` | Cancel the meter editor or an active boundary/anchor drag |

## Timeline view

| Shortcut | Action |
| --- | --- |
| `Ctrl++` | Zoom in |
| `Ctrl+-` | Zoom out |
| `Ctrl+0` | Reset zoom |

These shortcuts keep the current playhead timestamp at the fixed timeline
center.
