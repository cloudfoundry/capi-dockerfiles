FROM ubuntu:xenial-20210114

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
  apt-transport-https \
  ca-certificates \
  curl \
  dnsutils \
  git \
  iproute2 \
  openssh-client \
  software-properties-common \
  libpq-dev

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN apt-key fingerprint | grep 'Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88'
RUN add-apt-repository "deb https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-get update
RUN apt-get install -y --no-install-recommends docker-ce

RUN rm -rf /var/lib/apt/lists/*

ENV PACK_VERSION="v0.13.1"
RUN curl -LO "https://github.com/buildpacks/pack/releases/download/${PACK_VERSION}/pack-${PACK_VERSION}-linux.tgz"
RUN tar xvf "pack-${PACK_VERSION}-linux.tgz"
RUN mv pack /usr/local/bin/pack
RUN rm "pack-${PACK_VERSION}-linux.tgz"
