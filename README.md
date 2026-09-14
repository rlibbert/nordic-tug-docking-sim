# Prop Walk

A physics-based docking simulator for a single-screw Nordic Tug. Bring her alongside a tight marina slip using a throttle, a rudder, and one or two thrusters — no autopilot, no shortcuts.

**[Play it live](https://rlibbert.github.io/nordic-tug-docking-sim/)**

## Why this exists

Single-screw boat handling has a few quirks that don't show up in arcade boat games but matter a lot at the dock: the propeller doesn't just push straight, the rudder is useless without water moving past it, and a thruster runs out of authority the moment you're making any real way. This sim models those specifically, at the scale of a real hull, so the *behavior* is worth learning from even though the exact numbers are a reasonable approximation rather than a spec sheet.

## Vessels

| | Nordic Tug 34 | Nordic Tug 44 |
|---|---|---|
| Thrusters | Bow only | Bow **and** stern |
| Character | Lighter, quicker to turn | Heavier, more power, more momentum to manage |
| Marina | Same layout, scaled to fit the hull | Same layout, scaled to fit the hull |

The 44's stern thruster is the headline difference: push the bow one way and the stern the other and she pivots almost in place, something the 34 can't do with a bow thruster alone. Switching vessels mid-session resets the current approach.

## The physics

- **Prop walk** — the right-hand (clockwise) propeller drags the stern sideways as well as pushing the boat. In astern gear the stern walks to port, swinging the bow to starboard, most pronounced at low speed. A touch of ahead throttle walks it the other way, more gently.
- **Rudder** — only bites with water moving past it: the boat's own headway/sternway, or the wash from a burst of throttle. Dead in neutral, it does nothing.
- **Bow (and stern, on the 44) thruster** — pushes the hull sideways independent of the rudder, but loses authority above roughly 2–3 knots as the hull's own speed overpowers it. A docking tool, not a steering one.
- **Throttle detents** — a single-lever control with the shift detent sitting just off neutral: a quick push clicks the transmission into gear at idle before the throttle really opens up.
- **Full 3-DOF motion** — surge, sway, and yaw with coupling terms, hull drag, added mass, and yaw damping, tuned separately for each hull's mass and length.
- **Wind** — calm, light breeze, or a gusty crosswind that leans on the bow's windage.
- **Collision detection** against the pilings and a moored neighbor boat, with a docking check that requires the boat stopped, centered, and aligned in the slip before it counts.

## Controls

| Action | Keyboard | Touch |
|---|---|---|
| Throttle ahead / astern | `W` / `S` or `↑` / `↓` | Ahead / Astern buttons |
| Throttle to neutral | `X` | Neutral button |
| Rudder port / starboard | `A` / `D` or `←` / `→` | Port / Stbd buttons |
| Center rudder | `Space` | Ctr button |
| Bow thruster (hold) | `Q` / `E` | Port / Stbd thruster buttons |
| Stern thruster (hold, Tug 44 only) | `Z` / `C` | Port / Stbd thruster buttons |
| Reset approach | `R` | Reset button |

Each attempt starts from a random position and heading in the open water, so there's no single approach to memorize.

## Running it locally

It's a single self-contained HTML file — no build step, no dependencies.

```bash
open index.html
```

or serve it if your browser is picky about local file access:

```bash
python3 -m http.server 8000
```

then visit `http://localhost:8000/`.

## License

[MIT](LICENSE)
