#
# https://github.com/transport-intelligence/docker-images/blob/master/cpp-python/google-or-w-scip/Dockerfile 
#

FROM transportintelligence/operations-research:scip
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root
ENV DSTRB ubuntu-18.04
ENV GOR_DIR /opt/google-or
ENV GOR_VER 7.3
ENV GOR_RLS 7083
ENV GOR_TAR or-tools_${DSTRB}_v${GOR_VER}.${GOR_RLS}.tar.gz
ENV GOR_BASE_URL https://github.com/google/or-tools/releases
ENV GOR_URL ${GOR_BASE_URL}/download/v${GOR_VER}/${GOR_TAR}

# Google OR
# https://developers.google.com/optimization/install/cpp/linux
RUN mkdir -p ${GOR_DIR} && cd ${GOR_DIR} && \
  wget ${GOR_URL} && tar zxf ${GOR_TAR} && rm -f ${GOR_TAR}

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


