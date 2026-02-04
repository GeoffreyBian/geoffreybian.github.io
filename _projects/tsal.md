---
layout: page 
title: Tractive System Active Light (TSAL) 
description: Safety-critical PCB designed for the Quadruna electric race car to monitor voltage differentials. 
# img: assets/img/tsal_project.jpg 
importance: 6
category: Projects

---
`October 2023 – May 2024`

The Tractive System Active Light (TSAL) is a safety-critical component developed for UBC Formula Electric’s vehicle, Quadruna, for the 2024 Formula SAE competition. The board serves as a vital visual warning system, signaling a red light if high voltage (HV) and low voltage (LV) systems become imbalanced. In a racing environment where voltages can reach lethal levels, this board ensures that the vehicle is safe for both the driver and the pit crew by indicating whether the high-voltage system is active or potentially short-circuited into the 24V low-voltage electronics.

The engineering process involved translating high-level safety requirements into a physical PCB using Altium Designer. A primary technical challenge was the integration of a 555 timer circuit to meet FSAE regulations, which dictate that the TSAL must flash specifically when signaling a red "unsafe" state, while remaining solid for other states.

Designing for a high-performance vehicle required rigorous component selection; every LED was vetted for specific millicandela (mcd) ratings to ensure visibility under bright track conditions, and all power components were rated for the transients found in an electric powertrain. The final layout was optimized into a compact 8 cm x 4 cm rectangular footprint, requiring precise trace routing and adherence to strict design rules to fit within the mechanical constraints of the chassis.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/tsal_schematic.png" title="Schematic Diagram of the TSAL board in Altium" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Schematic Diagram of the TSAL board in Altium
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/tsal_altium.png" title="Board Diagram of the TSAL board in Altium" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Board Diagram of the TSAL board in Altium
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/tsal_physical.png" title="Physical TSAL board" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Physical TSAL board
</div>
