Integrating a Custom Docker Container
=====================================

This guide outlines the steps required to integrate a custom Docker
container into the AirTaxiSim simulation pipeline.

.. note::

   This guide is under active development.

Purpose
-------

This how-to guide is task-oriented and focuses on enabling users to run
AirTaxiSim components inside a custom Docker environment.

Typical Use Cases
-----------------

- Using a custom base image with additional system dependencies
- Running AirTaxiSim on a remote machine or cluster
- Ensuring reproducibility across development environments

Steps
-----

1. Create or modify a Dockerfile based on an existing AirTaxiSim-compatible image
2. Install required system and Python dependencies inside the container
3. Mount the AirTaxiSim repository into the container at runtime
4. Verify GPU and simulator access from within the container
5. Run a sample configuration to confirm successful integration

Notes
-----

This page currently contains placeholder content. Detailed instructions,
examples, and troubleshooting tips will be added in future versions of
the documentation.
