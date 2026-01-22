Installation
============

AirTaxiSim is a Python-based simulator for autonomous air taxis operating
in urban environments. The project is primarily developed and tested on
Linux systems.

Prerequisites
-------------

- Ubuntu 20.04 or 22.04
- NVIDIA GPU with compatible drivers
- Docker
- NVIDIA Container Toolkit
- Python 3.8+

Detailed instructions for installing Docker and the NVIDIA Container Toolkit
are provided in:

``doc/tools_installation.md``

Cloning the repository
----------------------

Clone the repository **with submodules**:

.. code-block:: console

   $ git clone https://github.com/CPS-IL/airtaxisim.git --recurse-submodules

Python dependencies
-------------------

Install the required Python packages:

.. code-block:: console

   $ python3 -m pip install loguru

Running AirTaxiSim
------------------

Once the installation is complete, you can run a basic simulation using one
of the provided configuration files:

.. code-block:: console

   $ cd airtaxisim
   $ python3 rraaa.py configs/single-static-jaxguam.yml

This will launch AirTaxiSim with a sample VTOL vehicle in a static urban
environment.
