---
layout: page
title: Turbulence
description: 
img: assets/img/project_3/turbulence_cropped.png
importance: 3
category: work
---

Injection of turbulence by merger shocks and its impact on re-acceleration of Cosmic Rays and amplification of magnetic fields

***

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project_3/perseusvirgo.jpg" title="radio" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Deep X-ray observations by <a href="https://chandra.harvard.edu/photo/2014/perseusvirgo/" target="_blank">Chandra</a> show shocks and gas sloshing in the Perseus cluster (left) and AGN jets in Virgo (right).
</div>


Galaxy clusters are highly dynamic systems with frequent mergers, accretion events abd episodes of feedback by AGN.
This stirrs up the hot intra-cluster medium (ICM) and injects energy at the scale of several hundred of kpc.
This energy is transported down to scales of the Lamour radius of the free electrons and protons in the plasma of the ICM following a turbulent cascade until it dissipates on these smallest scales.

----

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project_3/turbulence.png" title="turbulence map" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project_3/Eturb_evolution.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: A thin slice through the turbulent energy of the <a href="http://www.magneticum.org/complements.html#COMPASS" target="_blank">COMPASS</a> simulation set. Right: Time evolution of the total turbulent energy in the system for hot and cold gas.
</div>

I work with state-of-the art MHD zoom-in simulations of galaxy clusters to study the injection, evolution and dissipation of turbulent energy.
These ultra-high resolution simulations allow to study the role of turbulence even far outside the cluster center, as turbulence effects are resolution dependent.
In addition to energy dissipation turbulence provides a non-thermal pressure component.
This pressure component is found to be overestimated in most simulations (see [Sayers et. al. (2021)](https://ui.adsabs.harvard.edu/abs/2021MNRAS.505.4338S/abstract)).
We find that with the high resolution of the [COMPASS](http://www.magneticum.org/complements.html#COMPASS) set the non-thermal pressure support agrees well with observations (Böss et. al. *(in prep)*).

----

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project_3/dynamo.png" title="radio" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Phase-space diagram showing the effect of magnetic field amplification by the turbulent dynamo. For details see <a href="https://ui.adsabs.harvard.edu/abs/2022ApJ...933..131S/abstract">Steinwandel et. al. (2022)</a>.
</div>

Another effect turbulence has on galaxy clusters is the amplification of magnetic fields via the **turbulent dynamo**.
In this process magnetic field lines are stretched, bent and folded by turbulent motion of the plasma.
This amplifies the magnetic field exponentially over a timescale of only a few hundres of million years until the turbulent dynamo saturates.
To study this effect in simulations I contributed to the work by [Steinwandel et. al. (2022)](https://ui.adsabs.harvard.edu/abs/2022ApJ...933..131S/abstract) where we studied the impact of resolution in the turbulent dynamo and the amplification of the magnetic field.
For this worked we used the open source software packages I developed for work with our simulation code *OpenGadget3*, which you can find in the [Software](/repositories/) page of this website.