# Beat Editing

Beat editing repairs the project beat grid after simple beat generation, audio
analysis, beatbar analysis, import, or manual edits. The beat grid drives
snapping, alignment, beatbar-assisted workflows, and motion generation timing.

## Beat grid layer

Beat commands work in the Beat grid timeline layer, separate from point
editing. Selecting one beat or accent seeks playback to that marker timestamp.
Selecting multiple markers changes only the beat selection.

The Beat grid layer has three source tabs:

- `Unified`: read-only resolved timing view with audio and beatbar evidence.
- `Audio`: editable audio beat grid.
- `Beatbar`: editable committed beatbar hits.

Markers have three common meanings:

- `Beat`: primary rhythm markers used for beat order and ordinary snapping.
- `Accent`: extra timing hints for offbeats, pickups, and fill moments.
- `Downbeat`: a compatibility flag projected from a confirmed measure start,
  or a marker-only value in an older map-free grid.

Confirmed measure starts are red and confirmed group starts have weaker
emphasis. Pending meter proposals are reviewed under `Structure` > `Meter
boundary`; they do not become downbeats until accepted. Accents do not become
downbeats.

## Add, select, and delete markers

Use:

- `B` or `Edit > Add beat at playhead` to add a beat at the playhead;
- `A` or `Edit > Add accent at playhead` to add an accent at the playhead;
- `Delete` to remove selected beat or accent markers.

Right-click the beat timeline for context commands. With no marker selected,
the menu offers location-aware add commands. With a marker selection, the menu
offers selection commands such as delete, toggle beat/accent, selection
filtering, midpoint insertion, and span repair entries. Direct downbeat toggles
remain available only for older map-free grids; confirmed meter maps are edited
under `Structure` > `Meter boundary`.

Committed beatbar hits are edited from the `Beatbar` tab. Use `Delete` for
false positives, or the same beat-repair timing commands used by Audio when
the command is not accent, downbeat, or measure-start specific.

Beat edits are undoable when they commit a change. Commands that make no project
change report no change instead of creating Undo entries.

On the Audio grid, Beat timing edits reconcile the structural pulse grid. Adding
a Beat can create or repair a pulse slot; at an exact Accent it promotes that
marker. Retiming or deleting a Beat retimes or removes any corresponding slot.
`Toggle Beat/Accent` changes only the marker classification.

A confirmed meter anchor does not lock the marker displayed at that timestamp.
Using `Toggle Beat/Accent` to convert the marker leaves the saved meter region
and any existing structural pulse slot in place. Deleting a Beat removes any
corresponding slot but keeps the saved region and explicit anchor. Retiming a
valid primary beat range also reconciles its meter anchors with the retimed
grid.

## Saved commands

After a supported command in the Beat editing pane changes the source grid,
use `Register last...` in `Saved commands` to name that operation and its
effective values. Expand the panel, then click anywhere on a saved row except
its trash button to run it against the currently selected editable source and
markers. It does not switch source tabs or copy values into the ordinary
controls.

Hover a row to review its saved values and current availability. Audio-only
commands remain disabled on the Beatbar source, frame-step commands require a
known frame rate, and selected-tempo fill requires an estimated BPM. The number
in the left drag handle is the row's current shortcut position. Drag that
numbered handle to reorder rows; the first 30 positions can be invoked from the
Beat grid timeline with the saved-command shortcuts listed in the Keyboard
Shortcuts guide. Use the trash button to remove a saved command. Saved commands
are user-level data and are not included in project or funscript files.

A saved `Set measure start` command keeps its primary pulse count, grouping,
and optional time signature. Running it applies that definition directly to the
one selected Audio beat or accent marker; it does not open the Beat editing pane
or the Meter editor. Older saved versions that contained only a beat count
reopen as one group of that size with notation left unknown.

## Advanced paste

Select beat or accent markers in the Beat grid layer and copy them with
`Ctrl+C`. In `Edit > Beat editing...`, use `Advanced paste` below Beat repair
to paste the copied marker pattern at the current timestamp.

