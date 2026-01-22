Installation
============

This page explains how to install **AirTaxiSim** and its dependencies.

Prerequisites
-------------

Before installing AirTaxiSim, make sure you have:

- Python 3.8 or newer
- Git (with submodule support)
- A Linux-based environment (recommended)

Cloning the repository
----------------------

Clone the repository **with submodules**:

.. code-block:: console

   $ git clone https://github.com/CPS-IL/airtaxisim.git --recurse-submodules

This ensures that all required third-party components are fetched correctly.

Python dependencies
-------------------

Install the required Python packages using `pip`:

.. code-block:: console

   $ python3 -m pip install loguru

Additional dependencies and optional tools are documented in:

``doc/tools_installation.md``

Please follow that guide if you plan to use advanced features or development tools.

Verification
------------

To verify that the installation was successful, try running a sample simulation
as described in the :doc:`usage` page.

If all dependencies are installed correctly, the simulator should start without errors.
