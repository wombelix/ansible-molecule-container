FROM registry.suse.com/suse/sles12sp5:latest

LABEL org.opencontainers.image.title="SLES 12 SP5 - Python2"
LABEL org.opencontainers.image.description="Derived Container based on sles12sp5:latest that includes Python2 to allow testing Ansible Roles with Molecule"
LABEL org.opencontainers.image.authors="Dominik Wombacher <dominik@wombacher.cc>"
LABEL org.opencontainers.image.url="https://dominik.wombacher.cc"
LABEL org.opencontainers.image.source="https://dominik.wombacher.cc/~git/ansible-molecule-container/"

RUN update-ca-certificates
RUN zypper --gpg-auto-import-keys ref -s
RUN zypper -n in python python-certifi python-zypp rpm-python python-xml python-devel \
    gawk sudo bash ca-certificates which bind-utils curl sapconf psmisc; \
    rm -rf /var/cache/zypp/*; \
    rm -rf /var/log/*
