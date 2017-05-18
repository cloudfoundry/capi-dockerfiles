FROM ruby:2.3.4

RUN apt-get update && \
    apt-get -y install \
    build-essential \
    wget \
    unzip \
    proxychains \
    lsof \
    jq \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.16-linux-amd64 && \
    chmod +x /usr/local/bin/bosh
