# Docker
This repository stores Docker related scripts. In particular scripts that unify docker container and image management. These scripts are akin to scripts used in Linux service management.

# Docker Installation

The following section changes are needed after installing and configuring Docker.
## Ensure SELinux policy is relaxed in external volumes that is mounted by container
chcon -Rt svirt_sandbox_file_t ~/etc/docker/container/externals/
