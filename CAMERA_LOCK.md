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
| 03 Asset Borrowing | 8.2, 1.7, 2.75 | 9.65, 1.0, 3.85 |
| 04 Maintenance | 5.2, 2.0, -4.8 | 8.5, 2.1, -7.2 |
| 05 Depreciation | -5.0, 2.0, 3.8 | -8, 1.6, 7.5 |
| 06 Monitoring | -4.0, 2.2, -3.5 | -9, 1.8, -7 |
| 07 Audit Trail | -10.5, 2.0, 0 | -14.8, 1.7, 0 |

## 2. Frozen camera movement

- `PerspectiveCamera(48, aspect, 0.1, 120)`, opening faces west.
- Scroll-progress mapping + smoothstep easing + quadratic blend on the
  shot-03→04 segment in `updateTargets()`.
- Damping in `tick()`: position 2.4, target 2.2, floating screen 4.0,
  plus smoothed scroll progress (camera 2.6, hero 4.5).
- Scroll listener drives targets; camera state must stay scroll-driven.

## 3. Frozen info-box (`.glass-card`) positioning

- Base: `.sec-left` bottom-left, `.sec-right` top-right, max-width 530px.
- Per-section overrides: `data-cam="1"` bottom-anchored (14vh);
  `data-cam="3"` centered; `data-cam="4"` centered
  on wide screens only; `data-cam="5"` vertically centered;
  `data-cam="6"` lowered (24vh) on wide, bottom-anchored on narrow.
- Do not resize, recolor, or relocate the box without the full re-check.

## 4. Change procedure (exceptions only)

1. Change one value at a time.
2. Reload, walk all 7 shots, confirm labels + zero console errors.
3. Project key subject anchors per shot; confirm no subject hides
   behind the info box and nothing crops unintentionally.
4. Update the table above to match the new approved values.

## 5. Authorized exceptions (2026-10-05, user-approved)

- Shot 02 endpoint restored to the verified baseline after unverified
  reframing attempts caused a regression. Table above matches the code.
- Shot 03 endpoint moved south-east toward the borrower scan interaction.
  `section[data-cam="2"]` card vertically centered on the right.
  All other endpoints remain frozen.
- `section[data-cam="1"]` card bottom-anchored (14vh) and
  `section[data-cam="5"]` card vertically centered, so boxes settle clear
  of the header and complete together with the camera. All other
  per-section positioning in §3 remains frozen.
- Global card typography scale and kicker badge restyle apply to all
  feature cards. Card palette, radius, and glass treatment unchanged.
- Asset Management menu entry (`gotoSection(1)`) scrolls to the exact
  locked scrolling endpoint progress instead of generic section
  centering. Scroll mapping, endpoint, path, and easing untouched.

## 6. Agent safety rule (mandatory for all future work)

Distinguish camera MOVEMENT (easing, lerp, smoothness, duration,
sensitivity — behavior) from camera ENDPOINT (final position, target,
rotation, destination — locked).

If a request asks to move, shift, retarget, or reframe a camera in a
way that would change any locked endpoint — or is ambiguous about it —
DO NOT apply it directly. Warn the user that it touches a locked
endpoint, name the shot, and wait for explicit confirmation. Never
treat such a request as implicit approval. A movement change that
shifts an endpoint counts as an endpoint change.

## 7. Responsive camera tables (tablet / mobile)

- Desktop table (`SHOTS_DESKTOP`) is LOCKED per §1. Byte-identical values.
- `SHOTS_TABLET` (768–1023px, FOV 52) and `SHOTS_MOBILE` (<768px,
  FOV 60) are dedicated per-tier compositions aimed at each feature's
  focal objects. Same order, count, scroll mapping, timing, and labels.
- Tier switches only swap the active table + FOV on resize; scroll and
  animation systems are shared. Desktop behavior is only reachable and
  only used at >= 1024px, never modified by responsive code.
- Mobile motion principle: horizontal/depth-first dolly. Endpoints keep
  the desktop route shape (same view directions, ~85% distance) with
  retargeted centers, so transitions stay smooth without orbit feel.
  Mobile overview is a wide establishing shot; borrowing is shot from
  the north (employee front view) so the tablet/QR/laptop stay visible;
  Asset Management faces due west for a frontal asset-panel read.