- `Backward` uses the current timestamp as the pasted sequence end.
- `Mirroring backward` also uses the current timestamp as the end, but mirrors
  the copied timing.
- `Overwrite` controls whether markers at matching timestamps are replaced or
  skipped.
- `Repeat count` pastes consecutive copies of the copied pattern.

## Repair missing or extra beats

Use these commands when the analysis is close but needs local repair:

- `Insert midpoints`: add one marker between selected primary beats.
- `Fill selected span with beats`: add a typed number of evenly spaced beats
  inside two selected endpoints.
- `Fill from selected tempo`: project beats before or after the selected beat
  using the current estimated BPM.
- `Redistribute run`: keep selected run endpoints and space interior beats
  evenly.
- `Delete`: remove false-positive selected beat, accent, or committed beatbar
  hit markers.

Accent repair commands add timing hints without changing the primary beat
sequence. Use accent subdivisions or accent fills for rapid decoration moments,
then clear accents in a span when there are too many.

Beatbar hit markers support timing edits only, so accent, downbeat, and
measure-start commands are available only on the `Audio` tab. Beatbar fill from
selected tempo is available when an audio beat grid has an estimated BPM.

## Timing repair

Open `Edit > Beat editing...` or press `Ctrl+B` for settings-driven beat
editing commands.

The Timing section supports:

- fixed nudges such as `-10 ms`, `-5 ms`, `-1 ms`, `+1 ms`, `+5 ms`, and
  `+10 ms`;
- frame-step nudges when the loaded video frame rate is known;
- typed signed shifts in milliseconds;
- stretch controls for retiming a selected range.

Use nudges for small consistent offsets. Use stretch only when the selected
start and end markers are trustworthy and the interior timing needs retiming
across that span.

## Meter boundary tab

Choose the vertical `Structure` timeline layer and then the `Meter boundary`
top tab for all meter state and detailed meter editing. This tab uses the Audio
primary beats as a faint background grid; it does not duplicate meter state in
the Beat editing pane.

A confirmed meter is drawn as a region card from its start to end. The card
shows its time signature when known, or a description such as
`4 pulses (2+2), notation unknown`, together with origin, confidence, and pickup
state when space permits. Red lines mark measure starts, weaker lines mark group
starts, and ordinary pulses remain neutral. A selected region uses a stronger
border and hatch treatment.

The start and end edges are full-height resize grips, matching the direct
manipulation used by the Song regions. The first-complete-measure anchor has a
compact bottom grip, so it remains selectable when it shares a timestamp with
the start edge. A region may begin at the song boundary while its anchor occurs
later; the beats before that anchor are the pickup.

### Review meter proposals

A pending proposal appears as a distinct Suggested card with amber or gray
styling. Its proposed measure and group lines are projected across the complete
region as dashed lines. The card shows rank, pulse count, grouping, score, and
reason; additional algorithm detail is available in the timeline tooltip or
diagnostics.

Sections with ranked proposals show one Suggested card each. Sections that
could not produce a proposal remain in diagnostics but leave the editing
timeline blank for the user to fill. Use the viewport-fixed `Candidate n/N`
previous and next controls to compare up to three alternatives for the selected
section. Rejected proposals are skipped. Changing that section's displayed
alternative is session-only and does not add an Undo entry or alter the project.

Right-click a Suggested card to `Accept`, `Reject`, or `Edit and apply...` it.
Accepting it unchanged creates a confirmed detected region. Editing it first
creates a user-authored region instead. A pending proposal never changes
downbeats or motion generation. If `Accept` reports that the proposal no longer
has a complete structural pulse grid, rerun Audio analysis before accepting it
unchanged. After audio analysis, the app switches to `Structure` > `Meter
boundary` whenever any section still needs meter review, including a section
with no candidate card. Use `Set meter here...` or double-click a valid Audio
timeline position to define meter manually for a blank section. When every
section already has applied meter, the app switches to `Beat grid` > `Audio`.
Simple beat generation also switches to `Beat grid` > `Audio`.

### Add or edit a meter

Double-click a valid Audio timeline position in a region, or use its context
menu, to open the Meter editing rail immediately above the timeline. The rail
contains:

