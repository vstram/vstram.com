.. title: Anylogic: Discrete Event Simulation - Parametric Analysis - Part 03
.. slug: anylogic-discrete-event-simulation-part-03
.. author: vstram
.. date: 2020-05-11 17:35:35 UTC-03:00
.. tags: en, Discrete Event Simulation

Previously, the modeling in Anylogic of a simplified manufacturing system composed of a single step was presented. In addition, we introduced a way to measure the performance of this system, by measuring the production time and the count of manufactured parts. In this article we will show how to parameterize this system so that it is possible to change some variables and analyze the impact of these changes on the process during the model simulation.


.. TEASER_END

.. sidebar:: Contents

    .. contents::

=========
Objective
=========

Parameterize the process modeled in Anylogic 8.5.2 so that it's possible to change process variables during the simulation of the model, thus allowing to analyze the system's behavior under conditions different from those initially chosen.

===================
Process Description 
===================

1. The process is basically the same as the previous article.

==============
Considerations 
==============

1. The availability of raw material and the production time on the machine must be changed;
2. Such variation must respect pre-established limits.

==================
Process Parameters 
==================

1. Raw material availability rate: ``exponential, initial value = 1 piece/min``, allow a variation of ``+/- 15%``;
2. Machine production capacity: ``constant, initial value = 1 piece/min``, allow variation of ``+/- 50%``.

=========
Procedure
=========

1. Open the Anylogic project ``des02``. Save it with another name: ``des03``. Thus, we will be able to continue where we left off;
2. From the ``Agents`` palette, drag a ``Parameter`` block onto the work area. Name it: ``sourceRawMaterial``;
3. In the ``Type`` field, choose ``Double``;
4. In the ``Default value`` field, set ``1``
5. Drag a new ``Parameter`` block next to the previous one, but this time name it: ``machineProduction``. Repeat steps ``3`` and ``4`` above for this parameter created.
6. Now we will link these parameters to the ``source`` and ``machine`` blocks created in the previous articles. Select the ``source`` block and set ``sourceRawMaterial`` to ``Arrival rate``;
7. Select the block ``delay`` and set ``machineProduction`` to ``Delay time``;
8. Finally, we will create the graphical interface controls that will allow us to modify the parameter values during the simulation. For this, we will use the ``Controls`` palette. Drag the ``Slider`` control next to the ``sourceRawMaterial`` parameter.
9. Set the name as: ``slider_sourceRawMaterial``. Select the ``Link to:`` checkbox, and choose ``sourceRawMaterial`` from the list.
10. In the ``Minimum value`` field, set ``0.85``. And in ``Maximum value``, set ``1.15``. This is the range that the slider control will allow the ``sourceRawMaterial`` parameter to vary.
11. Drag another ``Slider`` control, this time next to the ``machineProduction`` parameter, and name it as : ``slider_machineProduction``. Select the ``Link to:`` checkbox, and choose ``machineProduction`` from the list.
12. In the ``Minimum value`` field, set ``0.5``. And in ``Maximum value``, set ``1.5``. This is the interval that the slider control will allow the ``machineProduction`` parameter to vary.

.. image:: /images/des_03.png

13. There you go! Start the simulation with ``F5`` and then click ``Play``.
14. During the simulation it is possible to adjust the parameter values within the pre-established limits. Modify and observe the results through the graphs.

================
Process Analysis 
================

O video abaixo mostra a gravação da simulação do processo modelado no Anylogic:

.. raw:: html

    <video src="/videos/des03.mp4" width="1094" height="738" controls preload></video>

Through the slider controls, it is possible to modify the parameters previously defined for this process, within the permitted limits. After the start of the simulation, observe the impact of the variation of the parameters in the production time distribution graph and in the graph that accompanies the number of pieces that pass through the ``source`` and ``delay`` blocks. The size of the parts queue is the most visible result of changing the parameters. Eventually, the queue comes close to the ``50`` piece limit, when a change is quickly made to the ``machineProduction`` parameter, reducing the production time to consume excess pieces in the queue.

It is possible to create parameters not only related to the process itself (raw material supply/transport capacity, production capacity of a machine), but also parameters related to costs, for example.

If for this simplified process it is already possible to make several interesting analyzes, imagine for a model of a complex production line, in which the manager needs to evaluate the impact of this modification and present the results of these modifications in a meeting with directors. Certainly a well done simulation can help to convince a change in the production line.

And that's it! In the next articles we will continue to bring some complexities to the modeled process. See you there!

=========
Resources
=========
1. To model the manufacturing process - https://www.anylogic.com/
2. To edit the figures - https://www.gimp.org/
3. Video capture - https://screencast-o-matic.com/
4. To download the Anylogic modeled process - `Clique Aqui </anylogic/DES03/DES03.alp>`_

