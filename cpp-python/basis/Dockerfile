FROM ubuntu:18.04
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root

# Update the system
RUN apt -y update

# Basic tools
RUN apt -y install unzip wget htop
RUN apt -y install git openssh-client

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
RUN wget -q -O sonar-scanner.zip https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.0.3.778-linux.zip && \
 unzip -q sonar-scanner.zip && \
 DIR=`pwd` && ln -s $DIR/sonar-scanner-3.0.3.778-linux/bin/sonar-scanner /bin && \
 rm -f sonar-scanner.zip

# Visualization
RUN apt -y install graphviz

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Handy aliases
RUN sed -i -e "s/#alias dir='dir --color=auto'/alias dir='ls -laFh --color=auto'/g" $HOME/.bashrc


