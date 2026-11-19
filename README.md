# 240 mm ventilated brake rotor — CAD and transient thermal baseline

**Status: Phase 1–3A deliverables documented; coupled thermo-structural,
material trade-off, durability and optimisation phases remain planned.**

This is an independent CAE study in **ANSYS Workbench Student 2026 R1** of a
240 mm dual-plate ventilated rotor. It is a preliminary thermal baseline, not a
qualified brake design or a completed lightweight-material comparison.

## Completed scope and evidence level

| Phase | Delivered scope | Evidence / qualification |
|---|---|---|
| 1 | Vehicle/load-case definition and braking-energy calculations | 195 kg vehicle plus rider; 80 km/h to rest in 4 s |
| 2A | Preliminary material-selection rationale and dual-plate architecture | 240 mm OD, 150 mm friction-track ID; material choice is a proposal, not a completed alloy/composite trade-off |
| 2B | Circumferentially smeared braking heat-flux derivation | 70% front-brake allocation, 90% rotor heat partition, equal heat input to both faces |
| 2C | Thermal boundary-condition design basis | Distinguishes proposed cooling mechanisms from the simplified implemented model |
| 3A | CAD, mesh-development workflow and transient thermal output | Archived geometry, temperature, heat-flux and probe images; solver not rerun for this documentation correction |
| Later phases | Coupled structural response, material/geometry trade-offs, modal/fatigue and optimisation | Planned; no completed coupled thermal-stress or disc-warping result claimed |

An older exploratory **standalone mechanical** run is described in the project
history. Its 228 N·m load case is not a coupled thermo-structural result and is
not counted as completion of the planned structural validation programme.

## Design basis

| Parameter | Baseline |
|---|---:|
| Rotor outside diameter | 240 mm |
| Friction-track inside diameter | 150 mm |
| Friction plates / gap | 3 mm / 6 mm / 3 mm; 12 mm overall |
| Preliminary vane count | 24 |
| Total mass / initial speed | 195 kg / 80 km/h |
| Braking time | 4 s |
| Front energy fraction / rotor heat fraction | 0.70 / 0.90 |
| Rotor thermal energy | Approximately 30.33 kJ |
| Initial heat flux on **each** annular face | Approximately 275 kW/m², decreasing linearly to zero at 4 s |
| Implemented initial / ambient temperature | 22 °C |

The energy-preserving idealisation is

$$Q_r=0.9(0.7)\frac12m v_0^2,\quad A=\pi(r_o^2-r_i^2),\quad
q''(t)=\frac{Q_r}{A t_b}\left(1-\frac{t}{t_b}\right)$$

for $0\le t\le t_b$, with zero applied braking flux afterwards. Integrating
this flux over **two faces** and the stopping time returns $Q_r$.
It is not explicit pad contact, rotor rotation or a moving heat-source model.

## Student-license mesh budget

The workflow is adapted to a **128,000-node student-license budget**. Every model
release must record its actual node/element count and successful solver status.
The old **623,036-node** setup is over budget and is not a convergence-verified
student-model result. The documented **114,520-node / 75,119-element** accepted
mesh belongs to the historical standalone mechanical case; do not relabel it as
the final thermal mesh. A separately identifiable final thermal mesh manifest
and formal mesh/time-step convergence records remain to be supplied.

## Archived thermal outputs

The project notes report a peak near **52 °C at 1.94 s**, then approximately
33.117 °C at 10 s, 28.161 °C at 30 s and 26.512 °C at 60 s. These are reported
baseline simulation outputs, not independently reproduced or experimentally
validated temperatures.

- [Geometry](Geometry.png)
- [Temperature](Temprature.png)
- [Heat flux](heat%20flux.png)
- [Temperature probe](Temerature%20prob.png)
- [10 s](Temperature%20at%2010%20s.png), [30 s](Temperature%20at%2030%20s.png), [60 s](Temperature%20at%2060%20s.png)

## Implemented-model limits

Internal ventilation-surface convection, radiation, detailed hub heat transfer,
CFD airflow, explicit pad contact and rotor rotation were not included in the
reported baseline. Thermal-to-structural temperature transfer was attempted but
not completed. Thermal hoop stress, warping, fatigue life, validated mass savings
and cast-iron/composite optimisation are therefore not established.

The recommended AISI 420-type material and the historical default Structural
Steel assignment must be kept distinct. Record the actual thermal material data
with its temperature range before making material-specific performance claims.

## Project notes and next release

See [scope and model-status register](docs/SCOPE_AND_MODEL_STATUS.md) for the
remaining evidence and [documentation verification](docs/VERIFICATION.md).
The existing Phase 1–2C DOCX and thermal PDF are historical design-basis/draft
records; proposals in them are not evidence that every boundary condition was
implemented. The `.wbpj` file may require companion project files to reproduce.

Next: archive the final thermal mesh and inputs, verify energy balance and
mesh/time-step sensitivity, complete temperature transfer, then assess structural
response and material/geometry alternatives. A new solver run is required to
claim those phases complete.
