---
layout: page
title: Turbo-compressor prototype
description: Centrifugal compressor for a model jet engine, from analytical design and CFD to a 3D-printed test rig
importance: 1
category: /engineering
related_publications: false
---

A two-semester team project to design, simulate, build and test the centrifugal compressor of a miniature (RC-scale) turbojet, then start sizing the combustion chamber that sits behind it.

- **Context:** R&D project (PJT), Arts et Métiers ParisTech, Aix-en-Provence, 2024–2025. Supervised by C. Faillat and P. Véron.
- **Tools:** Vista CCD (PCA Engineers), 3DExperience/CATIA, Siemens Star-CCM+, Abaqus, FDM 3D printing, Arduino.
- **Results:** CFD outlet pressure of **3.31 bar** against a **3.5 bar** design target; a working printed prototype that built **0.15–0.18 bar** at about **21,600 rpm** on the test bench, in line with the expected quadratic trend.

<div class="row mt-3">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-assembly-open.jpg" title="Printed prototype" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-rotor-stator.jpg" title="Rotor and stator CAD" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: the assembled prototype, with the motor mount, rotor, stator and outer casing. Right: the rotor (teal) inside the diffuser stator (red), as designed.
</div>

## 1. Design specification

The previous year's team had chosen an axial compressor, copied from fighter-jet engines. At RC scale, a single centrifugal stage is the standard choice, so we restarted from a benchmark of commercial micro-turbojets (JetCat P100-RX, P160 RXi-B and P300-PRO). Their pressure ratios range from 2.9 to 3.55, with peak speeds of 105,000–154,000 rpm.

A dimensional analysis (Vaschy-Buckingham) reduced the six governing quantities (diameter, length, speed, mass flow, inlet and outlet pressure) to four dimensionless groups.

Their values across the benchmark were consistent, so we scaled from the **JetCat P300-PRO**: a pressure ratio of **3.5**, a mass flow of **0.5 kg/s** and a speed of **105,000 rpm**.

## 2. Rotor and stator design

The impeller geometry came from Vista CCD, a meanline design tool by PCA Engineers, using design rules from the IMechE literature:

- **Inlet blade angle** of 60°, the optimum for maximum mass flow near Mach 0.55, rather than 80° for a static compressor, since the engine is meant to fly.
- **10° backsweep** at the trailing edge, which delays surge. The benchmark engines use the same value.
- **7 main blades and 7 splitter blades**, 2 mm thick, limited by what a 5-axis ball-end mill could machine at this scale. 1.5 mm fillets match a 1.5 mm ball-end tool.
- **20 mm hub** for the shaft, 0.1 mm tip clearance and an axial length of half the diameter, giving an **86 mm** rotor.

Because printing cannot hold a 0.1 mm tip gap, the printed version has a shroud built into the rotor.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-rotor-cad.jpg" title="Rotor" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-rotor-shroud.jpg" title="Shrouded rotor" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-stator-cad.jpg" title="Stator" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The open impeller with splitter blades, the shrouded version for printing, and the 20-vane diffuser stator (3DExperience).
</div>

The **stator** turns the swirling flow leaving the rotor back towards the axis. Its 20 guide vanes were set from the outlet velocity triangle at 100,000 rpm, assuming constant mass flow, no losses and flow that follows the blades.

The stator's flow area was kept constant along the passage as the radius changes.

## 3. CFD validation (Star-CCM+)

To keep the computation tractable, we simulated **a single blade passage** and used rotational symmetry for the rest. The air volume between two blades was extracted with a Boolean operation, then meshed and solved at the design point:

- **Boundary conditions:** stagnation inlet at 1 bar (air at rest), pressure outlet.
- **Physics:** steady, coupled, ideal gas, **k-ω SST** turbulence (k-ε is unsuited to this flow).
- **Mesh:** polyhedral cells with a 0.2 mm base size and prism layers in the boundary layer, keeping **y+ below 5** over almost all walls. Coarser 1 mm and 0.5 mm meshes diverged. 500 iterations took about 3 hours.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-cfd-mesh.jpg" title="Prism-layer mesh" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-cfd-velocity.jpg" title="Velocity magnitude" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-cfd-pressure.jpg" title="Total pressure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    One blade passage: the boundary-layer mesh, the velocity field (rising radially to the outlet) and the total pressure field.
</div>

The mean outlet pressure converged to **3.31 bar** for a 3.5 bar target, about 5% low. The mean outlet velocity was 581 m/s. Residuals stalled between 10⁻¹ and 10⁻², short of the usual target, but they no longer diverged. The mesh met Star-CCM+'s skewness and volume-change criteria, so we treated the result as a reasonable first validation of the design.

## 4. Structural check (Abaqus)

We also modelled a quarter of an aluminium rotor in Abaqus, under the 3.5 bar internal pressure and centrifugal loading. We ran 11 cases from 1,000 to 100,000 rpm. The stress grew linearly with speed, but peaked at only 0.016 MPa. A hand calculation shows this cannot be right: 10 g of blade at a radius of 43 mm and 100,000 rpm gives a force of about 47 kN, which is about 470 MPa on a 10 mm² section, beyond the yield strength of most aluminium alloys. We concluded that the load or unit setup in Abaqus was wrong, and listed this as an open issue rather than a result.

<div class="row mt-3">
    <div class="col-sm-8 mt-3 mt-md-0 mx-auto">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-abaqus.jpg" title="Abaqus quarter-rotor model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Von Mises stress on the quarter-rotor model. The near-uniform, tiny stresses pointed to a setup error.
