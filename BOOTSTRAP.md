# BOOTSTRAP: OpenSCAD Starter Template (Cursor Agent) — kebab-case docs + snake_case scad

You are an agent operating in this repository folder.

## Task
Create the following files with EXACT contents shown below. Create any needed
directories. Do not invent additional files unless required by the tree.
Use UTF-8. Preserve newlines. Do not wrap lines unnecessarily.

## Naming conventions (repo-wide)
- Markdown files: kebab-case (e.g., `render-matrix.md`, `style-guide.md`).
- OpenSCAD files: snake_case (e.g., `cable_clip.scad`, `util.scad`).
- Exception: `models/_template.scad` keeps the leading underscore convention.

## File tree to create
- agents.md
- spec.md
- plan.md
- openscad-api.md
- style-guide.md
- deps.md
- .gitignore
- lib/
  - project/
    - README.md
    - util.scad
  - vendor/
    - README.md
- models/
  - README.md
  - _template.scad
- tests/
  - render-matrix.md
- exports/
  - README.md

---

## FILE: agents.md
```text
# agents.md (OpenSCAD Starter Template)

## Purpose
This repo is an OpenSCAD project template optimized for spec-driven development
and AI-assisted coding (e.g., Cursor). It aims to improve correctness and
printability without unnecessarily constraining solutions.

## Target environment
- OpenSCAD: most recent stable release (not nightly).
- Units: millimeters (mm) everywhere unless a file explicitly states otherwise.
- Coordinate system: Z up.

## Authority and change control (important)
- spec.md is user-authored and defines the "what".
- Do NOT modify spec.md unless the user explicitly instructs you to.
- If spec.md is missing details or contains conflicts:
  - ask targeted questions, OR
  - propose a change in chat, clearly labeled "PROPOSED SPEC CHANGE", and wait
    for approval before editing spec.md.
- plan.md and implementation files may be updated as needed to satisfy spec.md,
  but must remain consistent with spec.md.

## Workflow (spec-driven)
- Read spec.md first. If details are missing, ask targeted questions or propose
  reasonable defaults and label assumptions (in plan.md), without editing spec.md.
- Read plan.md next and implement in small, verifiable steps.
- Update plan.md if the implementation approach changes or if new steps are
  discovered during implementation.

## Non-exhaustive references
- You MAY use any OpenSCAD built-in available in stable releases.
- Repo docs (e.g., openscad-api.md) are a convenience index, NOT a complete spec.
- You MUST NOT invent built-ins or library APIs.
  - If unsure a feature exists in stable: implement a fallback using known
    primitives OR leave a short TODO describing what to verify.

## Example pattern
- Use models/_template.scad as the canonical example for:
  - parameter block layout
  - debug flag usage
  - importing lib/project modules via `use <...>`
  - keeping models/ as thin wrappers around reusable modules

## Modeling conventions
- Put public parameters at the top of each model file with brief comments.
- Prefer simple CSG: union/difference/intersection.
- Prefer 2D profiles + linear_extrude() for prismatic parts.
- Avoid polyhedron() unless necessary (manifold pitfalls).
- Avoid minkowski() unless explicitly requested (performance).
- Remember: trig functions use degrees in OpenSCAD.

## Reusability
- Put reusable modules in lib/project/.
- Keep models/ as thin wrappers that call library modules.

## Debug / verification
- When helpful, include `debug=false` parameter.
- When `debug=true`, you may show:
  - axes and/or reference rulers
  - highlighted critical features using `#`
  - temporary cross-sections (projection(cut=true) or difference cuts)

## Assumptions
- If you must proceed with missing info, record assumptions in plan.md under an
  "Assumptions" section.
- Do not backfill assumptions into spec.md without explicit approval.

## Deliverable checklist for a new part
- Parameters + defaults + comments
- Clear anchor/origin behavior (centered vs corner-based)
- Minimal, readable module structure
- A small set of render cases in tests/render-matrix.md
```

---

## FILE: spec.md
```text
# Spec (OpenSCAD)

## Project
- Name: TBD
- Owner: TBD
- Date: TBD

## Goal
Describe what you’re building and what “done” means.

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
```

---

## FILE: plan.md
```text
# Plan

1. Extract critical dimensions + tolerance stack-ups from spec.md.
2. Define public parameters + derived values.
3. Choose construction approach:
   - 2D profile + linear_extrude (preferred for prismatic parts), OR
   - primitive solids + transforms + CSG
4. Build positive geometry first (the “solid”).
5. Add cutouts (holes, pockets, relief) via difference().
6. Add optional features behind flags (labels, fillets/chamfers, variants).
7. Add debug helpers (axes, highlights, optional cross-section).
8. Validate with tests/render-matrix.md (edge cases + expected outcomes).
9. If reusable, move modules into lib/project/ and keep models thin.

## Assumptions
- (List any assumptions made due to missing spec detail.)
```

---

## FILE: openscad-api.md
```text
# OpenSCAD API Quick Index (Non-exhaustive)

This is a convenience index to reduce mistakes. It is NOT a complete language
reference. You may use any OpenSCAD built-in available in stable releases.

