<!--
 SPDX-FileCopyrightText: 2022 Dominik Wombacher <dominik@wombacher.cc>
 SPDX-License-Identifier: CC-BY-SA-4.0
-->
# SLES 12 SP5 - Python, systemd

Derived Container based on sles12sp5:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule.

# How to run with Docker

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

- https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container#the_quest
- https://blog.swwomm.com/2020/10/testing-systemd-services-on-arch-fedora.html
- https://github.com/moby/moby/issues/6758#issuecomment-284923933

# How to use with Molecule

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

# Important

You need a SUSE Linux Enterprise Server 12 SP5 System with active subscription to build this container image.
