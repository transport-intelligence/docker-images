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

#
RUN sed -e "s/#alias dir='dir --color=auto'/alias dir='ls -laFh --color=auto'/g" /root/.bashrc

# OGDF
RUN mkdir -p /opt && cd /opt && git clone https://github.com/ogdf/ogdf.git && \
    mkdir -p /opt/ogdf/build && cd /opt/ogdf/build && cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && make install


