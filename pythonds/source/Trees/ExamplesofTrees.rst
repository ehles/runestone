..  Copyright (C)  Brad Miller, David Ranum, Jeffrey Elkner, Peter Wentworth, Allen B. Downey, Chris
    Meyers, and Dario Mitchell.  Permission is granted to copy, distribute
    and/or modify this document under the terms of the GNU Free Documentation
    License, Version 1.3 or any later version published by the Free Software
    Foundation; with Invariant Sections being Forward, Prefaces, and
    Contributor List, no Front-Cover Texts, and no Back-Cover Texts.  A copy of
    the license is included in the section entitled "GNU Free Documentation
    License".

Примеры деревьев
-----------------

Теперь, после знакомства со стеком и очередью, а также после получения опыта работы с рекурсией, мы рассмотрим распространённую структуру данных под названием **дерево**. Деревья используются во многих областях информатики, включая операционные системы, графику, базы данных и компьютерные сети. Эта структура имеет много общего со своими растительными тёзками. У неё есть корень, ветви и листья. Разница между деревьями в природе и в информатике заключается в том, что у последних корень расположен на самом верху, а листья - в самом низу.

Перед тем, как начать изучение этой структуры данных, давайте рассмотрим несколько рапространённых примеров деревьев. Первый из них - классификационное дерево из биологии. :ref:`Рисунок 1 <fig_biotree>` демонстрирует пример биологической классификации некоторых видов животных. Хоть он и прост, но из него можно извлечь несколько свойств деревьев. Первое, что показывает рисунок, - это иерахичность дерева. Под этим подразумевается структурирование по уровням. Те из них, что содержат более общую информацию, раполагаются ближе к верху, а чем данные более специализированы, тем они ниже. Верх в иерархии занимают царства, уровнем ниже ("дети" предыдущего уровня) находятся типы, затем классы и так далее. Однако, неважно, как глубоко мы спускаемся по классификационному дереву, - все представленные на нём организмы принадлежат животному миру.

.. _fig_biotree:

.. figure:: Figures/biology.png
   :scale: 50%
   :align: center
   :alt: image

   Рисунок 1: Таксономия некоторых широко рапространённых животных, показанная в виде дерева.

Обратите внимание: вы можете начать от верхушки дерева и пройти по кружкам и стрелочкам до самого низа. На каждом уровне можно задать себе вопрос и проследовать по пути, содержащему ответ на него. Например, так: "Это животное принадлежит хордовым или членистоногим?" Если первое - то идём влево и снова спрашиваем: "Это хордовое относится к млекопитающим?" Если нет, то мы зашли в тупик (правда, только в этом упрощённом примере). На уровне "млекопитающие" вопрос звучит как "Это млекопитающее - примат или плотоядное?" Так мы можем двигаться, пока не дойдём до самого низа дерева, где получим конкретное название животного.

Вторым свойством деревьев является то, что все потомки одного узла независимы от потомков другого. Например, род Felis имеет детей Domestica и Leo. У рода Musca тоже есть потомок по имени Domestica, но это совершенно другой узел, и он независим от ребёнка Felis. Это означает, что можно изменять узел, являющийся потомком Musca, не затрагивая при этом детей узла Felis.

Третье свойство заключается в том, что каждый лист уникален. Мы можем проложить путь от корня к листу, и он будет однозначно идентифицировать каждое существо из царства животных. Например, Animalia
:math:`\rightarrow` Chordate :math:`\rightarrow` Mammal
:math:`\rightarrow` Carnivora :math:`\rightarrow` Felidae
:math:`\rightarrow` Felis :math:`\rightarrow` Domestica.

Другой пример дерева, который вы вполне вероятно используете ежедневно, это файловая система. В ней директории (папки) структурированы в виде дерева. :ref:`Рисунок 2 <fig_filetree>` иллюстрирует небольшую часть из иерархии файловой системы Unix.

.. _fig_filetree:

.. figure:: Figures/directory.png
   :scale: 50%
   :align: center
   :alt: image

   Рисунок 2: Маленькая часть иерархии файловой системы Unix.

   Дерево файловой системы имеет много общего с деревом биологической классификации. Вы можете проложить путь от корня в любую директорию. Он будет идентифицировать её (и все файлы в ней) уникальным образом. Другое важное свойство деревьев, следующее из их иерархической природы, это то, что возможно перемещать целые секции (**поддеревья**) на различные позиции, не затрагивая при этом нижние уровни. Например, мы можем взять поддерево, начинающеся с /etc/, отцепить etc/ от корня и прикрепить к usr/. Это изменит уникальный путь для httpd с /etc/httpd на /usr/etc/httpd, но не повлияет на содержимое или любого из потомков директории httpd.

   Последний пример дерева - это обычная веб-страница. Рассмотрим следующую страничку, написанную на HTML. :ref:`Рисунок 3 <fig_html>` демонстрирует дерево, связывающее все HTML теги, использованные при её создании.

   ::

    <html xmlns="http://www.w3.org/1999/xhtml" 
	  xml:lang="en" lang="en">
    <head>
	<meta http-equiv="Content-Type" 
	      content="text/html; charset=utf-8" />
	<title>simple</title>
    </head>
    <body>
    <h1>A simple web page</h1>
    <ul>
	<li>List item one</li>
	<li>List item two</li>
    </ul>
    <h2><a href="http://www.cs.luther.edu">Luther CS </a><h2>
    </body>
    </html>


.. _fig_html:

.. figure:: Figures/htmltree.png
   :align: center
   :alt: image

   Figure 3: Дерево, связывающее элементы разметки веб-страницы.

Исходный HTML-код и связанное с ним дерево иллюстрируют другой вид иерархии. Обратите внимание, что каждый уровень дерева связан с уровнем вложенных HTML-тэгов. Первый тэг в исходнике - ``<html>``, последний - ``</html>``. Все оставшиеся тэги лежат внутри этой пары. Если вы проверите, то убедитесь, что это свойство вложенности истинно для всех уровней дерева.
