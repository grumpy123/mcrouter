# NOTE: much of this was taken from
# https://github.com/facebook/mcrouter/blob/b47a22b78ce170fdc0d8b205c7189e1226c028d1/mcrouter/scripts/docker/Dockerfile
# Update MCROUTER_BRANCH to build specific versions.

FROM ubuntu:22.04 AS production

MAINTAINER reddit <infrastructure@reddit.com>

ENV MCROUTER_DIR /usr/local/mcrouter
ENV DEBIAN_FRONTEND noninteractive
ENV DUMB_INIT 1.2.5

RUN apt-get update && apt-get install -y git sudo wget bash
RUN wget -O /tmp/dumb-init.deb "https://github.com/Yelp/dumb-init/releases/download/v${DUMB_INIT}/dumb-init_${DUMB_INIT}_amd64.deb"
RUN dpkg -i /tmp/dumb-init.deb
RUN rm /tmp/dumb-init.deb
RUN apt-get remove -y wget

RUN mkdir -p $MCROUTER_DIR/src
COPY . $MCROUTER_DIR/src/

RUN $MCROUTER_DIR/src/mcrouter/scripts/install_ubuntu_22.04.sh $MCROUTER_DIR
RUN rm -rf $MCROUTER_DIR/src
RUN ln -s $MCROUTER_DIR/install/bin/mcrouter /usr/local/bin/mcrouter

ENV DEBIAN_FRONTEND newt
