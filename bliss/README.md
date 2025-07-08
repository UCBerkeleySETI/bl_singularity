# Bliss containerization

## Overview

The files here can be used to create, install, and run an Ubuntu 24.04 based
Singularity/Apptainer container for (`bliss`)[https://github/com/n-west/bliss].

- `Makefile` - Used by `make` when building/installing the `bliss` container
- `README.md` - This file
- `bliss.def` - Singularity/apptainer defintions (aka "recipe") file
- `bliss_runner` - A utility script for running `bliss` apps from the container

## Building the container

The container can be built with `singularity` by running:

    sudo make

The container can be built with `apptainer` by running:

    sudo make SINGULARITY=apptainer

It must be built by a user with `root` permissions so don't forget the `sudo`!

## Installing the container and runner script

Install the container and the runner script, `bliss_runner`, by running:

    sudo make install

This will also create symlinks to the runner script for all `bliss` apps in the
container.

NB: You must also include the same `SINGULARITY=...` option, if any, that you
used when building the container so that the runner script's `SINGULARITY`
variable will get updated to match your containerization tool.

By default, everything will be installed in `/usr/local/bin`, but
you can change this by specifying `Makefile` variables on the command line.

For example to install everything into `/opt/bliss/bin`, run:

    sudo make install PREFIX=/opt/bliss

See the section below on `Makefile` variables for more details.

## Running bliss apps from the container

To run a `bliss` app, just invoke it by name and pass parameters as you
normally would.  The following `bliss` apps are valid for the current build:

- `bliss_find_hits`
- `bliss_generate_channelizer_response`
- `bliss_hits_to_dat`

These are actually symlinks to the `bliss_runner` script which will invoke the
containerization tool to execute the app specified by the symlink's name.

Invoking the runner script `bliss_runner` directly (i.e. not via a symlinnk)
will start a shell inside the container with the same bound directories as when
running a `bliss` app from the container.

## Potentially useful `Makefile` variables

- `SINGULARITY` - Specifies the container tool.  Defaults to `singularity`.
- `PREFIX` - `make install` will install files in `${PREFIX}/bin`.  Defaults to
  `/usr/local`.

## Potentially useful environment variables

- `CUDA_DIR` - specifes the local CUDA directory which will always be bound to
  `usr/local/cuda` in the container.
- `BLISS_DATADIRS` - A space-separated list of directories to bind into the
  container.  This has a fairly broad list of defaults, but you may need to
  adapt this to your system's local setup.  Only directories that exist will be
  bound into the container, so it's fine to include a superset of directories
  for your site.
