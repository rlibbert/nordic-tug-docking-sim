# Prop Walk

A physics-based docking simulator for a 32-foot single-screw Nordic Tug with a bow thruster. Bring her alongside a tight marina slip using a throttle, a rudder, and a bow thruster — no autopilot, no shortcuts.

**[Play it live](https://rlibbert.github.io/nordic-tug-docking-sim/)**

## Why this exists

Single-screw boat handling has a few quirks that don't show up in arcade boat games but matter a lot at the dock: the propeller doesn't just push straight, the rudder is useless without water moving past it, and a bow thruster runs out of authority the moment you're making any real way. This sim models those specifically, at the scale of a 32-foot hull, so the *behavior* is worth learning from even though the exact numbers are a reasonable approximation rather than a spec sheet.

## The physics

- **Prop walk** — the right-hand (clockwise) propeller drags the stern sideways as well as pushing the boat. In astern gear the stern walks to port, swinging the bow to starboard, most pronounced at low speed. A touch of ahead throttle walks it the other way, more gently.
- **Rudder** — only bites with water moving past it: the boat's own headway/sternway, or the wash from a burst of throttle. Dead in neutral, it does nothing.
- **Bow thruster** — pushes the bow independent of the rudder, but loses authority above roughly 2–3 knots as the hull's own speed overpowers it. A docking tool, not a steering one.
- **Throttle detents** — a single-lever control with the shift detent sitting just off neutral: a quick push clicks the transmission into gear at idle before the throttle really opens up.
- **Full 3-DOF motion** — surge, sway, and yaw with coupling terms, hull drag, added mass, and yaw damping tuned for an ~8,500 kg / 9.75 m displacement hull.
- **Wind** — calm, light breeze, or a gusty crosswind that leans on the bow's windage.
- **Collision detection** against the pilings and a moored neighbor boat, with a docking check that requires the boat stopped, centered, and aligned in the slip before it counts.

## Controls

| Action | Keyboard | Touch |
|---|---|---|
| Throttle ahead / astern | `W` / `S` or `↑` / `↓` | Ahead / Astern buttons |
| Throttle to neutral | `X` | Neutral button |
| Rudder port / starboard | `A` / `D` or `←` / `→` | Port / Stbd buttons |
| Center rudder | `C` | Ctr button |
| Bow thruster (hold) | `Q` / `E` | Port / Stbd thruster buttons |
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