- primary pulses per measure, from `1` through `32`;
- a grouping whose positive parts must add to that pulse count, such as `2+2`,
  `3+3`, `3+2`, or `2+3`; and
- an optional notated numerator and denominator.

A new definition starts at `4` pulses, grouping `2+2`, with notation unknown.
Editing a confirmed region or proposal starts with its current values. Applying
the first definition in a song region begins the region at the song boundary
and uses the resolved timeline position as its first complete measure anchor.
Applying a later definition creates or updates meter from that position to the
next boundary or song end.

Right-click a confirmed card for `Edit meter...`, `Add meter change here...`,
`Set measure start here`, `Remove meter change`, or `Delete meter region`.
Right-click empty map space for `Set meter here...`; an older map-free grid also
offers the explicit action that creates a reviewable proposal from stable
legacy downbeats. Migration uses one group `[N]`, leaves notation unknown, and
never guesses a time signature on project load.

`Delete meter region` removes that meter overlay and its derived downbeat
display, but keeps the stored structural pulse evidence available for a later
meter definition.

With keyboard focus on `Meter boundary`, `Enter` edits a confirmed region or
accepts the selected proposal. `Delete` removes a selected region or internal
boundary, or rejects the selected proposal. `Escape` cancels the editing rail or
a drag. `Space` continues to control playback. Results, validation failures,
and warnings appear in the bottom status bar rather than in an operation pane.

### Move boundaries and anchors

Drag a confirmed region's start edge, end edge, shared boundary, or measure
anchor. Meter handles snap to saved pulse slots, resolvable logical pulse
positions, and Audio markers without requiring those markers to be classified
as Beat. When no timing candidate exists in the editable range, the requested
Audio timestamp is accepted directly. Edges also accept exact song endpoints
and an adjacent confirmed-region edge. The drag preview is a ghost only; the
project changes once, when the pointer is released. Dropping on the original
position is a no-op and creates no Undo entry.

An edge may expand or shrink through blank, candidate-free, rejected, or
Pending space up to the next confirmed region. Overlapped proposals are removed
by that explicit user edit. A shared internal boundary moves the end of the
preceding region and the start of the following region together. Analyzer-
derived pause boundaries do not lock editing. Actual song boundaries cannot be
crossed, although a region can shrink away from one, and a preserved user region
that already crosses a newly detected song boundary can be normalized back to
the anchor's song range.

Incomplete or ambiguous analysis does not reject an otherwise valid manual
meter edit. The region change and its Undo entry are saved, the existing pulse
evidence in that unresolved range is left untouched, and other regions can
still resolve normally. Until the grid is repaired or reanalyzed, repeated
measure lines and beat-aware generation may remain unavailable in that
unresolved part.

When separated regions with the same definition meet, the editor combines them
only when the structural pulse grid proves that their measure phase agrees. If
phase conflicts or cannot be proved, it leaves an explicit shared boundary;
removing that boundary is an authoritative user decision and extends the left
region regardless of the automatic phase judgment. Overlapping regions and
crossing adjacent anchors remain invalid.

Inside a confirmed region, setting a measure start preserves that region's
definition and creates an explicit anchor. Removing a meter change removes an
explicit boundary; a repeated red measure start derived from the region cannot
be removed independently. Direct marker-only downbeat editing remains only for
older map-free data. The explicit anchor does not lock the marker at that time:
`Toggle Beat/Accent` leaves any existing structural pulse slot unchanged.
Deleting a Beat removes any corresponding slot but keeps the meter region's
saved anchor. Add a Beat at the anchor later if you want to restore a missing
slot.

## Suggested beat repair workflow

1. Generate or import a beat grid.
2. Watch a short section and compare markers against the video.
3. Delete obvious false positives.
4. Add missed beats or accents at the playhead.
5. Use midpoint, fill, or selected-tempo repair for local gaps.
6. Nudge or stretch sections only after the marker count looks right.
7. Confirm meter regions and proposal phase before using beat-aware motion
   generation.

Good beat editing makes point editing faster. When point snapping feels wrong,
return to the beat grid and repair the timing source first.
