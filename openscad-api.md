# OpenSCAD API Quick Index (Non-exhaustive)

This is a convenience index to reduce mistakes. It is NOT a complete language
reference. You may use any OpenSCAD built-in available in stable releases.

If you're not sure a function/module exists in stable OpenSCAD:
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
