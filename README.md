# Stair-Climbing Robot

A legged walking mechanism for automating agricultural work on terraced and stepped terrain, where wheeled and tracked machines cannot operate.

## Motivation

Terraced and mountain farming supports communities growing grains, potatoes, fruit and coffee, but it remains largely manual because tractors cannot handle steps and steep slopes. Legged robots can. This project develops a one-tenth-scale legged robot in two phases:

- **Phase 1:** hand-cranked walking mechanism that advances a stepped rack (complete)
- **Phase 2:** self-contained motorised robot that climbs steps and performs a secondary farming task (in progress)

---

# Phase 1: Hand-Cranked Walking Mechanism

## Goal

Design a stationary legged mechanism that, when its crank is turned continuously, advances a spring-loaded stepped rack, simulating a robot walking up stairs. The rack slides back when unsupported, as a robot would fall down the steps.

## Test Rack

| Top view | Side view | Front view |
|---|---|---|
| ![Top view](media/phase1/rack/rack_top_view.png) | ![Side view](media/phase1/rack/rack_side_view.png) | ![Front view](media/phase1/rack/rack_front_view.png) |

| Parameter | Value |
|---|---|
| Step rise | 3.7 ± 0.3 cm |
| Step run | 8 ± 0.5 cm |
| Rack tread width | 10 cm |
| Bias | Spring returns the rack backward when free |

## Requirements

1. Advance the rack continuously while the crank is turned
2. Prevent the rack from sliding back between steps
3. Generate at least 2 N of horizontal force against the return spring
4. Driven by a single hand crank, with no other input power

## Constraints

- Remain within a 24 × 24 × 24 cm envelope at all times, including swept motion
- Clamp to the table beside the rack without touching the rack or its frame
- No simple machines operating in isolation; no Jansen or Klann linkages
- Safe: no fast-moving or sharp components
- $60 budget

## Design

### Linkage

<img src="media/phase1/kinematics/coupler_curve.png" alt="Coupler curve simulation" width="450">

- Crank-rocker four-bar leg (Grashof), with the foot on an extension of the coupler
- Link lengths: ground 50.7 mm, crank 18.7 mm, coupler 48.5 mm, rocker 39.6 mm
- Stride matched to the 88.1 mm step pitch; O2 and O4 pivots 153 mm above the table
- Two legs 180° out of phase, so one foot always holds the rack while the other returns
- Linkage definition: [`kinematics/phase1/four_bar_leg_mechanism_generator.json`](kinematics/phase1/four_bar_leg_mechanism_generator.json), loadable in the Fusion 360 Mechanism Generator add-in to reproduce the foot path

### Frame and Assembly

| Full assembly | Frame |
|---|---|
| ![CAD assembly](media/phase1/cad/cad_full_assembly.png) | ![Frame assembly](media/phase1/cad/cad_frame_assembly.png) |

- Two-sided frame with a centrally supported crankshaft, removing the shaft-leg interference of a one-sided layout
- Stepped frame walls that clear the rack's side walls while keeping the legs close together
- Stainless barrel-fastener pivots, with spacers to remove axial play
- 15 mm thick legs for out-of-plane stiffness
- Crank links printed with integral rods to eliminate a toleranced fit

## Development

| Single-leg 3D-printed prototype | Final two-leg build |
|---|---|
| ![Mid-fidelity prototype](media/phase1/prototypes/prototype_mid_fidelity.png) | ![Final build](media/phase1/prototypes/prototype_final.png) |

Process: cardboard linkage prototypes → coupler-curve simulation → single-leg 3D-printed prototype → two-leg CAD iterations → final PLA build.

## Result

Clamped beside the rack, the prototype advanced it continuously under continuous cranking, with the two legs holding it against the spring between steps.





https://github.com/user-attachments/assets/4bd6b3c3-c30c-40ae-a99a-c7ab61f77248





---

# Phase 2: Motorised Robot (In Progress)

## Goal

A self-contained, battery-powered legged robot that climbs a series of steps itself while performing a synchronised secondary agricultural task.

## Planned Approach

- Carry the Phase 1 linkage forward as the robot's legs, adding leg pairs at different phases for stability under the robot's own weight
- Replace the hand crank with a motor driving the same crankshaft
- Drive the secondary task from that crankshaft so it stays synchronised with walking

---

## Repository Structure

Each top-level folder is split into `phase1/` and `phase2/`; Phase 2 folders will fill as that work progresses.

```
cad/phase1/
  frame/        table legs, linkage plates and top plate
  linkage/      cranks, couplers, rockers and handle
  hardware/     barrel fasteners, screws and spacers
kinematics/phase1/
  four_bar_leg_mechanism_generator.json
media/phase1/
  rack/         test rack drawings
  cad/          CAD renders
  kinematics/   coupler curve
  prototypes/   prototype photos
  video/        rack test video
reports/phase1/
  written_report_1.pdf
  written_report_2.pdf
```

## Phase 1 Parts

All parts are Fusion 360 (.f3d) files in `cad/phase1/`.

**Printed parts (PLA)**

| Part | File | Qty |
|---|---|---|
| Frame leg (L-shaped base, clamps to table) | `frame/frame_leg.f3d` | 2 |
| Linkage plate, crank side (bearing for handle-side crank) | `frame/frame_plate_crank_side.f3d` | 1 |
| Linkage plate, non-crank side | `frame/frame_plate_non_crank_side.f3d` | 1 |
| Top plate with centre crank support | `frame/frame_top_plate.f3d` | 1 |
| Outer crank with handle extrusion (O2 to A) | `linkage/crank_outer_handle_side.f3d` | 1 |
| Outer crank (O2 to A) | `linkage/crank_outer.f3d` | 1 |
| Inner crank | `linkage/crank_inner.f3d` | 2 |
| Inner crank connector | `linkage/crank_inner_connector.f3d` | 1 |
| Leg (coupler) | `linkage/coupler_leg.f3d` | 2 |
| Rocker | `linkage/rocker.f3d` | 2 |
| Handle | `linkage/handle.f3d` | 1 |

**Printed spacers (PLA)**

| Part | File |
|---|---|
| Spacer, 1.5 mm | `hardware/spacer_1p5mm.f3d` |
| Spacer, crank (×1) | `hardware/spacer_crank.f3d` |
| Spacer, barrel fastener (×5) | `hardware/spacer_barrel_fastener.f3d` |
| Spacer, square rod 4 mm (×2) | `hardware/spacer_square_rod_4mm.f3d` |
| Spacer, square rod 8 mm | `hardware/spacer_square_rod_8mm.f3d` |

**Hardware (stainless barrel fasteners and screws; models included for fit checks)**

| Part | File |
|---|---|
| Barrel fastener, 25 mm | `hardware/barrel_fastener_25mm.f3d` |
| Barrel fastener, 30 mm | `hardware/barrel_fastener_30mm.f3d` |
| Screws | `hardware/screws.f3d` |

## Team

Daksh Bhaskar, Kashvi Kunder, Will Garber, Kavish Mistry
