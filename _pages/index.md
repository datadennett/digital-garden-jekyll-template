---
layout: page
title: Home
id: home
permalink: /
---

# Welcome! 🌱

Welcome! I'm Nat Dennett, and this is my digital knowledge garden. Come take a stroll! It's still a little sparse for now, but I'm planting more seeds every day. My hope is that you'll find plentiful fruit to pluck off the vines: ideas you can use about data analysis, business intelligence, and language learning.

## Languages
[[Why I love Learning Languages]]

## Data Analysis
[[SQL Tips and Tricks]]

## Programming
[[MacOS hidden folders]]

<strong>Recently updated notes</strong>

<ul>
  {% assign recent_notes = site.notes | sort: "last_modified_at_timestamp" | reverse %}
  {% for note in recent_notes limit: 5 %}
    <li>
      {{ note.last_modified_at | date: "%Y-%m-%d" }} — <a class="internal-link" href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a>
    </li>
  {% endfor %}
</ul>

<style>
  .wrapper {
    max-width: 46em;
  }
</style>
