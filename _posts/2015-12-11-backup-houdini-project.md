---
title: "Backup Houdini Project."
date: 2014-12-11
permalink: /posts/2014/12/11/backup-houdini-project
tags:
  - vfx
  - supervision
  - houdini TD
  - film
  - post-production
  - python
excerpt: ""
layout: single
toc: true
---
A simple script with an interface for scene backup that runs through all the nodes in the project, unpacks the relative paths, replaces them with a new path, and copies what the path refers to specified folder, sorting it by content.
{: .text-justify .text-ident}

After that, replace everything with $HIP. Everything is extremely simple, but more than once saved life at work.
{: .text-justify .text-ident}

Works with all types of nodes. Last renders with mantra nodes will also be preserved.
{: .text-justify .text-ident}

<center>Link to Github:</center>

[Download](https://github.com/mikedatsik/CollectHoudiniProject){: .btn .btn--info .btn--bcenter }