If you’re not sure a function/module exists in stable OpenSCAD:
- prefer a fallback with known primitives, and/or
- leave a TODO with what to verify.

## Core primitives
- cube(size = [x,y,z] | x, center = false)
- sphere(r = ..., d = ...)
- cylinder(h = ..., r = ..., d = ..., r1 = ..., r2 = ..., d1 = ..., d2 = ..., center = false)
- square(size = [x,y] | x, center = false)
- circle(r = ..., d = ...)
- polygon(points = [...], paths = [...])
- polyhedron(points = [...], faces = [...])  (use sparingly)
- text(text, size = ..., font = ..., halign = ..., valign = ..., spacing = ...)
- import("file.stl" | "file.dxf" | ...)

## Transforms
- translate([x,y,z]) { ... }
- rotate([x,y,z]) { ... }        // degrees
- scale([x,y,z]) { ... }
- resize([x,y,z], auto = [...]) { ... }
- mirror([x,y,z]) { ... }
- multmatrix(m) { ... }
- color([r,g,b,a] or "name") { ... }
- offset(r = ..., delta = ..., chamfer = false) { ... }  // 2D

## CSG and shape operations
- union() { ... }
- difference() { ... }
- intersection() { ... }
- hull() { ... }
- minkowski() { ... }            // expensive

## Extrusion / projection
- linear_extrude(height = ..., center = false, twist = ..., slices = ..., scale = ...)
- rotate_extrude(angle = ..., convexity = ...) { 2D shape }
- projection(cut = false) { 3D shape }

## Resolution controls
- $fn: fixed number of fragments
- $fa: minimum fragment angle (degrees)
- $fs: minimum fragment size (mm)
Rule of thumb: $fn overrides $fa/$fs.

## Language constructs
- module name(args) { ... }
- function name(args) = expr;
- let(a = ..., b = ...) expr_or_block
- for (i = [start:step:end]) ...
- if (cond) ... else ...
- children([idx]) inside modules

## include vs use
- include <file.scad> : textual include (can cause redefinitions)
- use <file.scad>     : imports only modules/functions (preferred for libraries)

## Frequent pitfalls (high value)
- Trig uses degrees (sin/cos/tan).
- Cylinder args: prefer d/d1/d2 OR r/r1/r2 consistently.
- Decide and document anchoring (centered vs corner-based).
- minkowski/hull can explode render time; avoid by default.
- polyhedron requires consistent face orientation and manifold geometry.

## Canonical patterns

### Difference with a through hole
```scad
difference() {
  cube([40, 20, 4], center=true);
  cylinder(d=3.2, h=10, center=true);
}
```

### 2D profile + linear_extrude
```scad
module plate(w=40, h=20, t=4) {
  linear_extrude(height=t, center=true)
    square([w, h], center=true);
}
```

### Debug highlight
```scad
#translate([0,0,5]) cube([10,10,10], center=true);
```
```

---

## FILE: style-guide.md
```text
# Style Guide (OpenSCAD Starter)

## File naming conventions (repo-wide)
- Markdown files: kebab-case (e.g., render-matrix.md, style-guide.md).
- OpenSCAD files: snake_case (e.g., cable_clip.scad, util.scad).
- Exception: models/_template.scad keeps the leading underscore convention.

## Naming (in code)
- Use snake_case for variables, parameters, functions, and modules.
- Suffixes:
  - *_d diameter, *_r radius, *_h height, *_w width, *_t thickness
- Modules: nouns (e.g., mount_plate()).
- Functions: value-returning names (e.g., hole_positions()).

## Units and orientation
- mm.
- Z up.
- Prefer centered geometry for reusable modules unless there’s a strong reason
  not to; always document anchor/origin behavior.

## Parameters
- Public parameters at top of file with brief comments.
- Derived values grouped under a "Derived" section or computed with let().
- If clamping invalid values, comment why.

## Performance defaults
- Reasonable $fn; expose if surface quality matters.
- Avoid expensive ops by default (minkowski, heavy hull usage).

## Debug conventions
- `debug=false` flag when useful.
- Use:
  - `#` to highlight
  - `%` to show transparent reference geometry
  - `*` to disable blocks during iteration
```

---

## FILE: deps.md
```text
# deps.md

This project may vendor third-party OpenSCAD libraries under `lib/vendor/`.

For each dependency, record:
- name + version/commit (or release tag)
- source URL
- license (if known)
- how to import it
- which modules/functions we use
- any local wrapper modules (if applicable)

## Dependencies
(None yet)

## Import conventions
- Prefer `use <...>` for libraries (avoid symbol collisions).
- Use `include <...>` only when a library requires it.
```

---

## FILE: .gitignore
```text
# ---- Exports / build artifacts ----
exports/
out/
dist/
build/
*.stl
*.3mf
*.amf
*.obj
*.off
*.dxf
*.svg
*.png
*.jpg
*.jpeg
*.gif
*.pdf

# ---- OpenSCAD / CAD temporary & backup files ----
*~
*.bak
*.backup
*.tmp
*.temp
*.autosave
*.orig

# If you sometimes export/manipulate meshes in other tools:
*.step
*.stp
*.iges
*.igs

