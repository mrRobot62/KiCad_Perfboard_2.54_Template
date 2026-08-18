# Changelog

All notable changes to `BK_Perfboard_2.54` are documented in this file.

The structure follows the principles of Keep a Changelog.

## \[1.0.0\] - 2026-08-18

### Added

-   Initial KiCad 10 template for planning 2.54 mm perfboard projects.
-   Virtual 2.54 mm perfboard hole grid on `User.Drawings`.
-   Subtle visual grid presentation for improved routing readability.
-   Grid-aligned default board outline of `121.92 x 81.28 mm`.
-   Dedicated logical wiring layers:
    -   `B.Cu` - Bottom Wire
    -   `F.Cu` - Top Wire
    -   `In1.Cu` - Top Jumper
    -   `In2.Cu` - Bottom Jumper
-   `B.Cu` as the preferred/default working layer.
-   Custom `BK_Perf_SolderPoint` footprint for intentional solder,
    junction, and layer-transition points.
-   Rounded rectangular SolderPoint shape for clear visual distinction
    from ordinary component pads.
-   Support for common junctions and T-connections using a single
    SolderPoint.
-   Project-local footprint library.
-   German and English usage documentation:
    -   `docs/Perfboard-Layout_de.md`
    -   `docs/Perfboard-Layout_en.md`
-   English template information file for the KiCad template browser.
-   Repository README prepared for screenshots stored under `assets/`.

### Changed

-   Refined the virtual perfboard grid to reduce visual interference
    with routing.
-   Set `User.Drawings` to a reduced-opacity presentation.
-   Grouped the virtual perfboard grid objects to simplify handling and
    make accidental modification easier to detect.
-   Kept the visual grid editable instead of locking it, avoiding
    KiCad's intrusive locked-object display.
-   Aligned `Edge.Cuts` directly with 2.54 mm grid points to simplify
    board resizing and physical cutting.
-   Refined the SolderPoint concept from a generic free pad to an
    explicit electrical junction/transition point.
-   Established a routing philosophy favoring clear, practical,
    solderable wiring over purely shortest-path routing.
-   Kept `F.Silkscreen` available for component references and placement
    information.

### Validated

-   Verified ERC handling of intentionally unused pins using KiCad
    `No Connect` markers.
-   Verified routing between Bottom Wire and jumper layers through
    `BK_Perf_SolderPoint`.
-   Verified common-net T-junction routing using a single SolderPoint.
-   Verified DRC behavior for routed perfboard connections.
-   Validated the template with a two-digit CD4033 / 7-segment counter
    example.
-   Completed the validation example with:
    -   0 ERC errors
    -   0 ERC warnings
    -   0 DRC violations
    -   0 unconnected items

### Known Limitations

-   KiCad models through-hole objects as physical PCB features. A
    SolderPoint can therefore restrict routing at the same XY position
    on other logical layers even when an insulated wire could physically
    pass over that location on a real perfboard.
-   The template cannot determine whether component-side wiring is
    mechanically accessible around sockets, modules, capacitors, or
    other components.
-   DRC validates the KiCad model but does not replace a final
    real-world solderability review.
