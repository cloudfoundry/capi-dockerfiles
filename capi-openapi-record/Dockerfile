# Image for the weekly OpenAPI traffic-recording job.
#
# It has to run three toolchains in one container: Go (capi-bara-tests),
# Node (the spec build, wiretap and the report tooling), and the cf/credhub
# CLIs (targeting a claimed bosh-lite from the pool).
FROM golang:1.23-bookworm
LABEL org.opencontainers.image.authors="CF CAPI team"
LABEL org.opencontainers.image.url="https://github.com/cloudfoundry/capi-dockerfiles"

ENV bosh_cli_version=7.10.11
ENV credhub_cli_version=2.9.29
ENV node_major=22

RUN apt-get update && \
    apt-get -y install \
      ca-certificates \
      curl \
      wget \
      gnupg \
      git \
      jq \
      unzip \
      netcat-openbsd \
      build-essential \
      python3 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Node + yarn: the spec build (redocly), wiretap and the report scripts.
RUN curl -fsSL https://deb.nodesource.com/setup_${node_major}.x | bash - && \
    apt-get -y install nodejs && \
    npm install -g yarn && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# cf CLI v8: capi-bara-tests drives it directly.
RUN curl -fsSL "https://packages.cloudfoundry.org/stable?release=linux64-binary&version=8.8.2" \
      -o /tmp/cf.tgz && \
    tar -xzf /tmp/cf.tgz -C /usr/local/bin cf8 && \
    ln -sf /usr/local/bin/cf8 /usr/local/bin/cf && \
    rm /tmp/cf.tgz && \
    cf version

# credhub CLI: reads the bosh-lite's cf_admin_password.
RUN curl -fsSL "https://github.com/cloudfoundry/credhub-cli/releases/download/${credhub_cli_version}/credhub-linux-amd64-${credhub_cli_version}.tgz" \
      -o /tmp/credhub.tgz && \
    tar -xzf /tmp/credhub.tgz -C /usr/local/bin credhub && \
    chmod +x /usr/local/bin/credhub && \
    rm /tmp/credhub.tgz && \
    credhub --version

RUN wget -q -O /usr/local/bin/bosh https://storage.googleapis.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64 && \
    chmod +x /usr/local/bin/bosh && \
    bosh --version
