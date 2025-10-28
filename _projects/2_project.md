---
layout: page
title: Shocks
description:
img: assets/img/project_2/compass_cropped.png
importance: 2
category: work
---


High resolution simulations of shocks in galaxy clusters

***

The collision of galaxy clusters are the most energetic events in the universe since the Big Bang.
They are observable as spectacular arcs in the radio-sky, the so-called **radio relics**.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_2/relic.png" title="radio" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The radio relics in the cluster Abell 3667 as seen by MeerKAT. Image taken from <a href="https://ui.adsabs.harvard.edu/abs/2022A%26A...659A.146D/abstract" target="_blank">de Gasperin et. al. (2022)</a>.
</div>

The origin of this radio emission is thought to be relativistic electrons accelerated by the shock, which are loosing their energy in the form of synchrotron emission due to the magnetic field in the intra-cluster medium (ICM).

Further, recent observations show an increasing number of radio relics with complex morphologies. 
These relics are deformed, patchy and of strongly varying surface brightness.

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_2/compass.png" title="radio" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
        Shock structures found in the <a href="http://www.magneticum.org/complements.html#COMPASS" target="_blank">COMPASS</a> simulation set.
</div>

To study the origin of this observed deformation and patchyness I work with state-of-the art MHD zoom-in simulations of galaxy clusters.
These simulations contain an on-the-fly shock finder which allows to show shock surfaces and estimate acceleration of CR electrons, based on recent results from small scale plasma simulations.

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project_2/virgo.png" title="radio" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Shock surfaces classified with the <a href="https://github.com/maxlampe/virgo" target="_blank">VIRGO</a> pachage (see <a href="https://github.com/maxlampe/virgo" target="_blank">VIRGO</a>).
</div>

While the on-the-fly shock finder allows us to mark tracer particles that experience a shock, we can not easily disentangle colliding or overlapping shock waves from simultanious merger events.
To this end I contributed to the development of [Virgo](https://github.com/maxlampe/virgo), an advanced **Machine Learning** model which identifies shock surfaces and cathegorizes their associated tracer particles.
We presented the package and its application to the [COMPASS](http://www.magneticum.org/complements.html#COMPASS) simulation set in [Lamparth et. al. (2022)](https://ui.adsabs.harvard.edu/abs/2022arXiv220806859L/abstract).