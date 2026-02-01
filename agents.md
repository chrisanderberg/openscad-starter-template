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
