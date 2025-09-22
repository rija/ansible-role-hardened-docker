# role-hardened-docker

This is an Ansible role to harden an installation of Docker CE on Linux.

## Purposes

* Setup a certificate authenticated access to the daemon over TCP

## Prerequisites

* Docker CE is already installed following the official instructions at: (https://docs.docker.com/engine/install/)
* The target environment has systemd present and Docker service is enabled in systemd.
