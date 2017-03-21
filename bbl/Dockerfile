FROM ruby:2.3
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN \
  apt-get update && \
  apt-get -y install \
    build-essential \
    curl \
    jq \
    mercurial \
    software-properties-common \
    wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
    && curl -fSL -o /usr/local/bin/bosh-init \
        "https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-0.0.92-linux-amd64" \
    && chmod 0755 /usr/local/bin/bosh-init

RUN wget "$(curl -s https://api.github.com/repos/cloudfoundry/bosh-bootloader/releases | jq -r 'map(select((.prerelease == false) and (.draft == false) and (.tag_name|startswith("v2"))))[0].assets[].browser_download_url' | grep _linux)" && \
  mv bbl-* /usr/local/bin/bbl && \
  chmod +x /usr/local/bin/bbl
