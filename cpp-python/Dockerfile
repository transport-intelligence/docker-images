FROM ubuntu:18.04
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root
ENV SCIP_DIR /opt/scip
ENV SCIP_VER 5.0.1
ENV SCIP_TAR scipoptsuite-$SCIP_VER.tgz
ENV GOR_URL https://github.com/google/or-tools/archive
ENV GOR_DIR /opt/google-or
ENV GOR_TAR v6.7.1.tar.gz

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

# Python 2
RUN apt -y install python python-pip python-dev python-setuptools python-wheel python-six
RUN apt -y install swig
RUN python -m pip install --upgrade pip setuptools
RUN python -m pip install --upgrade gcovr

# Python 3
RUN apt -y install python3 python3-pip python3-dev python3-setuptools python3-wheel python3-six
RUN python3 -m pip install --upgrade pip setuptools
RUN python3 -m pip install --upgrade gcovr

# Software engineering - Sonar
RUN wget -q -O sonar-scanner.zip https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.0.3.778-linux.zip && \
 unzip -q sonar-scanner.zip && \
 DIR=`pwd` && ln -s $DIR/sonar-scanner-3.0.3.778-linux/bin/sonar-scanner /bin && \
 rm sonar-scanner.zip

# Visualization
RUN apt -y install graphviz

# Operations Research
## SCIP
RUN mkdir -p /opt/scip
COPY resources/$SCIP_TAR $SCIP_DIR
RUN cd $SCIP_DIR && tar zxf $SCIP_TAR
RUN cd $SCIP_DIR/scipoptsuite-$SCIP_VER make -j4 TPI=tny USRCFLAGS=-fPIC USRCXXFLAGS=-fPIC USRCPPFLAGS=-fPIC # GMP=false READLINE=false

## Google OR
RUN mkdir -p $GOR_DIR && cd $GOR_DIR && wget "$GOR_URL/$GOR_TAR"
RUN cd $GOR_DIR && tar zxf $GOR_TAR

## OGDF (Open Graph)
RUN mkdir -p /opt && cd /opt && git clone https://github.com/ogdf/ogdf.git && \
    mkdir -p /opt/ogdf/build && cd /opt/ogdf/build && cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && make -j4 install

## MiniZinc
#RUN mkdir -p /opt/mzinc && cd /opt/mzinc && git clone https://github.com/MiniZinc/libminizinc.git && \
#    mkdir -p /opt/mzinc/libminizinc/build && cd /opt/mzinc/libminizinc/build && cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. && make -j4 install

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Handy aliases
RUN sed -i -e "s/#alias dir='dir --color=auto'/alias dir='ls -laFh --color=auto'/g" $HOME/.bashrc


