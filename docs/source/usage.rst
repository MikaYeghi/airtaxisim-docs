Usage
=====

.. _installation:

Installation
------------

To use AirTaxiSim, first clone the repository with submodules:

.. code-block:: console

   $ git clone https://github.com/CPS-IL/airtaxisim.git --recurse-submodules

Next, install the required Python packages (see [doc/tools_installation.md](doc/tools_installation.md) for details):

.. code-block:: console

   $ python3 -m pip install loguru

Running the simulator
--------------------

You can run a sample simulation using the provided configuration files:

.. code-block:: console

   $ cd airtaxisim
   $ python3 rraaa.py configs/single-static-jaxguam.yml

This will launch the AirTaxiSim environment with a sample VTOL vehicle in a static urban scenario.

.. note::

   AirTaxiSim supports advanced features such as multi-agent simulations,
   edge-case testing, and dataset generation. See the :doc:`api` and
   :doc:`configs` sections for more details.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
