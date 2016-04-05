# Docker
This repository stores Docker related scripts. In particular scripts that unify docker container and image management. These scripts are akin to scripts used in Linux service management.

# Docker Installation

## Install Centos 7
The CentOS 7 installer ISO image can be downloaded from http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1511.iso. Choose a mirror closest to you for faster download time. 

1. Choose a minimal installation of Centos 7.
2. Create a user named docker. For simplicity, use a password docker.

## Join a Windows Domain (Optional)
This is an optional step for users who want to join the Docker server into a Windows domain.

1. Install Kerberos workstation.
2. Install Samba.

The following section changes are needed after installing and configuring Docker.
## Ensure SELinux policy is relaxed in external volumes that is mounted by container
chcon -Rt svirt_sandbox_file_t ~/etc/docker/container/externals/
