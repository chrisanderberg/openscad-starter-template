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
