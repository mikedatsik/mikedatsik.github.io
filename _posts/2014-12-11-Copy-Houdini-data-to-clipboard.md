---
layout: post
title: Copy Houdini data to clipboard.
excerpt_separator: <!--more-->
---

У меня что-то случилось со сценами в которых я работал
и мне нужно было перенести данные из них во вновь созданные. Houdini любезно предоставляет возможность копировать все что только захочется в свой буфер обмена, но оказалось что есть данные которые сложно перенести, собственно я говорю про Bundles, которые я часто использую.
<!--more-->

Решение нашел через простой модуль к python — pyperclip (https://pypi.python.org/pypi/pyperclip/).

Считал все Bundles вместе с содержимым с одной сессии houdini и вставил в другую.

Думаю можно придумать массу интересных применений для этого модуля.

<center>Ссылка на Github:</center>

<center><a href="https://github.com/mikedatsik/HoudiniClip" class="myButton">Download</a></center>