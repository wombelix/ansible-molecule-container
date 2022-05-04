# SPDX-FileCopyrightText: 2022 Dominik Wombacher <dominik@wombacher.cc>
#
# SPDX-License-Identifier: GPL-3.0-or-later

FROM registry.suse.com/suse/sles12sp5:latest

LABEL org.opencontainers.image.title="SLES 12 SP5 - Python2, systemd"
LABEL org.opencontainers.image.description="Derived Container based on sles12sp5:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule"
LABEL org.opencontainers.image.authors="Dominik Wombacher <dominik@wombacher.cc>"
LABEL org.opencontainers.image.url="https://dominik.wombacher.cc"
LABEL org.opencontainers.image.source="https://dominik.wombacher.cc/~git/ansible-molecule-container/"

RUN update-ca-certificates
RUN zypper --gpg-auto-import-keys ref -s
RUN zypper -n in systemd systemd-sysvinit \ 
    python python-certifi python-zypp rpm-python python-xml python-devel \
    gawk sudo bash ca-certificates which bind-utils curl sapconf psmisc \
    openssh rsyslog libaudit1 audit; \
    (cd /usr/lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /usr/lib/systemd/system/multi-user.target.wants/*; \
    rm -f /etc/systemd/system/*.wants/*; \
    rm -f /usr/lib/systemd/system/local-fs.target.wants/*; \
    rm -f /usr/lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /usr/lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /usr/lib/systemd/system/basic.target.wants/*; \
    rm -rf /var/cache/zypp/*; \
    rm -rf /var/log/*

CMD ["/sbin/init"]
