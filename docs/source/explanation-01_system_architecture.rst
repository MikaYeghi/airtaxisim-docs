System Architecture
===================

This page provides a high-level overview of the architecture of **AirTaxiSim**.

Audience
--------

Explanation pages focus on concepts, design decisions, and system behavior
rather than step-by-step instructions.

Overview
--------

AirTaxiSim is structured as a modular simulation framework consisting of multiple
Docker containers, which communicate with each other via **ROS 1**. Each container
represents a semantically meaningful module, such as perception, planning, or
control.

Motivation for Multi-Container Architecture
-------------------------------------------

The use of multiple Docker containers is motivated by two main considerations:

1. **Dependency isolation:** Different autonomy components may require
   different versions of Python or other packages (e.g., Python 3.10+ for one
   module versus Python 3.8 for another). Containerization ensures that each
   module can operate with its required dependencies without conflicts.

2. **ROS environment management:** ROS typically installs packages into the
   system's base environment, which can lead to conflicts and pollution of the
   host system. Encapsulating ROS inside Docker containers preserves a clean
   and reproducible environment, keeping the simulator self-contained.

Special Containers
------------------

AirTaxiSim includes several "special containers" that are mostly fixed and not
intended for user modification. Users are expected to interact with these
containers via ROS topics, while custom development is done in other containers.

The main special containers are:

- **carla**: A high-fidelity environment simulator based on CARLA.  
- **env_sim**: An infrastructure container that serves as an interface between
  Python and CARLA.  
- **sim_control**: A container responsible for controlling the simulator and
  collecting simulation data.  

User-Customizable Containers
----------------------------

All other containers are designed to be fully customizable. Users interact
with the CARLA container by:

- Publishing the ego vehicle pose to the appropriate ROS topic  
- Subscribing to perception data published by CARLA on ROS topics  

This design allows users to develop and test autonomy modules without modifying
the core simulation infrastructure.
