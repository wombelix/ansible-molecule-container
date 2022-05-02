# SPDX-FileCopyrightText: 2022 Dominik Wombacher <dominik@wombacher.cc>
#
# SPDX-License-Identifier: GPL-3.0-or-later

FROM registry.access.redhat.com/ubi7/ubi-init:latest

LABEL org.opencontainers.image.title="RHEL 7 (UBI) - Python2, systemd"
LABEL org.opencontainers.image.description="Derived Container based on ubi-init:latest that includes Python2 and systemd to allow testing Ansible Roles with Molecule"
LABEL org.opencontainers.image.authors="Dominik Wombacher <dominik@wombacher.cc>"
LABEL org.opencontainers.image.url="https://dominik.wombacher.cc"
LABEL org.opencontainers.image.source="https://dominik.wombacher.cc/~git/ansible-molecule-container/"

RUN yum install -y python rpm-python python-lxml python-devel \
    gawk sudo bash ca-certificates which bind-utils curl \
    openssh rsyslog;
