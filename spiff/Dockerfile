FROM ubuntu:trusty

RUN set -ex \
  && apt-get update \
  && apt-get -y install \
    wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
  && wget https://github.com/cloudfoundry-incubator/spiff/releases/download/v1.0.7/spiff_linux_amd64 \
    -O /usr/bin/spiff \
  && chmod 0755 /usr/bin/spiff
