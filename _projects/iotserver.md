---
layout: page
title: IoT Server
description: Internet of Things server to provide actuator and sensor functionalities to clients
img: assets/img/iot.jpg
importance: 1
category: work
giscus_comments: false
---
`November 2023 - December 2023`

In the course CPEN 221, I was tasked with implementing an Internet of Things (IoT) server. Hence, I designed a system comprising actuators and sensors (referred to as entities). These entities seamlessly communicated with a centralized server (called the Message Handler), creating a dynamic and interconnected IoT environment. Each entity, assigned to a specific client, transmitted events or data to the server.

`Client Control and Interaction`

Clients were given a range of control options over their entities. They could toggle actuators, momentarily halt data transmission from any entity, predict the next N events (N being some inputted number), and apply data filters. These controls allowed clients to customize their IoT experience, ensuring that data flow and device behavior aligned with their specific requirements. 

`Technical Insights`

This project served as a rich learning experience, providing insights into critical aspects of software development and IoT technologies. Key takeaways include knowledge in server implementation, proficiency in message passing and network programming, handling of concurrency challenges, ensuring safety in concurrent programming, and the implementation of multi-threading techniques to optimize system performance.

In particular, I learned the importance of unit-testing and integration-testing. These methods saved me a lot of time debugging the server and ensurred seamless client-server connection. 

`Application`

The hands-on experience garnered from this project not only bolstered my technical skills but also equipped me with the practical skills needed to manage and optimize distributed IoT environments. This provided a solid foundation for tackling the intricacies and challenges of real-world IoT applications and emphasized the importance of debugging especially with concurrent programs. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/iot1.png" title="Tasks Processed By Message Handler" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Tasks processed by the Message Handler shown in terminal
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/iot2.png" title="Connection of a Client in Main" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Connection of a client within the "Main" class shown in terminal
</div>
