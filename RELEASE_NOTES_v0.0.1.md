North v0.0.1

Overview
--------
This release introduces a redesigned Pebble watchface focused on compass-style navigation and a simplified visual language.

Key Features
------------
- Preserved center circle: The visual center circle is retained as a primary design element and visual anchor.
- Heading-driven hour pointer: The existing hour-hand artwork now acts as a heading pointer driven by the device compass (magnetic heading), showing orientation rather than local hour when enabled.
- Compass markers: Outer hour/minute markers were replaced with 16 compass points (N, NNE, NE, ... NNW) evenly spaced around the dial.
- Removed minute & second hands: Minute and second hands removed from the primary view to emphasize the heading pointer and reduce visual clutter.
- Conditional seconds support: Seconds-layer work remains in the codebase but is disabled by default in this design; settings still support seconds visibility/timeouts.
- Font & resource compatibility: The DIN condensed font (`DIN_CONDENSED_FFONT`) is included for all platforms; BT/Qt icon font selection is conditional for platform compatibility.

Implementation Notes
--------------------
- The compass integration uses the Pebble compass service; the heading value is exposed as `s_heading` and used to rotate the hour-hand graphic.
- The main drawing logic is in `src/c/North.c` (hour-hand drawing, center circle, tick rendering). Secondary source `src/c/NorthToo.c` is retained but excluded from the main build by `wscript`.
- Vector text rendering uses `pebble-fctx` with the embedded `DINPro-CondensedMedium.ffont` resource.
- Build fixes: `wscript` was updated to exclude `NorthToo.c` from the app source list; `.gitignore` updated to ignore Waf lock files.

User-visible Behavior
---------------------
- On devices with a compass, the hour-hand graphic will point toward magnetic heading; the center time text remains for time reading.
- The watchface keeps a clean, minimalist look aimed at navigation and orientation use-cases.

Files of interest
-----------------
- `src/c/North.c` — main watchface implementation and UI updates
- `wscript` — build exclusion of `src/c/NorthToo.c`
- `package.json` — resource declarations and message keys

Notes & Future Work
-------------------
- Optionally expose a setting to toggle the heading-driven mode vs. traditional time-driven hour-hand.
- Consider adding an on-screen compass label toggle (show/hide the 16-point labels) to reduce clutter on smaller displays.
- Add a signed tag and GitHub release (this release is published as `v0.0.1`).

Acknowledgements
----------------
- Thanks to the Pebble SDK and the `pebble-fctx` project for vector font rendering support.
