---
layout: page
title: my teaching portfolio
permalink: /teaching/
description:
nav: true
nav_order: 5
display_categories: [Me as a teacher]
horizontal: false
---

<div style="background-color: #424246; border: 1px solid #424246; padding: 15px; border-radius: 10px; margin-bottom: 20px;">
  <h2>Welcome to my teaching portfolio!</h2>
  <p>This page provides an overview of my approach to teaching, the courses I have taught, and feedback from my students.</p>
  <p>My goal as an educator is to inspire and empower students, fostering a deep understanding and appreciation of the subjects I teach.</p>
  <p>Below, you will find detailed information on my teaching philosophy, the courses I've been involved with, and evaluations from my students.</p>
</div>

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
</div>
