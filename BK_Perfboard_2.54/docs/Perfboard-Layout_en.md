# Perfboard Layout

## Purpose

This document describes the use of the KiCad template
`BK_Perfboard_2.54` for planning and documenting circuits on 2.54 mm
perfboard.

The template is a planning tool. It does not prescribe a specific wiring
or soldering technique.

## Basic Concept

The physical perfboard is represented in KiCad by a virtual 2.54 mm hole
grid. Electrical connections are modeled using several copper layers so
that wiring on both sides of the board and wire jumpers can be
represented clearly and checked by the DRC.

## Layer Concept

  KiCad Layer   Name            Use
  ------------- --------------- -------------------------------------
  B.Cu          Bottom Wire     Preferred wiring on the solder side
  F.Cu          Top Wire        Wiring on the component side
  In1.Cu        Top Jumper      Wire jumpers on the component side
  In2.Cu        Bottom Jumper   Wire jumpers on the solder side

`B.Cu` is the preferred working layer and is selected by default in the
template.

The additional layers are a logical representation in KiCad. They do not
represent a physically multilayered perfboard.

## Grid

The default grid is 2.54 mm and corresponds to the standard perfboard
pitch.

Finer auxiliary grids may be used when required, especially:

-   1.27 mm
-   0.635 mm

Components and solder points should normally remain aligned with the
physical 2.54 mm hole grid.

## Virtual Hole Grid

The hole grid on `User.Drawings` is provided for visual orientation
only.

It is not an electrical element and has no connection to schematic nets.

Its appearance is intentionally subtle so that tracks, jumpers,
footprints, and nets remain clearly visible.

## Board Outline

The template uses a grid-aligned default board outline of approximately
120 x 80 mm.

The actual dimensions are:

`121.92 x 81.28 mm`

The `Edge.Cuts` pass through grid points. This allows the user to resize
the board easily in complete 2.54 mm grid increments.

Grid points intersected by the board edge are not considered usable
solder points.

## BK_Perf_SolderPoint

`BK_Perf_SolderPoint` represents an intentionally placed electrical
solder, junction, or transition point.

Typical uses include:

-   transitions between wire and jumper layers
-   defined termination points for wire jumpers
-   net branches
-   T-junctions for multiple connections belonging to the same net

Multiple connections of the same net may meet at one common SolderPoint.
Adjacent SolderPoints should be avoided when a single common junction
provides the same function.

SolderPoints should only be used where they correspond to a meaningful
physical solder, transition, or junction point.

## Layer Changes

A layer change represents a change in the physical wiring method or
board side.

A `BK_Perf_SolderPoint` may be used for an intentional transition.

The user should always consider how the connection will actually be
soldered on the physical board.

## Wiring on the Component Side

Wiring on the component side is possible, but mechanical access may be
limited.

This is particularly relevant for:

-   DIL sockets
-   microcontroller boards
-   plug-in modules
-   large capacitors
-   densely placed components

A direct wire connection at a component pin may therefore be difficult
or impossible.

The template does not prevent such connections. Evaluating practical
solderability remains the user's responsibility.

## Routing Recommendations

The following guidelines help create clear and practical perfboard
layouts:

1.  Prefer `B.Cu` for normal wiring.
2.  Keep wiring grid-oriented and easy to follow where practical.
3.  Use jumpers deliberately when crossings cannot reasonably be
    avoided.
4.  Use SolderPoints only for physical solder, transition, or junction
    points.
5.  Where practical, combine multiple connections of the same net at a
    common junction.
6.  On perfboard, a slightly longer but clearly traceable connection may
    be preferable to a shorter connection that is difficult to solder.
7.  Keep power and GND wiring clear and mechanically robust.

These are recommendations rather than mandatory design rules.

## ERC and Unused Pins

Intentionally unused symbol pins should be marked with a `No Connect`
marker in the schematic.

This documents that the pin is deliberately left open and allows ERC to
distinguish an intentional unused pin from an accidentally omitted
connection.

The ERC should preferably be completed with no errors or warnings before
PCB layout begins.

## DRC

DRC is also useful for validating the modeled electrical connections of
a perfboard design.

The target state for a completed layout is:

-   0 Errors
-   0 Warnings
-   0 Unconnected Items

A clean DRC confirms the consistency of the KiCad model. It does not
guarantee that every planned connection is mechanically accessible or
practical to solder on the physical perfboard.

## Recommended Workflow

1.  Create the schematic.
2.  Run ERC and resolve errors.
3.  Assign footprints.
4.  Update the PCB from the schematic.
5.  Place components on the 2.54 mm grid.
6.  Plan normal wiring primarily on `B.Cu`.
7.  Add jumpers and SolderPoints where required.
8.  Review the routing for practical solderability.
9.  Run DRC.
10. Before physical assembly, compare the final layout with the actual
    perfboard and components being used.

## Note

The template represents the planned perfboard wiring in KiCad. It cannot
determine whether a connection is mechanically accessible or practical
with the actual components, wire, and soldering techniques used.

That decision remains part of the physical assembly planning.
