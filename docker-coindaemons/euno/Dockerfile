## Original from: https://github.com/jamesob/docker-bitcoind
FROM ubuntu:18.04 as build-env
LABEL MAINTAINER="Gert-Jaap Glasbergen <gertjaap@mit.edu>"
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install libdb5.3 libdb5.3++  libdb5.3-dev libdb5.3++-dev libssl1.0-dev libevent-dev  libboost-all-dev git apt-utils build-essential libtool autotools-dev automake pkg-config bsdmainutils curl software-properties-common cmake libcap-dev librsvg2-bin libz-dev libbz2-dev libtiff-tools python3-pip imagemagick
RUN mkdir /sources && cd /sources && git clone https://github.com/Euno/eunowallet && cd /sources/eunowallet && git reset 90bdcccda9eb0eee66e8b7f7d5c637afe27efaf3 --hard
RUN apt-get -y install libminiupnpc-dev
COPY rpcblockchain.cpp /sources/eunowallet/src/
WORKDIR /sources/eunowallet/src
RUN make -f makefile.unix

FROM ubuntu:18.04
RUN apt-get update && apt-get -y install libdb5.3 libdb5.3++ libssl1.0 libevent-2.1-6 libevent-pthreads-2.1-6 libboost-program-options1.65.1 libboost-system1.65 libboost-filesystem1.65 libboost-chrono1.65 libboost-thread1.65
RUN apt-get -y install libminiupnpc10
COPY --from=build-env /sources/eunowallet/src/euno* /usr/local/bin/
RUN mkdir /root/.euno
EXPOSE 9332

ADD ./docker_entrypoint.sh /usr/local/bin/docker_entrypoint.sh
RUN chmod a+x /usr/local/bin/docker_entrypoint.sh

ENTRYPOINT ["/usr/local/bin/docker_entrypoint.sh"]
