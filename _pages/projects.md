---
layout: page
title: projects
permalink: /projects/
description: >
  A collection of systems-level projects exploring embedded software, controls,
  distributed systems, and applied machine learning. These projects reflect my
  interest in building reliable software that interfaces with real hardware,
  physical processes, and large-scale infrastructure.
nav: true
nav_order: 2
display_categories: [Research, Projects]
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {%- for category in page.display_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
<!-- Display projects without categories -->
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
<p class="cover-credits">Cover photos from Wikimedia Commons:
GreenPASS, <a href="https://commons.wikimedia.org/wiki/File:Google_Data_Center,_Council_Bluffs_Iowa_(49062863796).jpg">Chad Davis</a> (CC BY 2.0);
Grid-Aware Cloud, <a href="https://commons.wikimedia.org/wiki/File:High_voltage_transmission_tower_and_lines._Auburn_WA.jpg">Ron Clausen</a> (CC0);
Wings, <a href="https://commons.wikimedia.org/wiki/File:Eurasian_magpie_2024_03_03_02.jpg">Alexis Lours</a> (CC BY 4.0). Cropped.</p>
</div>
