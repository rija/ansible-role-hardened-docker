# role-hardened-docker

This is an Ansible role to harden an installation of Docker on Linux.
It started as a replacement for `role-secure-docker` which is no longer maintained.
Over time, I will try to add other additional measures also documented in Docker's [security manual](https://docs.docker.com/engine/security/).

## Purposes

* Setup CA, client and server certificates to allow TLS client certificate authentication to the docker daemon
* Enable TCP access to the docker daemon

## Prerequisites

### For using

* Docker CE is already installed following the official instructions at: (https://docs.docker.com/engine/install/)
* The target environment has systemd present and Docker service is enabled in systemd.
* At the moment Ubuntu 24 is the only host on which the role has been tested against.

### For developing

Ensure the tool dependencies are installed with Homebrew

```
brew bundle
```

Then install the Ansible dependencies

```
ansible-galaxy install -r requirements.yml
```

## Testing

This role uses `molecule` for integration Testing
```
molecule test
```
