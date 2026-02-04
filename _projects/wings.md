---
layout: page 
title: wings
description: Image classification pipeline utilizing custom CNNs and transfer learning (ResNet-50) to identify bird species.
# img: assets/img/baja_can_dashboard.jpg
importance: 9
category: Projects
---

`December 2025 - Present`

Wings is a deep learning project focused on bird species classification. The project explores the performance trade-offs between building a custom Convolutional Neural Network (CNN) from scratch and leveraging industry-standard transfer learning models like ResNet-50.

### Technical Insights
Designed and implemented an end-to-end image classification pipeline using PyTorch and torchvision. The project involved comparing a ground-up architecture with a transfer learning approach to evaluate training efficiency and generalization.

* Custom CNN Development: Implemented a modular architecture using convolution, batch normalization, ReLU activation, max pooling, and fully connected layers.
* Transfer Learning: Applied a pretrained ResNet-50 backbone, replacing the classification head for specific bird species prediction.
* GPU Acceleration: Enabled seamless switching between CPU and CUDA for accelerated training and inference.
* Optimization Techniques: Mitigated overfitting through dropout, data normalization, and controlled freezing/unfreezing of model layers.

### Results
The study achieved faster convergence and improved accuracy using pretrained models compared to the custom architecture on limited datasets. This project highlights a scalable system design that allows for extension to new datasets or deeper network architectures.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bird.jpg" title="Eurasian Magpie inputted into the Machine Learning Model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Eurasian Magpie inputted into the Machine Learning Model
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bird_results.png" title="Prediction from the Wings Neural Network" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Prediction from the Wings Neural Network
</div>


[View the code on GitHub](https://github.com/GeoffreyBian/wings)
