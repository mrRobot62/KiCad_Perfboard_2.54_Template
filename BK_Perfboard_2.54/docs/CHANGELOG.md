# Changelog

All notable changes to the BK_Perfboard_2.54 template are documented in this file.

The format is based on Keep a Changelog and uses the categories
Added, Changed, Fixed, and Removed where applicable.

---

## [Unreleased]

### Added

- Added 2.54 mm virtual perfboard grid on `User.Drawings`.
- Added horizontal and vertical visual guide lines.
- Added grid-aligned default board outline.
- Added custom `BK_Perf_SolderPoint` footprint.
- Added dedicated logical layers for perfboard wiring:
  - `B.Cu` - Bottom Wire
  - `F.Cu` - Top Wire
  - `In1.Cu` - Top Jumper
  - `In2.Cu` - Bottom Jumper
- Added documentation in German and English:
  - `Perfboard-Layout_de.md`
  - `Perfboard-Layout_en.md`
- Added routing concept for representing physical wire connections and jumpers.
- Added support for intentional solder junctions and layer transitions using `BK_Perf_SolderPoint`.
- Added DRC-compatible modeling of perfboard wiring.
- Added example/test circuit with:
  - two 7-segment displays
  - two CD4033 decade counter/display drivers
  - Count, Reset, and Lamp Test push buttons
  - 5 V power connection

### Changed

- Set the default board size to a grid-aligned `121.92 x 81.28 mm`
  (approximately 120 x 80 mm).
- Board edges now pass through 2.54 mm grid points to simplify manual resizing
  and physical cutting of perfboard.
- Reduced virtual hole-grid line width for a less intrusive display.
- Reduced `User.Drawings` opacity to improve routing visibility.
- Virtual hole-grid objects are grouped to simplify handling and make accidental
  modification easier to detect.
- `B.Cu` is used as the preferred default wiring layer.
- Updated `BK_Perf_SolderPoint` to use a rounded rectangular pad shape for clear
  visual distinction from normal component pads.
- Refined the SolderPoint concept so one point can be used as a common junction
  for multiple connections of the same net.

### Fixed

- Resolved DRC issues caused by unsuitable SolderPoint geometry.
- Resolved footprint synchronization issues between the footprint library and PCB.
- Resolved ERC errors for intentionally unused pins by documenting them with
  `No Connect` markers.
- Verified the example circuit with:
  - 0 ERC errors
  - 0 ERC warnings
  - 0 DRC errors
  - 0 DRC warnings

---

## [0.1.0] - Initial Development

### Added

- Initial `BK_Perfboard_2.54` KiCad project template.
- Basic 2.54 mm perfboard representation.
- Initial project directory structure.
- Initial documentation structure.
- Initial custom footprint library.