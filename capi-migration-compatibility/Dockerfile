FROM ruby:3.2-buster
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

ENV bosh_cli_version 7.6.2
ENV bbl_version 9.0.23

RUN apt-get update && \
    apt-get -y install \
      build-essential \
      wget \
      xz-utils \
      lsof \
      jq \
      vim \
      netcat-openbsd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q -O /usr/local/bin/bosh https://storage.googleapis.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64 && \
    chmod +x /usr/local/bin/bosh

RUN wget -q -O /usr/local/bin/bbl https://github.com/cloudfoundry/bosh-bootloader/releases/download/v${bbl_version}/bbl-v${bbl_version}_linux_amd64 && \
    chmod +x /usr/local/bin/bbl
