---
layout: page
title: Wind turbine gearbox
description: Detailed design and digital mock-up of a 200 kW planetary speed-increaser in 3DEXPERIENCE/CATIA
importance: 3
category: /engineering
related_publications: false
---

- **Context:** Detailed design & DMU project, Arts et Métiers, 2023–2024 (team of 4)
- **Tools:** Dassault 3DEXPERIENCE / CATIA (part design, assembly, kinematic simulation, 2D drafting)
- **My part:** modelling of my share of the parts, and the detailed manufacturing drawing of the sun-gear shaft

- [Technical notice (PDF)](/assets/pdf/wind_gearbox_report.pdf)
- [2D drawings](#drawings)

We designed the gearbox that sits between the rotor and the generator of a **200 kW** wind turbine, starting from a specification, a minimal kinematic diagram and imposed SKF bearings. The rotor turns at 50–70 rpm; the asynchronous generator needs about 3,025 rpm.

<figure style="text-align:center">
  <img src="/assets/img/projects/wind-gearbox-full.jpg" alt="Full digital mock-up of the wind turbine gearbox"
       style="width:100%; max-width:560px; border-radius:8px;">
  <figcaption>Complete digital mock-up with its three aluminium housings.</figcaption>
</figure>

## Architecture

- **Planetary stage** (sun Z=23, 3 planets Z=43, ring Z=109, module 8 mm) driven by the planet carrier, ratio of about 5.74.
- **Two parallel spur stages** (57/21 and 63/19), combined ratio of 9.
- **Overall speed-up ≈ 51.7**, so 3,025 rpm at the generator for ≈ 58.6 rpm at the rotor.
- Hollow sun and carrier shafts, so a 60 mm rod can pass through the whole gearbox along its axis.
- Sealing with lip seals, flat gaskets and a V-ring; splash lubrication with fill/drain plugs and an oil-level gauge.
- Gears either cut on the shaft or fixed by key/splines and bearing shoulders; overall dimensions within ±3% of the imposed envelope.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    <img src="/assets/img/projects/wind-gearbox-open.jpg" alt="Gearbox without housings" style="width:100%; border-radius:8px;">
  </div>
  <div class="col-sm mt-3 mt-md-0">
    <img src="/assets/img/projects/wind-gearbox-planetary.jpg" alt="Planetary stage" style="width:100%; border-radius:8px;">
  </div>
</div>
<div class="caption">Left: gear train without housings. Right: planetary stage (one planet modelled).</div>

## Outcome

We delivered the 3D mock-up, an assembly sequence, a bill of materials (materials and manufacturing processes for each part), 2D drawings and a working kinematic simulation. Getting the kinematic simulation to run took several iterations; we fixed it mainly by adjusting the dimensions of the parts that collided.

## Drawings

Click a drawing to open the full-resolution PDF.

<figure style="text-align:center">
  <a href="/assets/pdf/wind_gearbox_assembly_drawing.pdf">
    <img src="/assets/img/projects/wind-gearbox-drawing-assembly.jpg" alt="General assembly drawing" style="width:100%; border:1px solid #888; border-radius:8px;">
  </a>
  <figcaption>General assembly drawing.</figcaption>
</figure>

<div class="row">
  <div class="col-sm-6 mt-3">
    <a href="/assets/pdf/wind_gearbox_sun_shaft_drawing.pdf">
      <img src="/assets/img/projects/wind-gearbox-drawing-sun-shaft.jpg" alt="Sun-gear shaft drawing" style="width:100%; border:1px solid #888; border-radius:8px;">
    </a>
    <div class="caption">Sun-gear shaft (my drawing).</div>
  </div>
  <div class="col-sm-6 mt-3">
    <a href="/assets/pdf/wind_gearbox_input_shaft_drawing.pdf">
      <img src="/assets/img/projects/wind-gearbox-drawing-input-shaft.jpg" alt="Input shaft drawing" style="width:100%; border:1px solid #888; border-radius:8px;">
    </a>
    <div class="caption">Input shaft.</div>
  </div>
  <div class="col-sm-6 mt-3">
    <a href="/assets/pdf/wind_gearbox_central_housing_drawing.pdf">
      <img src="/assets/img/projects/wind-gearbox-drawing-central-housing.jpg" alt="Central housing drawing" style="width:100%; border:1px solid #888; border-radius:8px;">
    </a>
    <div class="caption">Central housing.</div>
  </div>
  <div class="col-sm-6 mt-3">
    <a href="/assets/pdf/wind_gearbox_spur_housing_drawing.pdf">
      <img src="/assets/img/projects/wind-gearbox-drawing-spur-housing.jpg" alt="Spur-stage housing drawing" style="width:100%; border:1px solid #888; border-radius:8px;">
    </a>
    <div class="caption">Spur-stage housing.</div>
  </div>
</div>

Team: Harold Gardon, Dorian Mandrino, Mateo Mangialomini, Alexandre Poncelet.