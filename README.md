<!--
 SPDX-FileCopyrightText: 2022 Dominik Wombacher <dominik@wombacher.cc>
 SPDX-License-Identifier: CC-BY-SA-4.0
-->
# Ansible Molecule Container

Collection of Dockerfiles to build Container Images that include necessary packages to test Ansible Roles with Molecule.

[![REUSE status](https://api.reuse.software/badge/git.sr.ht/~wombelix/ansible-molecule-container)](https://api.reuse.software/info/git.sr.ht/~wombelix/ansible-molecule-container)

# Table of Content

* [Container](#container)
    * [SLES 12 SP5 - Python](#sles-12-sp5-python2)
    * [SLES 12 SP5 - Python, systemd](#sles-12-sp5-python2-systemd)
    * [RHEL7 (UBI) - Python, systemd](#rhel-7-ubi-python2-systemd)
* [How to run systemd Container with Docker](#how-to-run-systemd-container-with-docker)
* [How to use systemd Container with Molecule](#how-to-use-systemd-container-with-molecule)
* [Source](#source)
* [Contribute](#contribute)
* [License](#license)

# Container

## SLES 12 SP5 - Python2

Container based on sles12sp5:latest that includes Python2 to allow testing Ansible Roles with Molecule.

## SLES 12 SP5 - Python2, systemd

Container based on sles12sp5:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule.

## RHEL 7 (UBI) - Python2, systemd

Container based on ubi7/ubi-init:latest:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule.

# How to run systemd Container with Docker

```
docker run \
--tmpfs /run --tmpfs /tmp \
--volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
--volume /dev/shm --tmpfs /dev/shm:rw,nosuid,nodev,exec,size=64M \
--detach --rm \
--name <containername> \
<image>
```

The `/dev/shm` line is nececessary to meet requirements of the included `sapconf` package in the `sles12sp5-python2-systemd` container.
Can be omitted when using other container or if `sapconf` isn't required / can be ignored.

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

See [How to run systemd Container with Docker](#how-to-run-systemd-container-with-docker) section above for information about `/dev/shm`.

# Source

The primary location is: https://git.sr.ht/~wombelix/ansible-molecule-container

Mirrors of the repository are available on 
[Codeberg](https://codeberg.org/wombelix/ansible-molecule-container), 
[Gitlab](https://gitlab.com/wombelix/ansible-molecule-container) and 
[Github](https://github.com/wombelix/ansible-molecule-container).

# Contribute

Don't hesitate to provide Feedback, open an Issue or create an Pull / Merge Request.

Just pick the workflow or platform you prefer and are most comfortable with.

Feedback, Bug Reports or Patches via [Email](https://dominik.wombacher.cc/pages/contact.html) are also always welcome.

# License

Unless otherwise stated: `GNU General Public License v3.0 or later`

All files contain license information either as `header comment` or `corresponding .license` file.

[REUSE](https://reuse.software) from the [FSFE](https://fsfe.org/) implemented to verify license and copyright compliance.
