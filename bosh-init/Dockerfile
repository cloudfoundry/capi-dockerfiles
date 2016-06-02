FROM ruby:2.3
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN set -ex \
    && apt-get update \
    && apt-get install -y \
          build-essential \
          zlibc \
          zlib1g-dev \
          openssl \
          libxslt-dev \
          libxml2-dev \
          libssl-dev \
          libreadline6 \
          libreadline6-dev \
          libyaml-dev \
          libsqlite3-dev \
          sqlite3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
    && curl -fSL -o /usr/local/bin/bosh-init \
        "https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-0.0.92-linux-amd64" \
    && chmod 0755 /usr/local/bin/bosh-init
