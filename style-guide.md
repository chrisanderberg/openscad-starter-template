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
- Prefer centered geometry for reusable modules unless there's a strong reason
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
