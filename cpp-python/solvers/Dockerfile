FROM transportintelligence/operations-research:basis
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root

# Update the system
RUN apt -y update

# OGDF (Open Graph)
RUN mkdir -p /opt && cd /opt && git clone https://github.com/ogdf/ogdf.git && \
    mkdir -p /opt/ogdf/build && cd /opt/ogdf/build && \
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && make -j4 install

# MiniZinc
RUN mkdir -p /opt/mzinc && cd /opt/mzinc && git clone https://github.com/MiniZinc/libminizinc.git && \
    mkdir -p /opt/mzinc/libminizinc/build && cd /opt/mzinc/libminizinc/build && \
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBUILD_SHARED_LIBS=ON .. && make -j4 install

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


