# Anonymous Rebuttal Figure Assets

This repository contains the Chevrolet Silverado figures used for the anonymous
cross-solver validation response. The comparison uses the detailed 2007
Chevrolet Silverado CCSA V3e model under a matched nominal 35 mph full-frontal
rigid-wall impact in OpenRadioss and Ansys LS-DYNA.

## Contents

- `silverado/deformation/`: matched deformation views and timestep sheets.
- `silverado/history/`: force, acceleration, and global-energy comparisons.

The main paper-ready assets are:

- `silverado/deformation/openradioss_vs_lsdyna_iso_front_right_still.png`
- `silverado/deformation/openradioss_vs_lsdyna_underbody_still.png`
- `silverado/deformation/openradioss_vs_lsdyna_side_still.png`
- `silverado/history/silverado_solver_history_comparison.png`
- `silverado/history/energy_overlay.png`

## Comparison Notes

- The LS-DYNA force is the direct frontal rigid-wall reaction from `rwforc`.
- The translated OpenRadioss deck does not retain an unambiguous direct frontal
  wall channel, so its comparison force is the momentum-equivalent longitudinal
  force derived from the global momentum history.
- Force and acceleration histories use the same phaseless CFC60 filter and are
  compared on their native time axes without onset shifting.
- The energy figure includes kinetic, internal, contact, hourglass, and display
  total histories. The display total is calculated identically for both solvers
  as kinetic + internal + contact + hourglass energy. This avoids comparing the
  native LS-DYNA total, which additionally includes rigid-wall work, against an
  OpenRadioss component sum.

These results constitute a matched solver-to-solver verification case, not a
replacement for experimental validation or regulatory certification.
