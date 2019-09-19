---
title: "Export camera from Houdini to Nuke using EXR"
date: 2015-12-11
permalink: /posts/2015/12/11/houdini-to-nuke-exr-camera
tags:
  - vfx
  - supervision
  - houdini
  - nuke
  - film
  - post-production
  - python
excerpt: ""
layout: single
toc: true
---
# Abstract:
It was always a big problem for me to move the camera from Houdini to Nuke. All attempts to use fbx, for some reason, constantly led to crashes, inverting the directions of the coordinate axes and incorrect animation.
{: .text-justify .text-ident}

I saw a lot of scripts transferring the camera from Maya, Blender, etc., but since I work in Houdini I decided to make it for Houdini.
{: .text-justify .text-ident}

The main reason for doing this tool was the wide range possibilities for storing data in exr files. Exr is the main image format which I and my colleagues working with. I thought, if you render a picture for a compositing with information about the camera, which can always be read in Nuke. In this case, there are no problems with the mismatch between the camera and render versions, because Each finished frame will carry up-to-date information about form which camera frame was rendered.
{: .text-justify .text-ident}

After some research in Houdini transformation, we often animate the camera in all available ways, using Aim, additional parents and Nulls, I have realized that to solve the camera transfer problem, we need to use transformation matrices. In any package that is related to 3D, the calculation of the position and rotation in space is described as a transformation matrix (they are world (worldMatrix) and local). The Euler coordinate system gives us a better understanding of the visual process of working with a 3D object, but when exporting data from one package to another, it is much easier to use matrices, that give us the opportunity to get the position of the object and its rotation (as well as compression and size (for solid objects) important data but not for the camera)) regardless of how we acted on it to obtain movement or position. We can always transform the matrix and get any transformation component (transform, rotate, scale ...)
{: .text-justify .text-ident}

I will not go into the mathematical aspect of this story, if it is interesting to study in more detail, below I gave the materials that I used:
{: .text-justify .text-ident}

* <http://en.wikipedia.org/wiki/Transformation_matrix>
* [http://www.sidefx.com/docs/houdini13.0/hom/hou/ ObjNode#worldTransform](http://www.sidefx.com/docs/houdini13.0/hom/hou/ObjNode#worldTransform)
* [http://docs.thefoundry.co.uk/nuke/63/pythonreference/ _nukemath.Matrix4-class.html](http://docs.thefoundry.co.uk/nuke/63/pythonreference/_nukemath.Matrix4-class.html)

# Process:

## Houdini:

INFO: For now it worked only for Mantra, but it's no problem to make it for other renderers(Arnold, etc.)
{: .notice--success .text-justify}

To record a camera in exr, you need to create an expression in the Mantra Node, which in the field «_exr/comments_» enters the values of the position matrix in world coordinates, as well as the Focal Length and Aperture of the camera selected in this mantra node. It looks like this:
{: .text-justify .text-ident}

![cam_exp_mantra](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/cam_exp_mantra.png){: .align-center}

``` python
`pythonexprs("hou.node(hou.parm('camera').eval()).worldTransform().asTuple()")``pythonexprs("hou.parm(hou.parm('camera').eval()+'/focal').eval()")``")"``pythonexprs("hou.parm(hou.parm('camera').eval()+'/aperture').eval()")`
```

I made a shelf, which, if necessary, fills this field for me:
{: .text-justify .text-ident}

![cam_exp_mantra_shell1](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/cam_exp_mantra_shell1.png){: .align-center}

![cam_exp_mantra_shell2](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/cam_exp_mantra_shell2.png){: .align-center}

## Nuke:

To create a camera in Nuke based on the data from exr, we execute a script that reads data for each frame and puts keys on camera.
{: .text-justify .text-ident}
In practice, it looks like this:

1. Execute script:

![nuke_res](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/nuke_res.png){: .align-center}

2. We get camera with animation:

![nuke_res2](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/nuke_res2.png){: .align-center}

![nuke_res3](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/nuke_res3.png){: .align-center}

<center>Link on Github:</center>

[Download](https://github.com/mikedatsik/HouCameraToNuke){: .btn .btn--info .btn--bcenter }