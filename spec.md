# Spec (OpenSCAD)

## Project
- Name: TBD
- Owner: TBD
- Date: TBD

## Goal
Describe what you're building and what "done" means.

## Units
- All dimensions are in millimeters (mm).

## Printer assumptions (edit per project)
- Nozzle: 0.4 mm
- Layer height: 0.2 mm
- Min wall thickness: 1.2 mm (≈3 perimeters)
- Typical clearance:
  - slip fit: 0.20–0.40 mm
  - press fit: 0.00–0.20 mm (printer/material dependent)

## Functional requirements
- TBD

## Constraints
- Support-free: yes/no
- Max overhang target: 45° (if support-free)
- Strength-critical directions: TBD
- Material: TBD (PLA/PETG/ABS/etc.)

## Public parameters (model API)
List parameters, defaults, and constraints.

Example:
- wall = 2.0 (>= 1.2)
- clearance = 0.30 (>= 0)
- fillet_r = 0 (>= 0; 0 disables rounding)
- $fn = 64 (surface quality)

## Acceptance criteria
- Key dimensions:
  - TBD
- Printability:
  - No zero-thickness walls
  - No intentional self-intersections
- Rendering:
  - Renders in OpenSCAD stable without errors
  - Avoids extremely slow operations by default
