---
layout: page 
title: F1TENTH Dynamic Object Avoidance
description: A predictive ROS2 system using an Extended Kalman Filter and RGB-D sensor fusion to avoid high-speed dynamic obstacles.
# img: assets/img/doa_thumbnail.jpg
importance: 1
category: Projects
---

`September 2025 – December 2025`

**Team:** CPEN 391 Group 5  
**Core Stack:** ROS2 (Foxy), Python, OpenCV, Intel RealSense, F1TENTH Platform  

### Project Overview
Standard autonomous racing focuses on static wall-following or gap-finding. This project, **Dynamic Object Avoidance (DOA)**, pushes the F1TENTH platform to its limits by enabling it to detect, track, and predict the trajectory of small, fast-moving obstacles (like tennis balls) that are traditionally invisible to LiDAR.



### Technical Insights: The EKF Pipeline
The "secret sauce" of this project is the **4-State Constant Velocity Kalman Filter**. Because camera-based object detection is inherently noisy and the depth data from a moving car can be sparse, we implemented a filter to maintain a stable estimate of the object's position and velocity.

#### 1. State Estimation with Kalman Filtering
The filter maintains a state vector $\mathbf{x}_k$:
$$\mathbf{x}_k = \begin{bmatrix} p_x \\ p_y \\ v_x \\ v_y \end{bmatrix}$$

* **Prediction Step:** We project the ball’s position using the time delta ($\Delta t$) and the constant velocity assumption.
* **Correction Step:** We fuse raw measurements from the HSV vision pipeline. This allows the car to "remember" where the ball is and where it's going, even if the camera drops a frame.

#### 2. Predictive Masking
Once we have a filtered velocity, the system calculates a **Time-to-Collision (TTC)**. If a collision is predicted, we don't just "turn"—we perform **Predictive Masking**. We virtually "paint" an obstacle into the LiDAR scan at the *predicted* impact point. This forces the standard Gap Follower algorithm to treat the future collision zone as a physical wall, resulting in a smooth, proactive maneuver rather than a reactive jerk.



### Vision & Control Strategy
The system uses a modular ROS2 architecture consisting of five primary nodes:
* **Object Detection:** HSV segmentation + Pinhole Projection ($Z_{\text{cam}} \frac{u - C_X}{F_X}$).
* **Trajectory Prediction:** EKF-based state estimation.
* **Maneuver Node:** Dynamic speed adjustment and steering using a PD controller ($Kp = 0.33, Kd = 0.1$).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/object_detection.png" title="HSV Masking for Tennis Ball Detection" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/state_machine.png" title="3D Position Projection State Machine" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    3D Position Projection in Action and State Machine
</div>

---

### Project Links
* **GitHub Repository:** [Project_GA5 - Dynamic Object Avoidance](https://github.com/GeoffreyBian/DOA)
* **Full Report (PDF):** [DOA (Dynamic Object Avoidance)](/assets/pdf/DOA.pdf)