---
layout: page
title: Egg Roulette
description: "MuJoCo study on the SO-101: can a robot learn grip force from people in a touch glove?"
img: assets/img/covers/egg_roulette.jpg
importance: 2
category: Projects
---

`November 2026` · [Code, data and every figure on GitHub](https://github.com/GeoffreyBian/egg-roulette) · **[Run the simulation in your browser](https://geoffreybian.github.io/egg-roulette/)**

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

### Run it yourself

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <a href="https://geoffreybian.github.io/egg-roulette/">{% include figure.html path="assets/img/egg_roulette/live_sim.jpg" title="The live simulator: two policies on the same carton" class="img-fluid rounded z-depth-1" %}</a>
    </div>
</div>
<div class="caption">
    <a href="https://geoffreybian.github.io/egg-roulette/">Open the live simulator</a>. Works on phones too.
</div>

The [live version](https://geoffreybian.github.io/egg-roulette/) runs the same MuJoCo model in your browser,
compiled to WebAssembly and stepped at 500 Hz, with the trained policies running at 30 Hz. Nothing is
pre-recorded. By default each policy sees two 64x64 camera images, ray-cast from the MuJoCo scene in the
browser, and has to find the egg itself. A corner inset shows the images it got, with a heat map of the
pixels that most change its next action. You pick how the robot was trained: any of the 16 policies from the gain chart, or one of six
ablation recipes (no action chunks, glove lagging the video, pressure-only touch). Then you change what it
faces: eggs it never trained on, your own egg weight and crack force, slippery pads, a noisier camera, or
the touch sensor unplugged. Shift-drag an egg to push it with a spring force, show the contact forces and
collision geometry, and scrub back through the run. A parity test checks the JavaScript port against the
Python code. The browser's camera images match Python's on all but 0.01% of colour values, the actions match to
2e-7 given the same inputs, and the success rates on fresh eggs agree within sampling noise.

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

### From cameras instead of egg position

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/egg_roulette/gain_pixels.png" title="Gain chart from cameras" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The main results give the policy the egg's position. I retrained all 48 policies of the gain sweep (3 seeds) on two
64x64 cameras instead, a workspace view and the wrist camera, with a small CNN that turns each image into 32
keypoints. Touch still adds most of its lift: 41 points over robot demos alone from cameras, against 47 from egg
position. The 6-point gap shows up at every data size, but with 3 seeds its 95% interval is -3 to 15, so it may
be noise. All of it is on the touch side: without touch, cameras change nothing (43% vs 44%), while the touch
policy goes from 90% to 85%, mostly from cracking more raw eggs. One caveat favours touch here: the human demos
are rendered with the robot's gripper in place of the hand, which a real glove dataset would not get for free.

The [README](https://github.com/GeoffreyBian/egg-roulette#readme) covers the robustness grid, eggs the policy never
saw, the modelling notes and the limitations: this is simulation, the glove wearer is a scripted controller fitted to
real glove data, and the cameras are flat-shaded and noise-free.
