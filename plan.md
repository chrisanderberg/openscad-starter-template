# Plan

1. Extract critical dimensions + tolerance stack-ups from spec.md.
2. Define public parameters + derived values.
3. Choose construction approach:
   - 2D profile + linear_extrude (preferred for prismatic parts), OR
   - primitive solids + transforms + CSG
4. Build positive geometry first (the "solid").
5. Add cutouts (holes, pockets, relief) via difference().
6. Add optional features behind flags (labels, fillets/chamfers, variants).
7. Add debug helpers (axes, highlights, optional cross-section).
8. Validate with tests/render-matrix.md (edge cases + expected outcomes).
9. If reusable, move modules into lib/project/ and keep models thin.

## Assumptions
- (List any assumptions made due to missing spec detail.)
