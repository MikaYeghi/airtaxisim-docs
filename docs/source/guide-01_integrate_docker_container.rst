Integrating a Custom Docker Container
=====================================

This guide describes how to integrate a custom Docker container containing a
ROS package into the AirTaxiSim simulation pipeline.

In this guide, we assume you want to integrate an existing ROS package into
AirTaxiSim. The package can implement any functionality, such as flight
monitoring, perception, or path planning.

Core ROS Package
----------------

First, create an example ROS package by following the ROS 1 tutorial on creating a
`publisher-subscriber package <https://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29>`_.

Create a directory named ``my_ros_package`` in the root of the AirTaxiSim repository:

::

   .
   ├── LICENSE
   ├── README.md
   ├── VERSION
   ├── configs
   ├── doc
   ├── docker
   ├── env_sim
   ├── ground_station
   ├── media
   ├── msg
   ├── my_ros_package  # <-- new directory
   ├── path_planner
   ├── perception
   ├── rraaa.py
   ├── sim_control
   ├── tests
   ├── utils
   └── vehicles

Add your ROS package to the ``my_ros_package`` directory. The resulting structure
should resemble the following:

::

   my_ros_package/
   └── beginner_tutorials
      ├── CMakeLists.txt
      ├── include
      │   └── beginner_tutorials
      ├── package.xml
      ├── scripts
      │   ├── listener.py
      │   └── talker.py
      └── src

In practice, this package typically already exists and only needs to be integrated
into the simulator.

Integrating into AirTaxiSim
---------------------------

Integrating a new ROS package into AirTaxiSim consists of three steps:

1. **Create a Dockerfile** for the package.  
   This file defines the base image, installs dependencies, and sets up the ROS
   environment.

2. **Configure the Docker Compose service**.  
   Add a service definition to ``docker-compose.yml`` describing how the container
   is built and how it communicates with other services.

3. **Define a service configuration file**.  
   Create a YAML configuration specifying which ROS nodes are executed when the
   container starts.

Create a Dockerfile
~~~~~~~~~~~~~~~~~~~

Create a ``Dockerfile`` inside the ``my_ros_package`` directory:

::

   FROM ros:noetic

   COPY ./beginner_tutorials /catkin_ws/src/beginner_tutorials

   RUN apt-get update && apt-get install -y python3 python3-pip \
      && update-alternatives --install /usr/bin/python python /usr/bin/python3 10

This example uses the official ROS Noetic image as the base and copies the package
into a Catkin workspace. In a production setup, you will typically install
additional dependencies and build the workspace.

The directory structure should now be:

::

   my_ros_package/
   ├── Dockerfile  # <-- new file
   └── beginner_tutorials
      ├── CMakeLists.txt
      ├── include
      │   └── beginner_tutorials
      ├── package.xml
      ├── scripts
      │   ├── listener.py
      │   └── talker.py
      └── src

Configure docker-compose
~~~~~~~~~~~~~~~~~~~~~~~~

Next, configure Docker Compose to include the new container.

Open ``airtaxisim/docker/docker-compose.yml`` and add the following service
definition:

::

   my_ros_package:
      container_name: my_ros_package
      build:
         context: ../my_ros_package
         dockerfile: Dockerfile
      volumes:
         - /tmp/.X11-unix:/tmp/.X11-unix:rw
      privileged: true
      network_mode: host
      devices:
         - "/dev/snd"
      tty: true
      stdin_open: true
      working_dir: /catkin_ws/
      environment:
         - SERVICE_NAME=beginner_tutorials
         - SDL_VIDEODRIVER=x11
         - DISPLAY=$DISPLAY

This configuration defines how the container is built, which resources it can
access, and how it connects to the host system and other services.

Define the Service Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a service configuration file describing which ROS nodes should run inside
the container.

Navigate to ``airtaxisim/configs/services`` and create a file named
``my_ros_package.yml`` with the following contents:

::

   start_delay: 1
   ros:
   workspace: /catkin_ws
   ros_package: beginner_tutorials
   rosrun_files:
      - talker.py
      - listener.py

This configuration instructs AirTaxiSim to execute the ``talker.py`` and
``listener.py`` nodes from the specified ROS package when the container starts.

To enable the service during simulation, add it to the simulation configuration.
Open ``airtaxisim/configs/single-static-jaxguam.yml`` and include the service:

::

   services:
      my_ros_package:
         include: services/my_ros_package.yml

Running the Custom Container
----------------------------

Start the simulation with the custom container using:

::

   python3 rraaa.py configs/single-static-jaxguam.yml

After startup, verify that the container is running and that the ROS nodes are
executing as expected.

.. TODO: Add example output and verification steps.
