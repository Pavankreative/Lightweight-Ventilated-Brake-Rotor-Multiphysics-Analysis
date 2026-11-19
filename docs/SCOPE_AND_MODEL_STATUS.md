# Scope and model-status register

Updated 2026-11-19. This register supersedes broad completion language in the
[historical README](https://github.com/Pavankreative/Lightweight-Ventilated-Brake-Rotor-Multiphysics-Analysis/blob/c527dc96f771913208e2f74f03da41e74943e93e/README.md).

| Item | Current interpretation | Required close-out |
|---|---|---|
| Phases 1–2C | Completed design basis; includes proposed physics | Separate proposals from implemented loads/materials |
| Phase 3A | CAD and archived transient-thermal output | Publish final model/mesh manifest and solver logs |
| 128k-node budget | Constraint for the student workflow | Record actual thermal model node/element counts |
| 623,036-node mesh | Over-budget historical attempt | Never cite as successful convergence evidence |
| 114,520-node mesh | Historical mechanical-only run | Do not reuse as thermal mesh metadata |
| Thermal transfer | Attempted, not completed | Successful temperature mapping and equilibrium checks |
| Static mechanical case | Historical exploratory baseline | Review loads/supports/materials and convergence |
| Material comparison | Rationale exists; numerical trade-off pending | Traceable temperature-dependent datasets and matched cases |
| Vane cooling / radiation / hub sink | Proposed; omitted in implemented baseline | Add only with stated physical justification |
| Mass reduction / durability | Not demonstrated | Baseline comparison, fatigue inputs and validation |

Reported mechanical-only values (3.135 MPa equivalent stress; 0.000914 mm
deflection under 228 N·m) are retained as historical results, not as thermal
stress, warping or production safety evidence. No solver outputs were changed.
