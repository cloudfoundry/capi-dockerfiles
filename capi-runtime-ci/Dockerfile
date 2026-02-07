FROM ruby:3.2-bookworm
LABEL org.opencontainers.image.authors="CF CAPI team"
LABEL org.opencontainers.image.url="https://github.com/cloudfoundry/capi-dockerfiles"

ENV bosh_cli_version=7.9.17

RUN apt-get update && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q -O /usr/local/bin/bosh https://storage.googleapis.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64 && \
    chmod +x /usr/local/bin/bosh

RUN wget -q -O /tmp/protoc.zip https://github.com/protocolbuffers/protobuf/releases/download/v3.6.1/protoc-3.6.1-linux-x86_64.zip && \
    unzip -q /tmp/protoc.zip -d /usr/local && \
    rm /tmp/protoc.zip
