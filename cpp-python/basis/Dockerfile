#
# https://github.com/transport-intelligence/docker-images/blob/master/cpp-python/basis/Dockerfile
#

FROM ubuntu:18.04
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root
ENV GCOV_TMP_DIR /opt/gcovr

# Basic packages
# C++ and Python development
# JavaScript (JS) development
RUN apt-get -y update && \
  apt-get -y install apt-utils zip unzip wget htop git openssh-client vim \
  autoconf libtool zlib1g-dev lsb-release \
  cmake build-essential gcc-8 cppcheck clang-format-8 \
  libc6-dev-i386 \
  libboost-all-dev \
  libreadline-dev libncurses5-dev \
  libzmqpp-dev libssl-dev \
  libffi-dev swig \
  doxygen graphviz \
  libgmp-dev \
  flex bison \
  python python-pip python-dev python-setuptools python-wheel python-six \
  python3 python3-pip python3-dev python3-setuptools python3-wheel python3-six
RUN apt-get -y install  npm

# Python 2
RUN python -m pip install --upgrade pip setuptools virtualenv gcovr

# Python 3
RUN python3 -m pip install --upgrade pip setuptools virtualenv gcovr

# Software engineering - Sonar
RUN npm install -g sonarqube-scanner

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Handy aliases
RUN sed -i -e "s/#alias dir='dir --color=auto'/alias dir='ls -laFh --color=auto'/g" ${HOME}/.bashrc


