---
layout: page
title: Egg Roulette
description: A MuJoCo study on the SO-101 arm. Can a robot learn how hard to squeeze from people wearing a touch-sensing glove?
img: assets/img/egg_roulette/hero.png
importance: 2
category: Projects
---

`November 2026` · [Code, data and every figure on GitHub](https://github.com/GeoffreyBian/egg-roulette)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/egg_roulette/egg_roulette.gif" title="Robot demos only (left) vs. plus human demos with touch (right), same carton" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Same carton, same arm. Left: trained on robot teleoperation demos only. Right: plus 150 demos from a person wearing a touch glove.
</div>

Six eggs that look the same go from a carton to a basket. Some are raw (60 g, the shell cracks above 2.2 N). Some
are painted stone (300 g, needs about 3.5 N to carry). A camera can't tell them apart, so a robot trained on
teleoperation demos learns one compromise squeeze: it cracks raw eggs and drops stones. Add 150 demos from a person
wearing a touch glove and the same arm learns to start gentle, feel the load, and tighten only when the egg turns out
to be heavy.

| | eggs moved intact (25 robot demos) |
|---|---|
| robot teleop demos only | 49% |
| + human video, no touch | 42% |
| touch sensor on the robot, robot demos only | 52% |
| **+ 150 human demos with touch** | **93%** |

5 seeds x 60 test eggs per row. The human grip strategy is fitted to 718 real grasps from a 160-taxel glove dataset;
everything else is simulated, and the task was built so that looks mislead.

### The simulation

The scene is built with MuJoCo's `MjSpec` API on top of the unmodified SO-101 model from MuJoCo Menagerie. The edits
are where the physics lives:

- The jaw's stiff position servo becomes a torque-limited current loop closed at 500 Hz, so squeeze is a smooth
  function of the command, like an STS3215 with its P gain turned down.
- Silicone-pad contacts: friction 0.8, torsional friction for a 12 mm pad (`condim=6`), a soft 20 ms `solref`,
  elliptic friction cones and `impratio=10`.
- Native `touch` sensors over each jaw's contact patch, placed from 3,300 measured contact points, plus an
  `actuatorfrc` sensor standing in for servo current.
- Raw eggs crack at runtime: the egg is swapped for yolk, white and shell bodies that inherit its pose and velocity.

Policies are ACT-style: an MLP predicts chunks of 8 future actions, blended online with temporal ensembling. 80
policies for the main result, 160 for the ablations, 12,000 test eggs for the robustness grid.

### Checking the physics before trusting the learning

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/egg_roulette/physics_validation.png" title="Physics validation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

- On an isolated two-pad rig, MuJoCo's default solver settings (pyramidal cone, `impratio=1`) let an egg held at
  twice the friction limit slide 13 mm in half a second. With elliptic cones and `impratio=10` it settles 0.45 mm
  and stops, a clean Coulomb transition.
- The critical squeeze for a fast lift is the same to 3 decimals from 0.25 to 8 ms timesteps for Euler,
  implicitfast and RK4, and within 2% of rigid-body theory.
- On the full robot, the heaviest egg held grows linearly with squeeze, with an effective friction coefficient of
  0.53 holding still and 0.42 while carrying. That measured envelope sets the task constants.

### Results

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/egg_roulette/gain_chart.png" title="Gain chart" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

With 10 robot demos plus the human touch demos, the robot moves 90% of eggs intact. With 100 robot demos and no human
data it moves 43%: operators squeeze by eye, so the policy averages a gentle grip and a firm one.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/egg_roulette/episode_anatomy.png" title="Episode anatomy" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The touch policy closes to under 1 N on a raw egg and holds it there. On a stone it keeps tightening as the load
comes on, past the 3.5 N the gripper needs.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/egg_roulette/ablations.png" title="Ablations" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

32 ablations show what else matters. Action chunks are required (a one-step policy stalls at the pauses in human
demos). The robot needs its own touch sensor: a glove-trained policy run on a servo-current estimate gets 5%. Load is
the useful touch channel, and glove-to-video sync matters more than force calibration.

The [README](https://github.com/GeoffreyBian/egg-roulette#readme) covers the robustness grid, eggs the policy never
saw, the modelling notes and the limitations: this is simulation, the glove wearer is a scripted controller fitted to
real glove data, and policies see state rather than pixels.
