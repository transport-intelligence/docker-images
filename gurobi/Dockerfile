FROM ubuntu:18.04
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

#
RUN apt -y update
RUN apt -y install unzip cmake doxygen build-essential gcc-7 wget
RUN apt -y install graphviz git
RUN apt -y install python clang-format-6.0
RUN apt -y install openssh-client
RUN apt -y install cppcheck unzip python-pip
RUN apt -y install libboost1.65-all-dev
RUN pip install gcovr
RUN apt -y install libc6-dev-i386
RUN wget -q -O sonar-scanner.zip https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.0.3.778-linux.zip && \
 unzip -q sonar-scanner.zip && \
 DIR=`pwd` && ln -s $DIR/sonar-scanner-3.0.3.778-linux/bin/sonar-scanner /bin && \
 rm sonar-scanner.zip
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

