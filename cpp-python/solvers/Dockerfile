FROM transportintelligence/operations-research:basis
MAINTAINER Denis Arnaud <denis.arnaud_github at m4x dot org>
LABEL version="0.1"

# Environment
ENV HOME /root
ENV SCIP_DIR /opt/scip
ENV SCIP_VER 5.0.1
ENV SCIP_TAR scipoptsuite-$SCIP_VER.tgz

# Update the system
RUN apt -y update

# SCIP
RUN mkdir -p /opt/scip
COPY resources/$SCIP_TAR $SCIP_DIR
RUN cd $SCIP_DIR && tar zxf $SCIP_TAR
RUN cd $SCIP_DIR/scipoptsuite-$SCIP_VER && \
    make -j4 TPI=tny USRCFLAGS=-fPIC USRCXXFLAGS=-fPIC USRCPPFLAGS=-fPIC install # GMP=false READLINE=false
RUN rm -f $SCIP_DIR/$SCIP_TAR

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


