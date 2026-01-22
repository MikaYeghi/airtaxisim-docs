Running a Basic Simulation
==========================

This tutorial demonstrates how to run a pre-configured AirTaxiSim
scenario. It is intended as a minimal, hands-on starting point for new
users who want to quickly verify that the simulator is working.

Overview
--------

In this tutorial, you will learn how to:

- Navigate to the AirTaxiSim repository
- Run a pre-configured simulation scenario
- Understand what happens when the simulator starts

Prerequisites
-------------

Before starting this tutorial, make sure you have completed the
:doc:`quickstart` setup, including cloning the repository and installing the
required dependencies.

Running the Simulation
----------------------

AirTaxiSim ships with example configuration files that can be used
out of the box.

From the root of the repository, run:

.. code-block:: console

   $ cd airtaxisim
   $ python3 rraaa.py configs/single-static-jaxguam.yml

This command launches a basic simulation with a sample VTOL vehicle
operating in a static urban environment.

What to Expect
--------------

When the simulator starts successfully, you should see logs indicating
that the environment, vehicle model, and simulation components have
been initialized. Depending on your setup, a visualization window or
simulation output may appear.

Notes
-----

This tutorial intentionally focuses on execution rather than internal
details. More advanced tutorials will cover configuration files,
scenario customization, and pipeline extensions.
