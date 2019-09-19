---
title: "Copy Houdini data to clipboard."
date: 2014-12-11
permalink: /posts/2014/12/11/Copy-Houdini-data-to-clipboard
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


Something happened with my scenes and I needed to transfer the data from them to the newly created ones.  Houdini kindly provides the ability to copy everything that you want to your clipboard, but there is data that is difficult to transfer, actually I'm talking about the Bundles, which I often use.
{: .text-justify .text-ident}

Found a solution through a simple module in python — [Pyperclip](https://pypi.python.org/pypi/pyperclip/).
{: .text-justify .text-ident}

Read all the Bundles along with the content from one houdini session and inserted into another.
{: .text-justify .text-ident}

I think you can create a lot of interesting applications with this module.
{: .text-justify .text-ident}

<center>Link on Github:</center>

[Download](https://github.com/mikedatsik/HoudiniClip){: .btn .btn--info .btn--bcenter }