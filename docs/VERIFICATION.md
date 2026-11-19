# Documentation verification — 2026-11-19

Reviewed the current repository files and historical README. No ANSYS solve or
mesh-convergence rerun was performed. This change aligns scope and evidence; it
does not generate new thermal/structural performance results.

Independent Python arithmetic check:
- Rotor energy: 30333.333333 J.
- Annular area per face: 0.027567476 m².
- Initial declining heat flux per face: 275082.617690 W/m².
- Integral over both faces and 4 seconds equals rotor energy within 1e-12 relative tolerance.

Checked: the accepted 114,520-node count is below 128,000 and belongs to the
historical mechanical case; the 623,036-node attempt is above the stated budget.
The final thermal mesh count remains an evidence gap rather than an invented value.

Changed files: README.md, docs/SCOPE_AND_MODEL_STATUS.md, docs/VERIFICATION.md.
