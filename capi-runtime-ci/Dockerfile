FROM ruby:3.2-buster
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

ENV bosh_cli_version 7.6.1

RUN apt-get update && \
    apt-get -y install \
      build-essential \
      curl \
      debconf-utils \
      git \
      libcurl4-openssl-dev \
      libpq-dev \
      libreadline-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libxslt-dev \
      libyaml-dev \
      software-properties-common \
      unzip \
      wget \
      zip \
      zlib1g-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -O /usr/local/bin/bosh https://storage.googleapis.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64 && \
    chmod +x /usr/local/bin/bosh
