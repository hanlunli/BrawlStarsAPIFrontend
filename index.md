---
layout: base
title: Course Outlines
image: /images/mario_animation.png
hide: true
---

<!-- Liquid:  statements -->

<!-- Include submenu from _includes to top of pages -->
{% include nav_home.html %}
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %} 

Investing in Your Technical Future

Explore the Computer Science Pathway at Del Norte High School. All Del Norte CompSci classes are designed to provide a real-world development experience. Grading is focused on time invested, analytics, participation with peers, and engagement in learning.

- Project-based learning with teacher support
- Tech Talks by teacher complimented with Student Teaching
- Course learning includes Coding Languages, DevOps, GitHub, Research and Creativity
- Student teams practice Agile Development Methodologies: planning, communication, collaboration
- Class lab time provided and approximately 2-3 hours of homework per week