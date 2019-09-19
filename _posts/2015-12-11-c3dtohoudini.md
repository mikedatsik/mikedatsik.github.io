---
title: "Import .C3D to Houdini."
date: 2014-12-11
permalink: /posts/2014/12/11/c4dtohoudini
tags:
  - vfx
  - supervision
  - houdini TD
  - film
  - post-production
  - python
  - mocap
  - vicon
excerpt: ""
layout: single
toc: true
---

### Abstract

I will briefly describe the history of the project and why did I importer of .C3D files in Houdini, if you don't have time to read all this text, at the bottom of the post there is a short description and a link to the tool.
{: .text-justify .text-ident}

Recently there was a project where we had to create a system that allows us to create content for TV broadcasts in the shortest possible time, which will contain people-like animals. Since our team had little experience with character animation in general and with facial animation in particular, we had to read a lot of information on existing solutions and mathematics related to this issue. In this case, it was necessary to automate the process of following the data along the entire production chain: from filming (live-action + mocap) to actually obtaining the finished result.
{: .text-justify .text-ident}

### Process

As a result, we were inspired by Gollum from The Lord of the Rings, the guys from Weta Digital created a tricky system based on mixing various blandshapes of the hero’s face according to certain laws. We have our own mocap studio and we began to work closely with them. We managed to shoot simultaneously 2 data streams: data on the position of points on key nodes of the face, which gave us the opportunity to create a model of mixing states, data on the movement of the body and head.
{: .text-justify .text-ident}

We were given 2 types of data from Vicon Blade (fbx with the behavior of the head and c3d with points in space). Our main software is Sidefx Houdini, it did a great job with fbx data, but unfortunately it could not be read .C3D, the search for a ready-made solution failed. On the site of the format developer, I found several Python modules that can process this data type. I took them as a basis for my tool.
{: .text-justify .text-ident}

<iframe src="https://www.youtube.com/embed/UZG8iktpp9Y" width="560" height="315" frameborder="0"> </iframe>

After all data was successfully imported into Houdini, we made an asset which all information was loaded. Houdini has enormous potential, not only for creating graphics, but also as a tool for solutions architect. Asset analyzes the distances between the key points of the resulting animation and mixes various states of the hero’s face according to masks and laws (we had to make about 40 such states until we were satisfied with the result). It is also possible to improve automatic process with animating individual links.
{: .text-justify .text-ident}

There were problems with data synchronization (2 mocaps and a video), we solved it. Here is the link to the announcement: http://postmodern.com.ua/blogs/view/33
{: .text-justify .text-ident}

We already have a working prototype and understanding of all production processes, we plan  to design, in the near future, a certain product with even greater speed and better quality.
{: .text-justify .text-ident}

### Result

Actually this is tool for import C3D into Houdini. This is what the import process looks like:
{: .text-justify .text-ident}

![c3dtohoudini](/assets/images/blog/2015-12-11-c3dtohoudini/c3dtohoudini.png)

I implemented 2 types of imports for different tasks:
{: .text-justify .text-ident}

* An array of points to which data is written, including the name of each marker
* Group of Null nodes with the name for each marker.
![diffrent_types_c3d](/assets/images/blog/2015-12-11-c3dtohoudini/diffrent_types_c3d.png)

Video example of ready-to-work data:
{: .text-justify .text-ident}

<iframe src="https://www.youtube.com/embed/Dy6_l7fX0K0"></iframe>
<center>Link to GitHab:</center>
<center><a href="https://github.com/mikedatsik/C3DtoHoudini" class="myButton">Download</a></center>