---
layout: page
title: Plasma Physics
description:
img: assets/img/project_4/turbulence_jz_cropped.png
importance: 4
category: work
---

**Entity** - *A hardware-agnostic Particle-in-Cell code for plasma astrophysics*

***

Almost all of the visible matter in the universe is in the form of a plasma, a hot gas of electrons and ions threaded by magnetic fields.
In galaxy clusters, around neutron stars and black holes, or in the solar wind these plasmas are so dilute that particles practically never collide.
Instead they interact through the electric and magnetic fields they create themselves.
The physics on these small scales, like particle acceleration at shocks, instabilities driven by cosmic rays and the dissipation of turbulence, cannot be captured by the fluid description I use in my cosmological simulations.

**Particle-in-Cell (PIC)** simulations solve this problem from first principles.
They solve the Vlasov-Maxwell system of equations by following a large number of macroparticles, each representing many electrons or ions, as they move through electromagnetic fields defined on a grid.
The particles deposit their electric currents onto the grid, the fields are updated with Maxwell's equations, and the new fields are interpolated back to the particles to push them forward in time.

I am one of the developers of [Entity](https://entity-toolkit.github.io), a new, fully open-source PIC code built for modern GPU supercomputers.
Using the [Kokkos](https://kokkos.org) library it runs on NVIDIA, AMD and Intel GPUs, as well as on CPUs, from a single code base.
Entity is the first PIC code that solves the Vlasov-Maxwell system in general coordinates, which allows it to simulate both Cartesian boxes and curvilinear geometries like the magnetospheres of neutron stars.
We presented the code in [Hakobyan et al. (2026)](https://ui.adsabs.harvard.edu/abs/2026ApJS..285...11H/abstract).

---

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/publication_preview/shape_functions.png" title="Particle shape functions" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Particle shape functions $\mathcal{S}_1$ to $\mathcal{S}_{11}$ implemented in Entity, normalized to the size of a grid cell $\Delta x$. Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2026arXiv260515260B/abstract" target="_blank">Böss et al. (2026)</a>.
</div>

Most plasma phenomena grow from initially tiny fluctuations, so a PIC code has to make sure that a growing instability is physical and not just numerical noise.
Each macroparticle has a finite size, described by its *shape function*.
The standard choice only spreads a particle over its neighboring grid cells.
With a limited number of particles per cell this produces noise, which artificially heats the plasma and can seed purely numerical instabilities.

In [Böss et al. (2026)](https://ui.adsabs.harvard.edu/abs/2026arXiv260515260B/abstract) I led the effort to add higher-order methods to Entity.
We implemented the charge-conserving current deposit by [Esirkepov (2001)](https://ui.adsabs.harvard.edu/abs/2001CoPhC.135..144E/abstract) for shape functions up to 11th order, together with a field interpolation that uses the same shapes.
Going from first- to second-order shape functions reduces the grid resolution needed to keep a cold plasma numerically stable by a factor of $\sim 4$ per dimension, and third order by a factor of $\sim 8$.
This can offset the higher cost per particle, since the total cost of a simulation grows steeply with resolution.

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_4/decaying_turbulence.png" title="Decaying turbulence" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Current density $J_z$ in a simulation of decaying plasma turbulence after three Alfvén crossing times. From left to right: the standard Zigzag deposit, the Esirkepov deposit with 2nd, 3rd, 5th and 9th order shape functions, and Zigzag with 16 passes of current filtering. Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2026arXiv260515260B/abstract" target="_blank">Böss et al. (2026)</a>.
</div>

In simulations of decaying turbulence, higher-order shapes clearly reduce the noise in the small-scale current sheets, while the large-scale structure stays the same.
They also improve energy conservation: with 9th-order shapes the error in total energy drops by two orders of magnitude, and 2nd order already conserves energy as well as the standard scheme at $8\times$ the resolution.
Filtering the currents smooths the noise as well, but at the risk of also smoothing out physical gradients.

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_4/field_stencils.png" title="Field stencils" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Magnetic field $B_z$ of a single electron moving through vacuum with a Lorentz factor $\gamma = 10$, for different directions of motion (rows) and field solver stencils (columns). The numerical Cherenkov effect shows up as additional waves ahead of or behind the particle. Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2026arXiv260515260B/abstract" target="_blank">Böss et al. (2026)</a>.
</div>

The second ingredient is the field solver.
The standard Yee scheme computes spatial derivatives from only two neighboring grid points.
On such a grid electromagnetic waves travel slightly slower than in reality, so particles moving at almost the speed of light can outrun their own fields and emit spurious radiation, the so-called *numerical Cherenkov instability*.
We generalized Entity's field solver to wider finite-difference stencils, which can be tuned to suppress this numerical dispersion.
Besides established 2D stencils from the literature, we introduced new stencils optimized for 3D simulations.

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_4/pair_shock.png" title="Relativistic pair shock" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Density (top), temperature (middle) and out-of-plane magnetic field (bottom) in a relativistic pair-plasma shock. In each block the upper panel uses the standard Yee stencil, the lower panel the optimized min3 stencil. Left: Zigzag deposit, right: Esirkepov deposit with 3rd order shape function. Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2026arXiv260515260B/abstract" target="_blank">Böss et al. (2026)</a>.
</div>

This matters a lot for relativistic shocks.
In a 2D simulation of a shock in an electron-positron plasma with an upstream Lorentz factor of $\gamma = 10$, the numerical Cherenkov instability heats the plasma ahead of the shock by almost three orders of magnitude when using the Yee stencil.
This overheated plasma changes the structure of the shock and leads to a steeper spectrum of accelerated particles downstream.
Combining the optimized min3 stencil with 3rd-order shape functions almost completely removes the instability.

None of these methods is a silver bullet: higher-order shapes are cheap in 1D, but become prohibitively expensive beyond 3rd order in 3D.
Entity now lets the user choose the combination of shape function order, field stencil and current filtering that works best for a given problem.