# ---- Logs ----
*.log

# ---- OS cruft ----
.DS_Store
Thumbs.db

# ---- Editor / IDE ----
.vscode/
.idea/
*.swp
*.swo

# Cursor (commonly created)
.cursor/
.cursor-cache/

# ---- Node / Python / misc (only relevant if you add tooling later) ----
node_modules/
.env
.venv/
__pycache__/
```

---

## FILE: lib/project/README.md
```text
# lib/project

Put reusable project modules here.

Guidelines:
- Keep modules small and composable.
- Document anchor/origin behavior (centered vs corner-based).
- Prefer `use <...>` from models/ to avoid accidental symbol collisions.
```

---

## FILE: lib/vendor/README.md
```text
# lib/vendor

Vendored third-party libraries go here (optional).

When you add a library, record:
- name + version/commit
- source URL
- what you use it for
- how to import it (use/include)

Consider adding a `deps.md` at repo root when you start adding dependencies.
```

---

## FILE: lib/project/util.scad
```text
// lib/project/util.scad
// Minimal general-purpose helpers for OpenSCAD projects.
// Keep this small to avoid conflicts with external libraries.

// Clamp helper: returns x limited to [lo, hi].
function clamp(x, lo, hi) = min(max(x, lo), hi);

module debug_axes(len = 20, t = 0.8) {
  // X (red), Y (green), Z (blue), starting at origin extending +axis.
  color([1, 0, 0]) cube([len, t, t], center = false);
  color([0, 1, 0]) cube([t, len, t], center = false);
  color([0, 0, 1]) cube([t, t, len], center = false);
}

module through_hole(d, h, center = true) {
  cylinder(d = d, h = h, center = center);
}

// Subtractive union: through hole + counterbore near the "top" face.
// Intended usage: difference() { solid(); counterbore_hole(...); }
module counterbore_hole(through_d, bore_d, bore_h, h, center = true) {
  union() {
    cylinder(d = through_d, h = h, center = center);

    // Place counterbore at the positive-Z face if centered, else at top of part.
    translate([0, 0, center ? (h / 2 - bore_h / 2) : (h - bore_h)])
      cylinder(d = bore_d, h = bore_h, center = true);
  }
}

// Subtractive union: through hole + conical countersink near the "top" face.
module countersink_hole(through_d, sink_d, sink_h, h, center = true) {
  union() {
    cylinder(d = through_d, h = h, center = center);

    translate([0, 0, center ? (h / 2 - sink_h / 2) : (h - sink_h)])
      cylinder(d1 = sink_d, d2 = through_d, h = sink_h, center = true);
  }
}
```

---

## FILE: models/README.md
```text
# models

Top-level files that produce a renderable part live here.

Convention:
- Keep these thin wrappers.
- Import reusable modules from lib/project/ via `use <...>`.
- Put parameter block at the top with defaults for that model variant.
```

---

## FILE: models/_template.scad
```text
// models/_template.scad
// Starter model wrapper.
//
// How to use:
// - Copy this file to a new name (e.g., bracket.scad).
// - Edit the parameters and the `main()` module.
// - Keep reusable helpers in lib/project/.

use <../lib/project/util.scad>;

// ---------- Public parameters (mm) ----------
debug = false;

part_w = 40;
part_h = 20;
part_t = 4;

hole_d = 3.2; // e.g., clearance for M3
$fn = 64; // surface quality

// ---------- Model ----------
module main() {
  difference() {
    // Base plate
    cube([part_w, part_h, part_t], center = true);

    // Through hole at center
    through_hole(d = hole_d, h = part_t + 2, center = true);
  }

  if (debug) {
    // Show axes at origin
    debug_axes(len = 25, t = 0.8);

    // Highlight the nominal hole cylinder (visual check)
    #through_hole(d = hole_d, h = part_t + 2, center = true);
  }
}

main();
```

---

## FILE: tests/render-matrix.md
```text
# Render / Validation Matrix

Use this as a lightweight test plan. Add cases as the project evolves.

## General checks (every model)
- [ ] Renders without errors in OpenSCAD stable.
- [ ] No obviously zero-thickness walls.
- [ ] No unintended self-intersections.
- [ ] Parameter defaults render a sensible part.
- [ ] Debug mode (if present) doesn’t change the exported solid.

## Suggested parameter cases
1. Default parameters
   - Expected: clean render, correct overall size, key features present.

2. Minimum-ish values (edge case)
   - Reduce wall thickness to minimum allowed by spec.
   - Expected: still printable, no features collapse.

3. Maximum-ish values (stress case)
   - Increase overall dimensions.
   - Expected: performance still acceptable, no artifacts.

4. Clearance/tolerance sweep (if relevant)
   - clearance = 0.2 / 0.3 / 0.4
   - Expected: mating features adjust as intended.
```

---

## FILE: exports/README.md
```text
# exports

Put generated STLs/3MFs/renders here (optional).

Many people add this to .gitignore to avoid committing binary artifacts.
```

---

## Done criteria
- All files exist exactly as specified.
- Directories exist as specified.
- No extra files created.