</div>

## 5. Prototype and test bench

The rotor, stator, casing and motor mount were printed in PLA, and the parts in contact were sanded to close the gaps and smooth the airflow. Several parts had to be reprinted because the printed tolerances drifted from the CAD.

- **Shaft:** a machined steel shaft was drawn and quoted, but for lack of workshop time an **M8×85 screw** replaced it. Boring the rotor for the screw added a lot of imbalance.
- **Guidance:** a 20×8×7 bearing seated against its shoulder keeps the rotor clear of the casing. A second bearing seat was added at the rotor inlet for proper guidance.
- **Coupling:** a flexible **TPU** coupler threads onto the M8 shaft and the M5 motor shaft.
- **Casing:** a cylindrical shell closes the stage and channels the air into a rear plenum, where the pressure tap sits.

<div class="row mt-3">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-printed-parts.jpg" title="Printed stator and rotor" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-assembly.jpg" title="Closed assembly" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: the printed stator and shrouded rotor. Right: the assembly with the motor and ESC mounted above the rotor.
</div>

**Drive.** An iFlight XING-E Pro 2207 1800KV brushless motor runs from a LiPo through a Hobbywing XRotor 45A ESC. An Arduino reads a potentiometer and outputs the PWM command. The power estimate showed that this motor cannot reach the 100,000 rpm design point, so the bench was always meant to test at reduced speed. Speed is estimated from the PWM command, the battery voltage and the motor KV rating.

**Measurement.** An MPX700DP differential pressure sensor with an op-amp stage feeds the Arduino. It was calibrated from 0 to 3 bar against the manometer of the lab's air compressor and stayed within 5% of the reference.

<div class="row mt-3">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-test-bench.jpg" title="Test setup" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-wiring.jpg" title="Motor wiring" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: the test setup, with the sensor board, Arduino and compressor. Right: wiring of the LiPo, ESC, motor and Arduino with its speed potentiometer.
</div>

## 6. Test results

Each test point holds a fixed speed command and records the pressure rise. We ran **three series from 0 to 21,600 rpm**. Above that, vibration from the unbalanced rotor risked breaking the parts.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-test-measured.png" title="Measured pressure rise" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Pressure rise against estimated rotor speed for the three runs, after zero-offset correction. The dashed line is a quadratic through zero and the 3.5 bar, 100,000 rpm design point.
</div>

All three runs show real compression, reaching 0.15–0.18 bar at the top speed, and they follow the expected quadratic trend closely. The tested range is still only the first fifth of the design speed, so this supports the design without proving the 3.5 bar target.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-test-extrapolation.png" title="Tested range vs design point" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The same data on the full speed range: the tests cover the shaded region; the design point lies far beyond it.
</div>

## 7. Next stage: combustion chamber

With the compressor sized, we started the combustion chamber using the **Melconian and Modak** procedure. We chose an **annular** chamber, since the shaft runs through the engine's centre and can-type chambers would be too small at this scale. From the compressor's 0.5 kg/s and an assumed pattern factor of 0.25:

| Quantity | Value |
|---|---|
| Reference area | 0.0128 m² |
| Casing diameters (outer / inner) | 130 mm / 24 mm |
| Liner diameters (outer / inner) | 112 mm / 42 mm |
| Reference velocity | 21.6 m/s (Mach 0.31) |
| Liner length | 117 mm |
| Primary / secondary / dilution zones | 26 / 17.5 / 60 mm |

<div class="row mt-3">
    <div class="col-12 mx-auto mt-3" style="max-width: 450px;">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-combustor-schematic.jpg" title="Combustor airflow" class="img-fluid rounded z-depth-1" %}
        <div class="caption">Airflow split through the primary, secondary and dilution zones.</div>
    </div>
    <div class="col-12 mx-auto mt-3" style="max-width: 280px;">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-combustor-cad.jpg" title="Liner CAD" class="img-fluid rounded z-depth-1" %}
        <div class="caption">First CAD of the perforated liner.</div>
    </div>
    <div class="col-12 mx-auto mt-3" style="max-width: 220px;">
        {% include figure.liquid loading="eager" path="assets/img/projects/turbo-engine-cad.jpg" title="Compressor and combustor" class="img-fluid rounded z-depth-1" %}
        <div class="caption">The compressor stacked on the combustion chamber.</div>
    </div>
</div>

Fuel injection and the turbine were left open, since both depend on measured compressor outlet conditions that only a metal prototype could provide.

## Lessons and next steps

- **Balance the rotor first.** Imbalance, not motor power, capped the tests at about 22,000 rpm. A machined shaft and a balanced rotor are the prerequisites for going faster.
- **Build a metal version.** A machined aluminium rotor would allow testing near the design speed. The shaft drawing and stock quotes are ready.
- **Better instrumentation:** an optical tachometer instead of estimating speed from PWM, and temperature sensors for efficiency.
- **Fix the structural model** and validate it against the hand estimate before trusting it.

## Documents

- [Poster (PDF)](/assets/pdf/poster_pjt.pdf)
- [Final presentation slides (PDF)](/assets/pdf/sountenance_pjt.pdf)

<iframe src="/assets/pdf/poster_pjt.pdf" width="100%" height="700"
        style="border:1px solid #888; border-radius:8px;"></iframe>
<p><a href="/assets/pdf/poster_pjt.pdf">Open the PDF in a new tab</a></p>

Team: Dorian Mandrino, Mateo Mangialomini, Alexandre Poncelet, Charny Xu (with T. Lhote and G. Rique in the first semester).