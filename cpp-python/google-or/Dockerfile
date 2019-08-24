#
# https://github.com/transport-intelligence/docker-images/blob/master/cpp-python/google-or/Dockerfile 
#
FROM transportintelligence/operations-research:solvers
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
ENV GOR_TAR or-tools_${DSTRB}_v${GOR_VER}.${GOR_RLS}.tar.gz
ENV GOR_BIN_DIR ${GOR_DIR}/or-tools_${DSTRBC}-64bit_v${GOR_VER}.${GOR_RLS}/bin
ENV GOR_BASE_URL https://github.com/google/or-tools/releases
ENV GOR_URL ${GOR_BASE_URL}/download/v${GOR_VER}/${GOR_TAR}

# Google OR
# https://developers.google.com/optimization/install/cpp/linux
RUN mkdir -p ${GOR_DIR} && cd ${GOR_DIR} && \
  wget ${GOR_URL} && tar zxf ${GOR_TAR} && rm -f ${GOR_TAR}
RUN echo >> ${HOME}/.bashrc && \
  echo "# Google OR" >> ${HOME}/.bashrc && \
  echo "export PATH=\"\${PATH}:${GOR_BIN_DIR}\"" >> ${HOME}/.bashrc && \
  echo >> ${HOME}/.bashrc

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


