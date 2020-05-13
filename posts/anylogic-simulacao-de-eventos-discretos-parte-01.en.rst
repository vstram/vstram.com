.. title: Anylogic Discrete Event Simulation - Simple Example - Part 01
.. slug: anylogic_discrete_event_simulation_01
.. author: vstram
.. date: 2020/04/30
.. tags: en, Discrete Event Simulation

Modeling of a simplified manufacturing process, composed by just a single step, using the Anylogic 8.5.2 software and the **Discrete Event Simulation** approach (DES). The process consists of one machine, processing a stream of raw materials that can be accumulated in a queue of limited capacity.

.. TEASER_END

.. image:: /images/man-wearing-gray-shirt-and-welding-mask-covered-in-welding.jpg

.. sidebar:: Contents

    .. contents::

=========
Objective
=========

Use Anylogic 8.5.2 to simulate the manufacturing process of a product, composed of a single step. The Discrete Event Simulation approach is adopted.

===================
Process Description
===================

1. Process starts with the raw material being fed by a constant supply flow;
2. The machine processes this raw material, transforming it into a final product;
3. This raw material can accumulate in a queue nearby the machine;

==============
Considerations
==============

1. Process designed without operators. Once the raw material approaches the machine, it's loaded instantly for processing. Likewise, as soon as the raw material is transformed into a finished product, it's immediately transported to the stock. There are no delays in loading/unloading parts on the machine;
2. There are no variations in the machine's production performance (due to wear of tools or parts). The machine does not require repairs or adjustments during the entire production. The energy supplied by the electrical network remains stable and capable of meeting the machine's operation;
3. The quality of the raw material and the finished product after being processed by the machine are always considered ideal. There are no scraps;
4. There are no variations in the raw material supply capacity;
5. There are no transportation restrictions, either from raw material to the machine, or from finished products after the machine's production;
6. Dimensions and weights of both the raw material and the finished product are not being considered;

==================
Process Parameters  
==================

1. The raw material average supply Rate is ``1`` item per ``minute``;
2. The capacity for accumulating raw material parts nearby the machine is ``50`` items;
3. The machine is capable of transforming the raw material into finished product in a constant time of 60 seconds
4. The capacity of the machine is one part at a time.

=========
Procedure 
=========

1. Create a new model in Anylogic. Assign a name, such as: ``des01``;
2. Change the time unit from seconds to minutes. Click on ``Finish``;
3. We use the blocks available in the ``Process Modeling Library`` palette to model this process. Start by dragging a ``source`` block to the desktop;
4. Set the source block's ``Arrival Rate`` property to ``1`` item per ``minute``;
5. Drag a ``queue`` block next to the ``source`` tile. Note that they are automatically connected. Set the ``Capacity`` property to ``50``;
6. Drag a ``delay`` block next to the ``queue`` block. The ``delay`` block will model the machine responsible for processing the raw material into a final product. Set the ``Delay Time`` property to ``1 minute``;
7. Drag a ``sink`` block next to the ``delay`` block. The ``sink`` block is used to indicate the end of the process;
8. The modeling of this simplified process is done. Start the simulation by clicking on the ``Run Simulation`` button on the toolbar (or press F5);
9. The simulation screen appears. It is possible to start, pause, interrupt and adjust the speed of the simulation. Start the simulation by clicking on the ``Run`` button. Observe the variation of the numbers next to each block. They indicate the movement of items at the entrance, inside the block and at its exit.

.. figure:: /images/des_01.png

    Image showing Anylogic with the process model and some configuration screens

=================
Processo Analysis 
=================

This process was modeled to represent a perfectly balanced process, which would be the goal of every production manager. Although excessively idealized, it allows establishing benchmarks when compared to a real process. That is, it represents the maximum performance limit to which the process must be optimized.

Such reasoning (ideal x real comparison) can also be taken at each stage of the process, in such a way that it is possible to score the performance of each stage individually. Thus, once a certain stage of the process performs far below ideal, actions can be taken to verify and correct whatever is necessary.

Note that, during the simulation, a small queue of parts (raw material) eventually occurs. The machine cannot process all the flux of parts coming from the ``source`` block. This happens due the fact that raw material availability is given at an average rate of ``1`` part per ``minute``. According to the documentation, Rate is defined as:

    Rate: Used to schedule sporadic state changes with a known average time. (...) the time interval is determined by an exponential distribution parameterized with the given rate. For example, if the rate is 0.2, the intervals will have average values of 1/0.2 = 5 units of time

That is, it does not mean that the raw material is delivered every ``1`` constant minute. This is the only concession to the intention to model this process perfectly. The intention here was to observe the behavior of the queue over time.

In the next articles, I will bring this model to the harsh reality faced daily on the shop floor, gradually adding some of the most common difficulties encountered during the manufacture of products. I will also add in the model some ways to measure the performance of the process, because you cannot control something that is not measured.

Until then!

=========
Resources 
=========

1. https://www.anylogic.com/ - To model the manufacturing process
2. https://www.gimp.org/ - To edit the pictures
