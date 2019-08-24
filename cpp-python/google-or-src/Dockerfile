FROM transportintelligence/operations-research:solvers
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root
ENV GOR_URL https://github.com/google/or-tools/archive
ENV GOR_DIR /opt/google-or
ENV GOR_VER 7.3
ENV GOR_TAR v$GOR_VER.tar.gz

# Update the system
RUN apt -y update && apt-get -y install zip libgflags-dev libgoogle-glog-dev libgoogle-glog0v5 \
  libprotobuf-dev libprotobuf10 libprotobuf-c-dev protobuf-c-compiler \
  coinor-cbc coinor-clp coinor-libcbc-dev coinor-libclp-dev coinor-libcgl-dev coinor-libcgl-dev coinor-libflopc++-dev coinor-libvol-dev coinor-libflopc++-dev

# Bazel
ENV BAZEL_VER 0.28.1
RUN mkdir -p /opt/bazel && cd /opt/bazel && \
    wget https://github.com/bazelbuild/bazel/releases/download/$BAZEL_VER/bazel-$BAZEL_VER-installer-linux-x86_64.sh && \
    chmod +x *.sh && \
    ./bazel-$BAZEL_VER-installer-linux-x86_64.sh

# Abseil
ENV PATH $PATH:$HOME/bin
RUN mkdir -p /opt && git clone https://github.com/abseil/abseil-cpp.git /opt/abseil && \
  mkdir -p /opt/abseil/build && cd /opt/abseil/build && \
  cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && \
  make install

# glog
RUN mkdir -p /opt && git clone https://github.com/google/glog.git /opt/glog && \
  cd /opt/glog && cmake -H. -Bbuild -G "Unix Makefiles" && \
  cmake --build build --target install

# Protobuf
ENV PB_VER 3.9.1
RUN mkdir -p /opt/protobuf && cd /opt/protobuf && \
  wget https://github.com/protocolbuffers/protobuf/releases/download/v$PB_VER/protobuf-cpp-$PB_VER.tar.gz && \
  tar zxf protobuf-cpp-$PB_VER.tar.gz && cd protobuf-$PB_VER/cmake && \
  mkdir build && cd build && \
  cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && \
  make install

# Coin OR

# Google OR
# https://developers.google.com/optimization/install/cpp/source_linux
RUN mkdir -p $GOR_DIR && cd $GOR_DIR && wget "$GOR_URL/$GOR_TAR"
RUN cd $GOR_DIR && tar zxf $GOR_TAR
RUN mkdir -p $GOR_DIR/or-tools-$GOR_VER/build && \
    cd $GOR_DIR/or-tools-$GOR_VER/build && \
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && \
    make all install

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


