FROM centos:7
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root

#
VOLUME ["/sys/fs/cgroup", "/run", "/tmp"]

# Import the Centos-7 GPG key to prevent warnings
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7

# Update of CentOS
RUN yum -y clean all
RUN yum -y upgrade

# EPEL
RUN yum -y install epel-release

# Base install
RUN yum -y install initscripts
RUN yum -y install sudo htop less file rpmconf git-all bash-completion unzip tar wget curl which yum-utils net-utils

# Python
RUN yum -y install python34 python34-pip python34-devel pygpgme
RUN pip3 install -U pip

# Databases for Tyk
RUN yum -y install redis
RUN yum -y install mongodb-server
RUN systemctl enable redis
RUN systemctl enable mongod

# Tyk
COPY resources/tyk-dashboard.repo /etc/yum.repos.d
RUN yum -y install tyk-dashboard

# Tell Docker about the Tyk dashboard port
EXPOSE 3000

# Handy aliases
RUN echo "alias dir='ls -laFh --color'" >> $HOME/.bashrc

#
RUN echo "root:root"|chpasswd
#CMD ["/usr/sbin/init"]
CMD ["/bin/bash"]

