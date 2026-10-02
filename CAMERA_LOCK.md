# CAMERA LOCK — Assetrack Motion

Status: **FROZEN**. Final camera endpoints, camera movement, and info-box
positioning were approved after per-shot verification on wide (1520×856)
and square (1062×718) viewports.

Rule: scene objects and UI must adapt to the camera, never the reverse.
Any change to the items below requires re-verifying all 7 shots on both
aspect ratios (labels, console, subject-vs-card projection) before merging.

## 1. Frozen camera endpoints (`shots` array)

| Shot | Position (x, y, z) | Target (tx, ty, tz) |
|------|--------------------|---------------------|
| 01 Overview | 13.2, 3.5, 1.0 | -3, 1.0, 1.0 |
| 02 Asset Management | 8.8, 1.9, 6.3 | 6.3, 1.05, 7.0 |
| 03 Asset Borrowing | 7.9, 1.75, 1.9 | 9.55, 0.9, 3.35 |
| 04 Maintenance | 5.2, 2.0, -4.8 | 8.5, 2.1, -7.2 |
| 05 Depreciation | -5.0, 2.0, 3.8 | -8, 1.6, 7.5 |
| 06 Monitoring | -4.0, 2.2, -3.5 | -9, 1.8, -7 |
| 07 Audit Trail | -10.5, 2.0, 0 | -14.8, 1.7, 0 |

## 2. Frozen camera movement

- `PerspectiveCamera(48, aspect, 0.1, 220)`, opening faces west.
- Scroll-progress mapping + smoothstep easing + quadratic blend on the
  shot-03→04 segment in `updateTargets()`.
- Damping in `tick()`: position 3.2, target 3.0, floating screen 4.0.
- Scroll listener drives targets; camera state must stay scroll-driven.

## 3. Frozen info-box (`.glass-card`) positioning

- Base: `.sec-left` bottom-left, `.sec-right` top-right, max-width 530px.
- Per-section overrides: `data-cam="3"` centered; `data-cam="4"` centered
  on wide screens only; `data-cam="5"` top on narrow screens only;
  `data-cam="6"` lowered (24vh) on wide, bottom-anchored on narrow.
- Do not resize, recolor, or relocate the box without the full re-check.

## 4. Change procedure (exceptions only)

1. Change one value at a time.
2. Reload, walk all 7 shots, confirm labels + zero console errors.
3. Project key subject anchors per shot; confirm no subject hides
   behind the info box and nothing crops unintentionally.
4. Update the table above to match the new approved values.
