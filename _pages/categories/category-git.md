---
layout: archive
title: "깃"
permalink: categories/git
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Git %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}