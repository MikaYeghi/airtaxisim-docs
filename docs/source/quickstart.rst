Quick Start
===========

AirTaxiSim is a Python-based simulator for autonomous air taxis operating
in dense urban environments. This guide walks you through installing the
required dependencies and running a basic simulation.

Prerequisites
-------------

- Ubuntu 20.04 or 22.04
- NVIDIA GPU with compatible drivers
- Docker
- NVIDIA Container Toolkit
- Python 3.8+

Detailed instructions for installing Docker and the NVIDIA Container Toolkit
are available in:

``doc/tools_installation.md``

Clone the Repository
--------------------

Clone the repository **with submodules**:

.. code-block:: console

   $ git clone https://github.com/CPS-IL/airtaxisim.git --recurse-submodules

Python Dependencies
-------------------

Install the required Python package:

.. code-block:: console

   $ python3 -m pip install loguru

Run a Sample Simulation
-----------------------

After installation, launch AirTaxiSim using one of the provided configuration
files:

.. code-block:: console

   $ cd airtaxisim
   $ python3 rraaa.py configs/single-static-jaxguam.yml

This starts a sample simulation with a VTOL vehicle operating in a static
urban environment.
