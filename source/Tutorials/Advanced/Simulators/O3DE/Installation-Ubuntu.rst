Installation (Ubuntu)
======================================

**Goal:** Install Open 3D Engine (O3DE) from the .deb package and run a simulation using the O3DE-extras template.

**Tutorial level:** Advanced

**Time:** 20-30 minutes

.. contents:: Contents
   :depth: 2
   :local:

Background
-------------

This tutorial will guide you through the steps to install Open 3D Engine (O3DE) from a .deb package and set up the O3DE-extras package for simulation on Ubuntu. The guide minimizes terminal use and focuses on GUI-based steps where possible.

Prerequisites
-------------

It is recommended to understand basic ROS principles covered in the beginner :doc:`../../../../Tutorials`.
In particular, :doc:`../../../Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace` and :doc:`../../../Beginner-Client-Libraries/Creating-Your-First-ROS2-Package` are useful prerequisites.

Before you begin, ensure you have the following:

- **ROS 2 installed**: The o3de-extras package assumes that ROS 2 is already installed on your system.

Setting up O3DE from GitHub on Linux
------------------------------------

Step 1: Install Required Dependencies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First, install the necessary dependencies by running the following commands in your terminal:

.. code-block:: bash

   sudo apt-get update
   sudo apt-get install -y build-essential ninja-build python3 python3-pip python3-venv \
                           libglu1-mesa-dev libxcb-xinerama0 libxcb-xinput0 libxcb-xinput-dev \
                           libfontconfig1 libssl-dev uuid-dev clang lld

Step 2: Clone the O3DE Repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Next, clone the O3DE repository from GitHub:

.. code-block:: bash

   git clone https://github.com/o3de/o3de.git
   cd o3de

This command downloads the O3DE source code into a directory named ``o3de`` and changes the current working directory to it.

Step 3: Configure the O3DE Project
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. @TODO: Restricted in manifest file

Run the ``cmake`` command to configure the project. This will generate the necessary build files in the ``build`` directory.

.. code-block:: bash

   cmake -B build/ -S . -G "Ninja Multi-Config"

Here’s what each argument does:

- ``-B build/``: Specifies the output directory for the build files.
- ``-S .``: Specifies the source directory (current directory).
- ``-G "Ninja Multi-Config"``: Specifies Ninja as the build system with multi-config support.

If you experience any issues regarding the ``restricted.json`` file, try opening the ``o3de_manifest.json``:

.. code-block:: bash

   nano ~/.o3de/o3de_manifest.json

then, remove the ``restricted`` list located in the file.

Step 4: Set Up the Project Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before building the O3DE, you need to set up the project environment. Run the following script to do so:

.. code-block:: bash

   ./scripts/o3de.sh register --this-engine

This command registers the engine, allowing you to create and manage projects with O3DE.

Step 5: Build O3DE
^^^^^^^^^^^^^^^^^^

Now, build O3DE using the ``cmake`` command:

.. code-block:: bash

   cmake --build build/ --config profile

This command builds O3DE in ``profile`` mode, which is recommended for development. You can replace ``profile`` with ``debug`` or ``release`` depending on your needs.


Download and Install o3de-extras 
----------------------------------

Downloading a .zip package 
^^^^^^^^^^^^^^^^^^^^^^^^^^^

   1. Navigate to the `o3de-extras GitHub repository <https://github.com/o3de/o3de-extras>`_.
   2. Download the necessary files as a ZIP package. To do this, click the **Code** button on the repository's main page and select **Download ZIP**.
   3. Once the ZIP file is downloaded, extract its contents to a folder of your choice.


Setting up o3de-extras
^^^^^^^^^^^^^^^^^^^^^^

Now, you need to inform O3DE about the location of the extra assets in this repository by registering them. From the O3DE repository folder, you can register some or all of the extra assets using the ``o3de register`` command. Since these are optional assets, you may choose to register only those that you need. For example, to register a specific gem, use the following command:

.. code-block:: bash

   ./scripts/o3de.sh register --gem-path <o3de-extras>/Gems/<gem name>

If you want to register all the gems, you can do so since the repository follows the standard O3DE compound repository structure, with all gems located in the ``<o3de-extras>/Gems`` directory. To register all gems at once, use:

.. code-block:: bash

   ./scripts/o3de.sh register --all-gems-path <o3de-extras>/Gems

This process can be repeated for any other object types, if they exist:

.. code-block:: bash

   ./scripts/o3de.sh register --all-engines-path <o3de-extras>/Engines
   ./scripts/o3de.sh register --all-projects-path <o3de-extras>/Projects
   ./scripts/o3de.sh register --all-gems-path <o3de-extras>/Gems
   ./scripts/o3de.sh register --all-templates-path <o3de-extras>/Templates
   ./scripts/o3de.sh register --all-restricted-path <o3de-extras>/Restricted

If you've registered a gem, which functions like a plugin or component within a project, and you wish to use it in your project, you need to enable it by using the ``o3de enable-gem`` command:

.. code-block:: bash

   ./scripts/o3de.sh enable-gem --gem-name <gem name> --project-name <project name>


Setting Up and Running a Simulation
------------------------------------

Creating a New ROS 2 Project
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. **Register the ROS 2 Project Template**:

   Navigate to your O3DE directory and register the ROS 2 Project Template from the ``o3de-extras`` repository:

   .. code-block:: bash

      ./scripts/o3de.sh register --all-templates-path <path-to-o3de-extras>/Templates

   This command registers all templates within the ``o3de-extras`` repository, including the ROS 2 Project Template.

2. **Create a New Project**:

   Create a new project using the ROS 2 Project Template:

   .. code-block:: bash

      ./scripts/o3de.sh create-project --project-name <project_name> --template-name Ros2ProjectTemplate --project-path <path-to-project-directory>

   Replace ``<project_name>`` with your desired project name and ``<path-to-project-directory>`` with the directory where you want the project to be created.

3. **Configure and build the Project**:

   After creating the project, you need to cofigure and build it:

   Navigate to your project directory:

   .. code-block:: bash

      cd <project_path>

   .. code-block:: bash

      cmake -B build/ -S . -G "Ninja Multi-Config"

   .. code-block:: bash

      cmake --build <path-to-build-directory> --target <project_name> Editor

   Ensure the build completes without errors.

Setting Up the SLAM Navigation Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ROS 2 Project Template includes several example projects. In this tutorial, you will use the SLAM navigation example to simulate a robot performing SLAM and navigation tasks.

1. **Navigate to the Example Directory**:

   The SLAM navigation example is located in the following directory:

   .. code-block:: bash

      <project-directory>/Examples/slam_navigation

2. **Run the Example**:

   Launch the example by opening the O3DE Editor:

   .. code-block:: bash

      <path-to-o3de-directory>/build/bin/profile/Editor

   Once in the Editor, open the SLAM navigation level by navigating to the ``Levels`` tab and selecting the SLAM navigation level.

   Press ``Ctrl+G`` to start the simulation.

3. **Launching ROS 2 Nodes**:

   In a new terminal, source your ROS 2 environment and launch the ROS 2 nodes required for SLAM and navigation:

   .. code-block:: bash

      source /opt/ros/foxy/setup.bash
      ros2 launch slam_navigation slam_navigation_launch.py

   This command starts the ROS 2 nodes, enabling the robot in the simulation to perform SLAM and navigation.
