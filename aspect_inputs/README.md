# ASPECT input files for the annulus benchmark

These are the ASPECT parameter files (`.prm`) for the twelve benchmark runs of the
paper (Ra = 10^4 to 10^9, free-slip and zero-slip boundary conditions), as run.
Together with the GTXLBM inputs in this repository they allow both sides of the
benchmark to be reproduced.

## ASPECT version

All runs used the official ASPECT Docker image `geodynamics/aspect:latest`,
which at the time of the runs contained ASPECT 3.1.0-pre (main branch, commit
`ac19c42d2`) built with deal.II 9.6.0. ASPECT is open-source software hosted by
the Computational Infrastructure for Geodynamics: https://aspect.geodynamics.org

## Files

| File | BC | Ra |
|------|----|----|
| `aspect_zeroslip_Ra1e4.prm` ... `aspect_zeroslip_Ra1e9.prm` | zero-slip top/bottom | 10^4 ... 10^9 |
| `aspect_freeslip_Ra1e4.prm` ... `aspect_freeslip_Ra1e9.prm` | free-slip top/bottom | 10^4 ... 10^9 |

The side boundaries at 45 and 135 degrees are free-slip (tangential) in all runs.
The domain is ASPECT's `chunk` geometry (quarter annulus) with Earth-like radii
(r_outer = 6378 km, r_inner = 3478 km) and physical parameters matching the GTXLBM
runs (rho = 4500 kg/m^3, eta = 2.8e22 Pa s, kappa = 1e-6 m^2/s, alpha = 3e-5 1/K,
dT = 3400 K). The Rayleigh number is set through the gravitational acceleration,
g = 0.025 x 10^(n-4) m/s^2 for Ra = 10^n.

## Running

The runs were launched through Docker, for example:

```
docker run --rm \
  -v "$(pwd)":/home/aspect/work \
  --workdir /home/aspect/work \
  geodynamics/aspect:latest \
  mpirun -np <N> aspect aspect_freeslip_Ra1e6.prm > aspect.log 2>&1 &
```

With a native ASPECT installation the equivalent is
`mpirun -np <N> aspect aspect_freeslip_Ra1e6.prm`.

Checkpointing is enabled (`Resume computation = auto`), so an interrupted run
resumes from the last checkpoint when restarted with the same command. The
`End time` set in the files is generous; the runs of the paper were stopped once
the diagnostics were statistically steady, at the modelled times t_p listed in
the paper's run-time table.

## Diagnostics

The Nusselt numbers use the boundary heat fluxes from the `heat flux statistics`
postprocessor (consistent boundary flux method), normalized by the conductive
solution of the annulus, and V_rms uses the velocity statistics, as described in
the paper. Both diagnostics were evaluated identically for ASPECT and GTXLBM and
averaged over the final 40 per cent of each run.
