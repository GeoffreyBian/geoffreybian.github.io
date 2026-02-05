---
layout: page
title: Grid Aware Cloud
description: Optimization of Battery Energy Storage Systems (BESS) for data center cost reduction and grid stability.
# img: assets/img/bess_optimization.jpg
importance: 2
category: Research
---

`September 2025 – December 2025`

Geoffrey Bian, UREP Affiliate, with Zihan Pan (PhD Candidate), and Mohammad Shahrad (Assistant Professor)
**Affiliation:** [UBC Cloud Infrastructure Lab (CIRRUS)](https://cirrus.ece.ubc.ca/), University of British Columbia

### Project Overview
As data center electricity demand surges due to AI and cloud computing, managing grid constraints and volatile wholesale prices has become critical. **Grid Aware Cloud** investigates the physical side of energy management using Battery Energy Storage Systems (BESS) as a co-located buffer for data center loads. This project specifically models the sizing and daily operation of BESS to minimize the total cost of ownership by balancing energy procurement with battery health.



### Technical Insights: Linear Programming & Optimization
I developed a linear programming (LP) formulation in **Python** using the **PuLP** library to solve for the optimal energy capacity (E_cap) and hourly dispatch schedule. Unlike static models, this framework treats battery degradation as a throughput-based cost, effectively converting capital expenditure (CAPEX) into a usage-dependent operating expense (OPEX).

* **Objective Function**: Minimizes the sum of grid electricity costs, cycling degradation costs, and amortized capacity costs.
* **Constraints**: Enforces energy balance (state-of-charge), power balance (grid vs. load), and C-rate limits to ensure the simulation remains physically realistic.
* **Data Grounding**: Evaluated using **Google data center power traces** and real-time electricity price signals from **ComEd** and **Dominion**.



### Application & Results
The simulation demonstrated that a co-located BESS can achieve net daily savings of approximately **31.88%** compared to a grid-only baseline. By charging during low-price or negative-price intervals and discharging during peak demand, the system exploits price arbitrage while naturally limiting excessive cycling that would prematurely degrade the battery. This methodology provides a scalable framework to compare physical storage against software-based workload shifting.

---

### Project Links
* **GitHub Repository:** [grid-cloud-migration-estimates](https://github.com/ubc-cirrus-lab/grid-cloud-migration-estimates)
* **Full Report (PDF):** [Optimal Sizing and Operation of BESS](/assets/pdf/BESS.pdf)