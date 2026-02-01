# OpenSCAD Starter Template

An **OpenSCAD starter template** for 3D models and prints: spec-driven, AI-friendly, with millimeters (mm) and Z-up everywhere.

## Using this template

**If you use [BOOTSTRAP.md](BOOTSTRAP.md) to generate the project structure yourself**

- The bootstrap creates the file tree (agents.md, spec.md, lib/, models/, etc.) but does **not** create a root README.md or LICENSE.
- You must add your **own** README.md and LICENSE for your project.

**If you clone this repo**

- You get this README and the current LICENSE (MIT, per [LICENSE](LICENSE)).
- You should **replace** both the root README.md and LICENSE with your own (project name, copyright holder, and license choice).

## Vendored libraries and licensing

The template includes a `lib/vendor/` area for third-party OpenSCAD libraries (see [BOOTSTRAP.md](BOOTSTRAP.md) and [lib/vendor/README.md](lib/vendor/README.md)). **Adding vendored libraries to the repo can restrict which license is appropriate** for the overall project (e.g. GPL/AGPL vs MIT). Check each vendored library’s license and, if needed, choose or adjust your project’s LICENSE accordingly.

## Project layout

See [BOOTSTRAP.md](BOOTSTRAP.md) for the full file tree. Key directories: `lib/project/`, `lib/vendor/`, `models/`, `tests/`, `exports/`.

## Getting started

Put your requirements in spec.md, use agents.md for AI/agent context, and implement under lib/project/ and models/.
