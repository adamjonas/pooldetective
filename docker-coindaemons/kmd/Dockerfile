FROM debian:stable-slim
LABEL MAINTAINER="Gert-Jaap Glasbergen <gertjaap@mit.edu>"
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y libgomp1 wget && wget https://github.com/KomodoPlatform/komodo/releases/download/0.6.1/komodo_linux_0.6.1.tar.gz
RUN tar xvf komodo_linux_0.6.1.tar.gz \
  && mv /linux64/* /usr/local/bin/ 

EXPOSE 7771 

ADD ./docker_entrypoint.sh /usr/local/bin/docker_entrypoint.sh
RUN chmod a+x /usr/local/bin/docker_entrypoint.sh
RUN chmod a+x /usr/local/bin/fetch-params.sh
ENTRYPOINT ["/usr/local/bin/docker_entrypoint.sh"]
