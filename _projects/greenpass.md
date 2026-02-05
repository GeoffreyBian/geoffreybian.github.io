---
layout: page
title: GreenPASS optimization
description: Collaborative workload shifting framework designed to reduce data center carbon emissions without increasing user costs.
# img: assets/img/baja_can_dashboard.jpg
importance: 1
category: Research
---

`September 2025 – Present`

**Collaborators:** Zihan Pan (PhD Candidate), Mohammad Shahrad (Assistant Professor), Geoffrey Bian (UREP Affiliate)
**Affiliation:** [UBC Cloud Infrastructure Lab (CIRRUS)](https://cirrus.ece.ubc.ca/), University of British Columbia

### Research Summary
The core of our evaluation utilizes a simulation-based methodology scaled to cluster-level production traces from the **Alibaba v2020 GPU dataset**. By simulating workloads across four North American regions (Virginia, California, Texas, and Ontario), we analyzed the feasibility of shifting ~70,000 jobs based on Carbon Intensity (CI) and Locational Marginal Pricing (LMP).

Key findings from our research include:
* **Cost-Neutral Sustainability:** GreenPASS can achieve significant carbon reduction while eliminating the typical 4% to 10% cost overhead associated with user-managed shifting.
* **Data Access Synergy:** Our Duplication & Reuse policy demonstrates that co-locating data with shifted workloads is essential; reusing data across recurring jobs further reduces shifting costs and maximizes carbon savings.
* **Robustness Across Time:** Simulations spanning five years (2020–2024) confirm that carbon reduction remains consistent despite seasonal and annual variations in grid intensity and electricity prices.



### Publication Status
The paper detailing this framework and its evaluation is currently **pending approval** for the *17th ACM International Conference on Future and Sustainable Energy Systems ([ACM e-Energy 2026](https://energy.acm.org/conferences/eenergy/2026/))*.