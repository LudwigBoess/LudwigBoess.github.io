---
layout: page
title: Shocks
description:
img: assets/img/project_2/compass_cropped.png
importance: 2
category: work
giscus_comments: false
---

High-resolution simulations of shocks in galaxy clusters

***

Collisions of galaxy clusters are the most energetic events in the Universe since the Big Bang.
The shocks they drive are observable as spectacular arcs in the radio sky, the so-called **radio relics**.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_2/relic.png" title="Radio relics in Abell 3667" alt="MeerKAT radio image of the radio relics in Abell 3667" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The radio relics in the cluster Abell 3667 as seen by MeerKAT. Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2022A%26A...659A.146D/abstract" target="_blank">de Gasperin et al. (2022)</a>.
</div>

This radio emission is thought to originate from relativistic electrons accelerated at the shock, which lose their energy as synchrotron radiation in the magnetic field of the intra-cluster medium (ICM).

Further, recent observations show an increasing number of radio relics with complex morphologies.
These relics are deformed, patchy and of strongly varying surface brightness.

---

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_2/compass.png" title="Shocks in COMPASS" alt="Shock structures in a simulated galaxy cluster from the COMPASS simulation set" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Shock structures found in the <a href="http://www.magneticum.org/complements.html#Compass" target="_blank">COMPASS</a> simulation set.
</div>


To study the origin of this deformation and patchiness I work with state-of-the-art MHD zoom-in simulations of galaxy clusters.
These simulations contain an on-the-fly shock finder ([Beck et al. 2016](https://ui.adsabs.harvard.edu/abs/2016MNRAS.458.2080B/abstract)), which identifies shock surfaces and allows us to estimate the acceleration of CR electrons based on recent results from small-scale plasma simulations.

---

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_2/virgo.png" title="Shock classification with Virgo" alt="Shock surfaces in a simulated galaxy cluster, labelled by Virgo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Shock surfaces in a simulated galaxy cluster, classified by Virgo. Each color marks an individual shock surface, the right panel additionally shows particles classified as non-shock (gray). Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2022arXiv220806859L/abstract" target="_blank">Lamparth et al. (2022)</a>.
</div>

While the on-the-fly shock finder allows us to mark tracer particles that experience a shock, it cannot easily disentangle colliding or overlapping shock waves from simultaneous merger events.
To this end I contributed to the development of [Virgo](https://github.com/maxlampe/virgo), a scalable, unsupervised **machine learning** pipeline which identifies individual shock surfaces and classifies their associated tracer particles.
We presented the package and its application to the [COMPASS](http://www.magneticum.org/complements.html#Compass) simulation set in [Lamparth et al. (2022)](https://ui.adsabs.harvard.edu/abs/2022arXiv220806859L/abstract).

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/publication_preview/box4.png" title="SPH vs. MFM shock detection" alt="Surface density, temperature and dissipated shock energy in the Box4 simulation for SPH and MFM" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Surface density, temperature and dissipated shock energy in the Box4 simulation, run with SPH (top) and MFM (bottom). Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2026arXiv261038700B/abstract" target="_blank">Böss et al. (2026)</a>.
</div>

The on-the-fly shock finder described above was built for smoothed particle hydrodynamics (SPH).
Fully Lagrangian methods like SPH have historically had a hard time capturing shocks as accurately as grid-based or moving-mesh codes.
This is especially true in galaxy clusters, where shocks overlap and collide while being embedded in strong shear flows.
To remedy this I developed the first shock finder with shock surface reconstruction for **meshless finite mass (MFM)** hydrodynamics, using the MFM implementation in *OpenGadget3* ([Groth et al. 2023](https://ui.adsabs.harvard.edu/abs/2023MNRAS.526..616G/abstract)).
It identifies shocked cells from converging flows, reconstructs the shock surface by walking along the kernel neighbors, and evaluates the Rankine-Hugoniot jump conditions across that surface to obtain the sonic Mach number.

We tested the new shock finder against analytic solutions for hydrodynamic, magnetized and CR-modified shock tubes, as well as Sedov-Taylor blast waves.
In cosmological simulations it captures more than three orders of magnitude more dissipated shock energy than the legacy SPH shock finder in the Box4 galaxy group, converges at much lower resolution, and produces CR protons that fill almost the entire volume of our galaxy cluster zoom-in simulations.
We presented the method in [Böss et al. (2026)](https://ui.adsabs.harvard.edu/abs/2026arXiv261038700B/abstract).
