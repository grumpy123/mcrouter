# NOTE: much of this was taken from
# https://github.com/facebook/mcrouter/blob/b47a22b78ce170fdc0d8b205c7189e1226c028d1/mcrouter/scripts/docker/Dockerfile
# Update MCROUTER_BRANCH to build specific versions.

FROM            ubuntu:22.04 AS production

MAINTAINER      reddit <infrastructure@reddit.com>

ENV             MCROUTER_BRANCH         kko-jammy
ENV             MCROUTER_DIR            /usr/local/mcrouter
#ENV             MCROUTER_REPO           https://github.com/facebook/mcrouter.git
ENV             MCROUTER_REPO           https://github.com/grumpy123/mcrouter.git
ENV             DEBIAN_FRONTEND         noninteractive
ENV             DUMB_INIT               1.2.5

RUN             apt-get update && apt-get install -y git sudo wget bash && \
                # ubuntu:16.04 package distro does not have dumb-init
                wget -O /tmp/dumb-init.deb "https://github.com/Yelp/dumb-init/releases/download/v${DUMB_INIT}/dumb-init_${DUMB_INIT}_amd64.deb" && \
                dpkg -i /tmp/dumb-init.deb && \
                rm /tmp/dumb-init.deb && \
                apt-get remove -y wget && \
                mkdir -p $MCROUTER_DIR/repo && \
                cd $MCROUTER_DIR/repo && git clone $MCROUTER_REPO && \
                cd $MCROUTER_DIR/repo/mcrouter/mcrouter/scripts && \
                git checkout $MCROUTER_BRANCH && \
                ./install_ubuntu_22.04.sh $MCROUTER_DIR && \
                rm -rf $MCROUTER_DIR/repo && \
                ln -s $MCROUTER_DIR/install/bin/mcrouter /usr/local/bin/mcrouter

ENV             DEBIAN_FRONTEND newt
