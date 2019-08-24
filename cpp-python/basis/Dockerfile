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
RUN apt -y update && \
  apt-get -y install apt-utils zip unzip wget htop git openssh-client vim

# C++ development
RUN apt -y install autoconf libtool zlib1g-dev lsb-release
RUN apt -y install cmake build-essential gcc-7 cppcheck clang-format-6.0
RUN apt -y install libboost1.65-all-dev
RUN apt -y install doxygen
RUN apt -y install libc6-dev-i386
RUN apt -y install libreadline-dev libgmp-dev
RUN apt -y install flex bison

# Python 2
RUN apt -y install python python-pip python-dev python-setuptools python-wheel python-six
RUN apt -y install swig
RUN python -m pip install --upgrade pip setuptools virtualenv
RUN python -m pip install --upgrade gcovr

# Python 3
RUN apt -y install python3 python3-pip python3-dev python3-setuptools python3-wheel python3-six
RUN python3 -m pip install --upgrade pip setuptools virtualenv
RUN python3 -m pip install --upgrade gcovr

# Software engineering - Sonar
RUN apt-get -y install npm
RUN npm install -g sonarqube-scanner

# Visualization
RUN apt -y install graphviz

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Handy aliases
RUN sed -i -e "s/#alias dir='dir --color=auto'/alias dir='ls -laFh --color=auto'/g" $HOME/.bashrc


