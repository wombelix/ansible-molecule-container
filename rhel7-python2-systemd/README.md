<!--
 SPDX-FileCopyrightText: 2023 Dominik Wombacher <dominik@wombacher.cc>
 SPDX-License-Identifier: CC-BY-SA-4.0
-->
# RHEL 7 (UBI) - Python, systemd

Derived Container based on ubi7/ubi-init:latest:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule.

# How to run with Docker

```
docker run \
--tmpfs /run --tmpfs /tmp \
--volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
--detach --rm \
--name <containername> \
<image>
```

Further details why the other tmpfs and volume statements are necessary:

- <https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container#the_quest>
  (Archive: [[1]](https://web.archive.org/web/20231009083718/https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container#the_quest), 
  [[2]](https://archive.today/2023.10.09-083730/https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container%23the_quest))
- <https://blog.swwomm.com/2020/10/testing-systemd-services-on-arch-fedora.html>
  (Archive: [[1]](https://web.archive.org/web/20230529154629/https://blog.swwomm.com/2020/10/testing-systemd-services-on-arch-fedora.html), 
  [[2]](https://archive.today/2023.10.09-083756/https://blog.swwomm.com/2020/10/testing-systemd-services-on-arch-fedora.html))
- <https://github.com/moby/moby/issues/6758#issuecomment-284923933>
  (Archive: [[1]](https://web.archive.org/web/20231009083829/https://github.com/moby/moby/issues/6758#issuecomment-284923933), 
  [[2]](https://archive.today/2023.10.09-083829/https://github.com/moby/moby/issues/6758%23issuecomment-284923933))

# How to use with Molecule

```
platforms:
  - name: <containername>
    image: <image>
    pre_build_image: true
    tmpfs:
      - /run
      - /tmp
    volumes:
      - "/sys/fs/cgroup:/sys/fs/cgroup:ro"
```
