# role-hardened-docker

This is an Ansible role to harden an installation of Docker on Linux.
It started as a replacement for `role-secure-docker` which is no longer maintained.
Over time, I will try to add other additional measures also documented in Docker's [security manual](https://docs.docker.com/engine/security/).

## Purposes

* Setup CA, client and server certificates to allow TLS client certificate authentication to the docker daemon
* Enable TCP access to the docker daemon

## Prerequisites

* Docker CE is already installed following the official instructions at: (https://docs.docker.com/engine/install/)
* The target environment has systemd present and Docker service is enabled in systemd.

## Testing

This role uses `molecule` for integration Testing
```
molecule test
```
