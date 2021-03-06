# Dockerfile for building Ansible image for Debian 7 (wheezy), with as few additional software as possible.
#
# @see https://launchpad.net/~ansible/+archive/ubuntu/ansible
#
# Version  1.0
#


# pull base image
FROM debian:wheezy

MAINTAINER William Yeh <william.pjyeh@gmail.com>


RUN echo "===> Installing python, sudo, and supporting tools..."  && \
    apt-get update  && \
    DEBIAN_FRONTEND=noninteractive         \
    apt-get install -y                     \
        python python-yaml sudo            \
        curl gcc python-pip python-dev  && \
    \
    \
    echo "===> Installing Ansible..."   && \
    pip install ansible                 && \
    \
    \
    echo "===> Removing unused APT resources..."                       && \
    apt-get -f -y --auto-remove remove curl gcc python-pip python-dev  && \
    apt-get clean                                                      && \
    rm -rf /var/lib/apt/lists/*  /tmp/*                                && \
    \
    \
    echo "===> Adding hosts for convenience..."        && \
    mkdir -p /etc/ansible                              && \
    echo '[local]\nlocalhost\n' > /etc/ansible/hosts


# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]
