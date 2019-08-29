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


У меня что-то случилось со сценами в которых я работал и мне нужно было перенести данные из них во вновь созданные. Houdini любезно предоставляет возможность копировать все что только захочется в свой буфер обмена, но оказалось что есть данные которые сложно перенести, 
собственно я говорю про Bundles, которые я часто использую.
{: .text-justify .text-ident}

Решение нашел через простой модуль к python — [Pyperclip](https://pypi.python.org/pypi/pyperclip/).
{: .text-justify .text-ident}

Считал все Bundles вместе с содержимым с одной сессии houdini и вставил в другую.
{: .text-justify .text-ident}

Думаю можно придумать массу интересных применений для этого модуля.
{: .text-justify .text-ident}

<center>Ссылка на Github:</center>

[Download](https://github.com/mikedatsik/HoudiniClip){: .btn .btn--info .btn--bcenter }