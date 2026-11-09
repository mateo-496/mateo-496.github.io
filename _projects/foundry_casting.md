---
layout: page
title: Aluminium sand casting
description: Designing, simulating and pouring an AlSi13 bird-feeder part in a 3D-printed sand mould
importance: 3
category: /engineering
related_publications: false
---

- **Context:** Arts et Métiers foundry project (team of 3), autumn 2024
- **Tools:** CATIA V5, ESI QuikCAST (thermal and filling simulation), 3D-printed sand mould

- [Full report, in French (PDF)](/assets/pdf/foundry_report.pdf)
- [Presentation (pictures),  in French (PDF)](/assets/pdf/foundry_presentation.pdf)

We took a bird-feeder base (a thin dish with two helical arms) from CAD to a real aluminium part, poured at the school foundry.

<div class="row mt-3">
  <div class="col-sm-6">
    <img src="/assets/img/projects/foundry-cast-part.jpg" alt="The cast part with its feeders and gating system, next to the pouring cup"
         class="img-fluid rounded z-depth-1" loading="lazy">
  </div>
  <div class="col-sm-6">
    <img src="/assets/img/projects/foundry-final-part.jpg" alt="The finished aluminium bird-feeder part after fettling"
         class="img-fluid rounded z-depth-1" loading="lazy">
  </div>
</div>
<div class="caption">Left: the casting straight out of the mould, with feeders and runners. Right: the part after fettling.</div>

**Design and simulation**

- Compared pouring orientations in QuikCAST and kept the one that moved shrinkage away from the thin screw boss, then thickened that boss so it could take a feeder.
- Sized three cylindro-spherical feeders with the modulus, volumetric-shrinkage and feeding-distance rules.
- Sized a two-ingate gating system: filling time from the thinnest section (1.16 mm, filling time of about 1.4 s), then iterated on hydraulic efficiency to get the sprue section.
- Re-simulated the full layout: the cavity fills in about 1.5 s with the metal still 38 °C above the liquidus, and solidification ends inside the feeders.

<img src="/assets/img/projects/foundry-quikcast.jpg" alt="QuikCAST solid-fraction simulation of the part"
     class="img-fluid rounded z-depth-1 d-block mx-auto" style="max-width: 520px;" loading="lazy">
<div class="caption">QuikCAST solid-fraction simulation.</div>

**Mould and casting**

- Split the mould for 3D sand printing (a conical core for the helical arms, a plug for cleaning the top feeder, and tongue-and-groove joints), then flamed it and poured it.
- Measured yield matched the prediction closely: a metal-to-part ratio of 2.89, against 2.93 expected.
- Cutting the feeders showed the shrinkage cavities ended up in them as intended.

<div class="row mt-3">
  <div class="col-sm-6">
    <img src="/assets/img/projects/foundry-feeder-top.jpg" alt="Cross-section of the top feeder showing a shrinkage cavity"
         class="img-fluid rounded z-depth-1" loading="lazy">
  </div>
  <div class="col-sm-6">
    <img src="/assets/img/projects/foundry-feeder-side.jpg" alt="Cross-section of a side feeder and part of the runner showing a shrinkage cavity"
         class="img-fluid rounded z-depth-1" loading="lazy">
  </div>
</div>
<div class="caption">Sectioned feeders: the top feeder (left) and a side feeder with part of the runner (right). The shrinkage cavities sit in the feeders, not in the part.</div>

- Some small shrinkage pores remained on the dish. We traced them to the solidification front splitting across the dish, which a tapered dish thickness would have fixed.


Team: Maxence Chauvel, Dorian Mandrino, Mateo Mangialomini.