---
title: "Вышел «Полярный Рейс», новый фильм над которым я работал."
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
# Предистория:

Для меня всегда было большой проблемой перенести камеру из Houdini в Nuke. Все попытки использовать fbx, по каким-то причинам, постоянно приводили к сбоям, переворачиванию направлений осей координат и неправильной анимации.
{: .text-justify .text-ident}

Я видел достаточно много скриптов переносящих камеру из Maya, Blender и т.д., но так как я работаю в Houdini я решил сделать себе удобный инструмент для этого.
{: .text-justify .text-ident}

Основным толчком для меня стало открытие широких возможностей по хранению данных в exr файлах. Exr являтся основным форматом изображений в котором работаю я и мои колеги. Я подумал, если рендерить картинку для композа сразу с информацией о камере, которую в свою очередь всегда можно прочитать а Nuke. При этом отпадают проблемы с несовпадением версий камеры и рендера, т.к. каждый готовый кадр будет нести актуальную информацию о том, с какой камеры от был посчитан.
{: .text-justify .text-ident}

Почитав немного о наследовании трансформации в Houdini, а зачастую мы анимируем камеру всеми доступными способами, с помощью Aim или используем дополнительные паренты и нули, я понял что для решения задачи переноса камеры нужно использовать матрицы трансформации. В любом пакете, который имеет отношение к 3D вычисление положения и поворота в пространстве описывается в виде матрицы трансформации(они бывают мировыми(worldMatrix) и локальными). Система координат Эйлера дает нам более понятное понимание визуального процесса работы с 3Д объектом, но при экспорте данных с одного пакета в другой, намного проще воспользоваться матрицами, которые дают нам возможность получить позицию объекта и его поворот(а еще сжатие и размер(для твердотельных объектов важные данные но не для камеры)) не зависимо от того, каким образом мы воздействовали на него для получения движения или позиции. Мы всегда можем преобразовать матрице и получить любую компоненту трансформации(transform, rotate, scale…)
{: .text-justify .text-ident}

Я не буду вдаваться в математический аспект данной истории, если интересно изучить подробнее, ниже я привел материалы которые я использовал:
{: .text-justify .text-ident}

* <http://en.wikipedia.org/wiki/Transformation_matrix>
* [http://www.sidefx.com/docs/houdini13.0/hom/hou/ ObjNode#worldTransform](http://www.sidefx.com/docs/houdini13.0/hom/hou/ObjNode#worldTransform)
* [http://docs.thefoundry.co.uk/nuke/63/pythonreference/ _nukemath.Matrix4-class.html](http://docs.thefoundry.co.uk/nuke/63/pythonreference/_nukemath.Matrix4-class.html)


# Процесс:

## Houdini:

Для того, чтобы записать камеру в exr нужно создать expression в Mantra Node, который в поле «exr/comments» вписывает значения матрицы положения в мировых координатах, а также Focal Length и Aperture выбранной в данной mantra node камеры. Выглядит это так:
{: .text-justify .text-ident}

![cam_exp_mantra](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/cam_exp_mantra.png){: .align-center}

``` python
`pythonexprs("hou.node(hou.parm('camera').eval()).worldTransform().asTuple()")``pythonexprs("hou.parm(hou.parm('camera').eval()+'/focal').eval()")``")"``pythonexprs("hou.parm(hou.parm('camera').eval()+'/aperture').eval()")`
```

Для удобства я сделал shelf, который при необходимости заполняет это поле для меня:
{: .text-justify .text-ident}

![cam_exp_mantra_shell1](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/cam_exp_mantra_shell1.png){: .align-center}

![cam_exp_mantra_shell2](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/cam_exp_mantra_shell2.png){: .align-center}

## Nuke:

Чтобы создать камеру в Nuke на основе записанных нами данных, выполняем скрипт, который считывает в каждом кадре, на протяжении всесго отрезка существования сиквенции, анимацию и ставит ключи на камеру.
{: .text-justify .text-ident}
На практике это выглядит так:

1. Выполняем скрипт:

![nuke_res](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/nuke_res.png){: .align-center}

2. Получаем камеру с анимацией:

![nuke_res2](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/nuke_res2.png){: .align-center}

![nuke_res3](/assets/images/blog/2015-12-11-houdini-to-nuke-exr-camera/nuke_res3.png){: .align-center}


<center>Ссылка на Github:</center>

[Download](https://github.com/mikedatsik/HouCameraToNuke){: .btn .btn--info .btn--bcenter }