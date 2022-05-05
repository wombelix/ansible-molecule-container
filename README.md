<!--
 SPDX-FileCopyrightText: 2022 Dominik Wombacher <dominik@wombacher.cc>
 SPDX-License-Identifier: CC-BY-SA-4.0
-->
# Ansible Molecule Container

Collection of Dockerfiles to build Container Images that include necessary packages to test Ansible Roles with Molecule.

[![REUSE status](https://api.reuse.software/badge/dominik.wombacher.cc/~git/ansible-molecule-container)](https://api.reuse.software/info/dominik.wombacher.cc/~git/ansible-molecule-container)

# Table of Content

* [Container](#container)
    * [SLES 12 SP5 - Python](#sles-12-sp5-python2)
    * [SLES 12 SP5 - Python, systemd](#sles-12-sp5-python2-systemd)
* [License](#license)

# Container

## SLES 12 SP5 - Python2

Derived Container based on sles12sp5:latest that includes Python2 to allow testing Ansible Roles with Molecule.

## SLES 12 SP5 - Python2, systemd

Derived Container based on sles12sp5:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule.

## RHEL 7 (UBI) - Python, systemd

Derived Container based on ubi7/ubi-init:latest:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule.

```
docker run \
--tmpfs /run --tmpfs /tmp \
--volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
--volume /dev/shm --tmpfs /dev/shm:rw,nosuid,nodev,exec,size=64M \
--detach --rm \
--name <containername> \
<image>
```

The `/dev/shm` line is nececessary to meet requirements of the included `sapconf` package.

Further details why the other tmpfs and volume statements are necessary:

- <https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container#the_quest>
- <https://blog.swwomm.com/2020/10/testing-systemd-services-on-arch-fedora.html>
- <https://github.com/moby/moby/issues/6758#issuecomment-284923933>

### How to use systemd Container with Molecule

```
platforms:
  - name: <containername>
    image: <image>
    pre_build_image: true
    tmpfs:
      - /run
      - /tmp
      - /dev/shm:rw,nosuid,nodev,exec,size=64M
    volumes:
      - "/sys/fs/cgroup:/sys/fs/cgroup:ro"
      - "/dev/shm"
```

# License

Unless otherwise stated: `GNU General Public License v3.0 or later`

All files contain license information either as `header comment` or `corresponding .license` file.

[REUSE](https://reuse.software) from the [FSFE](https://fsfe.org/) implemented to verify license and copyright compliance.
