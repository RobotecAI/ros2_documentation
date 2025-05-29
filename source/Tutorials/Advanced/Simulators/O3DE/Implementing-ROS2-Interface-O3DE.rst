Setting up a robot simulation (Advanced)
========================================

**Goal:** Learn the steps to set up and execute a ROS 2 topics and services in O3DE.

**Tutorial level:** Advanced

**Time:** 30 minutes

.. contents:: Contents
   :depth: 2
   :local:

Background
----------

In this tutorial you will extend the project created in the first tutorial: :doc:`./Setting-Up-Simulation-O3DE`. In particular, you will deep dive into the C++ implementation of the ROS 2 interfaces in O3DE. The aim is to learn how to implement ROS 2 topics and services in O3DE to control and interact with robots and simulation environments.

Prerequisites
-------------

This is a continuation of the first tutorial: :doc:`./Setting-Up-Simulation-O3DE`.
It is mandatory to create the project based on its instructions and to get the working environment before starting this part.

Creating a New ROS 2 Project
----------------------------

1. **Register the Template**:

Register the template with O3DE so that it can be used to create a new project.

From the root directory of your O3DE installation, run:

.. code-block:: bash

   ./scripts/o3de.sh register --all-templates-path <path_to_o3de_extras>/Templates

This command registers all templates in the ``o3de-extras`` repository, including the Robotic Manipulation Template.

2. **Create a New Project**:

Create a new project using the ROS 2 Robotic Manipulation Template:

.. code-block:: bash

   ./scripts/o3de.sh create-project --project-name <project_name> --template-name Ros2RoboticManipulationTemplate --project-path <path-to-project-directory>

This will generate a new project directory with the necessary files and configurations.

3. **Install Dependencies**:

Navigate to your project directory:

.. code-block:: bash

   cd <project_path>

Install the required Python packages and dependencies for the project. Typically, you will need to install ROS 2 and MoveIt dependencies. This can often be done with:

.. code-block:: bash

   sudo apt install ros-${ROS_DISTRO}-moveit ros-${ROS_DISTRO}-moveit-resources ros-${ROS_DISTRO}-depth-image-proc

Ensure that you also have any additional dependencies specified in the project's ``requirements.txt`` or equivalent configuration files.

4. **Configure and build the Project**:

After installing dependencies, cofigure and build the project using the following commands:

.. code-block:: bash

   cmake -B build/ -S . -G "Ninja Multi-Config"

.. code-block:: bash

   cmake --build <path-to-build-directory> --target <project_name> Editor

Ensure the build completes without errors.   


Configurations and launch of the project
----------------------------------------

1. **Configure ROS 2 and MoveIt**:

The template may include configuration files for ROS 2 and MoveIt. Ensure these are properly configured to match your simulation setup. Key files include:

- **ROS 2 Launch Files**: Typically found in the ``launch`` directory, configure these files to start the ROS 2 nodes required for your simulation.
- **MoveIt Configuration**: Check the ``moveit_config`` directory for MoveIt configuration files. Ensure these files are correctly set up for your robot and planning requirements.

2. **Launch the Simulation**:

Start the O3DE Editor:

.. code-block:: bash

   <path-to-o3de-directory>/build/bin/profile/Editor

In the O3DE Editor:

1. Open the example level provided by the template. Navigate to the ``File`` menu, select ``Open Level``, and choose the example level from the ``Levels`` directory.
2. Launch the ROS 2 nodes and MoveIt components required for the simulation. For manipulation, this can be done with:

.. code-block:: bash

   ros2 launch Examples/panda_moveit_config_demo.launch.py

And for the palletization try:

.. code-block:: bash

   source install/setup.bash
   ros2 launch ur_moveit_config ur_moveit.launch.py ur_type:=ur10 use_sim_time:=true use_fake_hardware:=true


3. **Simulate Robotic Manipulation**:

With the simulation running, you can interact with the robotic manipulator in the O3DE Editor. Test different manipulation tasks and adjust configurations as needed. Use the MoveIt interface to plan and execute robotic movements.

For further details on configuring ROS 2 and MoveIt for your specific needs, refer to the `MoveIt 2 Documentation`_ and the `O3DE Robotics Project Configuration`_ guide.

.. _MoveIt 2 Documentation: https://moveit.ros.org/documentation/
.. _O3DE Robotics Project Configuration: https://development--o3deorg.netlify.app/docs/user-guide/interactivity/robotics/project-configuration/
