FROM ruby:3.2-buster
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

ENV bosh_cli_version 7.6.2

RUN apt-get update && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q -O /usr/local/bin/bosh https://storage.googleapis.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64 && \
    chmod +x /usr/local/bin/bosh
