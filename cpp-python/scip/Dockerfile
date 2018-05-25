FROM transportintelligence/operations-research:solvers
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

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


