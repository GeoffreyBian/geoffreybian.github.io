---
layout: page 
title: UBC Baja Vehicle CAN Bus Network
description: Network of 5 STM32 ECUs communicating suspension and rear vehicle data to a Raspberry Pi dashboard.
# img: assets/img/baja_can_dashboard.jpg
importance: 7
category: Projects
---

`September 2024 – February 2025`

For the UBC Baja SAE team, I developed the vehicle’s distributed CAN bus network, connecting five STM32-based ECUs—four controlling the independent suspension modules and one managing the rear PCB—to a centralized dashboard running on a Raspberry Pi using Gradle. The system enables real-time communication of vehicle telemetry, sensor data, and actuator states to a unified dashboard, allowing the driver and team to monitor performance and diagnose issues during testing and competition.

The project involved designing a robust communication protocol over CAN to handle high-frequency updates from multiple ECUs without message collisions or data loss. Each STM32 ECU was responsible for reading sensors, performing local control calculations, and broadcasting status messages over the bus. The dashboard software aggregated messages from all ECUs, processed telemetry, and displayed key vehicle parameters such as suspension position, shock velocity, and rear powertrain metrics.

A key technical challenge was ensuring deterministic behavior under the high-speed data loads typical of off-road vehicle operation. This required careful selection of message IDs, prioritization of CAN frames, and implementation of caching and filtering strategies on the dashboard to maintain smooth visualization. Additionally, the system had to be resilient to transient bus errors and node dropouts, ensuring the vehicle remained operable even if a single ECU failed or temporarily disconnected.

The project combined embedded firmware development, real-time systems design, and software engineering for the dashboard application. The resulting network provides a scalable architecture for integrating future subsystems and improving the vehicle’s telemetry capabilities.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/baja_ecu.png" title="STM32 ECU module for suspension control" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    STM32 ECU module for suspension control
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/baja_dash.png" title="Raspberry Pi dashboard displaying telemetry from all ECUs" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Raspberry Pi dashboard displaying telemetry from all ECUs
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/baja_car.jpg" title="Baja Vehicle Mochi" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Baja Vehicle Mochi
</div>

[View the firmware on GitHub](https://github.com/UBC-Baja-SAE/firmware)
