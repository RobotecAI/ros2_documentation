.. redirect-from::

    Tutorials/Simulators/O3DE/Setting-up-a-Robot-Simulation-O3DE
    Tutorials/Advanced/Simulators/O3DE

Setting up a robot simulation (Basic)
=====================================

**Goal:** Setup a robot simulation and control it from ROS 2.

**Tutorial level:** Advanced

**Time:** 20 minutes

.. contents:: Contents
   :depth: 2
   :local:

Background
----------

In this tutorial you will extend the project created in the first tutorial: :doc:`./Installation-Ubuntu`.
The aim is to learn how O3DE Editor works and how it can be used to modify the simulation scene, existing robots, and ROS 2 interfaces.

Prerequisites
-------------

This is a continuation of the first part of the tutorial: :doc:`./Installation-Ubuntu`.
It is mandatory to start with the first part to ensure the project is based on the correct template and build successfully.

Sample simulation modifications using O3DE Editor
-------------------------------------------------

1. Quick tour over O3DE Editor and ``rosbot_xl`` prefab
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- explain entity outlier, inspector, asset browser, list ROS2 components of ``rosbot_xl`` prefab

2. Updating ``rosbot_xl`` prefab
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- add camera to ``rosbot_xl``

3. Add ``rosbot_xl_slamtec`` prefab to the scene
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- add overrides to make two robots different

4. Add ROS2 spawner to the scene
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- add spawner, spawn multiple robots
