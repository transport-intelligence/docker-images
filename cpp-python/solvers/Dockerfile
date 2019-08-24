#
# https://github.com/transport-intelligence/docker-images/blob/master/cpp-python/solvers/Dockerfile
#

FROM transportintelligence/operations-research:basis
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root
ENV DSTRB_TYPE ubuntu
ENV DSTRB_TYPEC Ubuntu
ENV DSTRB_VER 18.04
ENV DSTRB ${DSTRB_TYPE}-${DSTRB_VER}
ENV DSTRBC ${DSTRB_TYPEC}-${DSTRB_VER}
ENV GOR_DIR /opt/google-or
ENV GOR_VER 7.3
ENV GOR_RLS 7083
ENV FZC_TAR or-tools_flatzinc_${DSTRB}_v${GOR_VER}.${GOR_RLS}.tar.gz
ENV FZC_BIN_DIR ${GOR_DIR}/or-tools_flatzinc_${DSTRBC}-64bit_v${GOR_VER}.${GOR_RLS}/bin
ENV GOR_BASE_URL https://github.com/google/or-tools/releases
ENV FZC_URL ${GOR_BASE_URL}/download/v${GOR_VER}/${FZC_TAR}

# OGDF (Open Graph)
RUN mkdir -p /opt && cd /opt && git clone https://github.com/ogdf/ogdf.git && \
    mkdir -p /opt/ogdf/build && cd /opt/ogdf/build && \
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && make -j4 install

# MiniZinc
RUN mkdir -p /opt/mzinc && cd /opt/mzinc && git clone https://github.com/MiniZinc/libminizinc.git && \
    mkdir -p /opt/mzinc/libminizinc/build && cd /opt/mzinc/libminizinc/build && \
    export CXXFLAGS="$CXXFLAGS -fPIC" && \
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && make -j4 install

# FlatZinc
# https://developers.google.com/optimization/install/cpp/linux
RUN mkdir -p ${GOR_DIR} && cd ${GOR_DIR} && \
  wget ${FZC_URL} && tar zxf ${FZC_TAR} && rm -f ${FZC_TAR} 
RUN echo >> ${HOME}/.bashrc && \
  echo "# (Google OR) FlatZinc" >> ${HOME}/.bashrc && \
  echo "export PATH=\"\${PATH}:${FZC_BIN_DIR}\"" >> ${HOME}/.bashrc && \
  echo >> ${HOME}/.bashrc

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


